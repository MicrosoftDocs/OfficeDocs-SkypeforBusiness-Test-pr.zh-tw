---
title: 規劃雙因素驗證
TOCTitle: 規劃雙因素驗證
ms:assetid: 16f08710-8961-4659-acbf-ebb95a198fb4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn308562(v=OCS.15)
ms:contentKeyID: 56269070
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 規劃雙因素驗證

 

_**上次修改主題的時間：** 2015-04-06_

以下是設定 Microsoft Lync Server 2013 環境以支援雙因素驗證時的部署考量清單。

## 用戶端支援

Lync 2013 的 Lync Server 2013 累計更新 (2013 年 7 月) 桌面用戶端是目前唯一支援雙因素驗證的 Lync 用戶端。

## 拓撲需求

我們極力建議客戶使用具備 Lync Server 2013 累計更新 (2013 年 7 月) 的專屬 Lync Server 2013 Edge、Director 和 User 集區部署雙因素驗證。若要為 Lync 使用者啟用被動式驗證，必須為其他角色和服務停用其他驗證方法，包括下列項目：


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>組態類型</th>
<th>服務類型</th>
<th>伺服器角色</th>
<th>要停用的驗證類型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Web 服務</p></td>
<td><p>WebServer</p></td>
<td><p>Director</p></td>
<td><p>Kerberos、NTLM 和憑證</p></td>
</tr>
<tr class="even">
<td><p>Web 服務</p></td>
<td><p>WebServer</p></td>
<td><p>前端</p></td>
<td><p>Kerberos、NTLM 和憑證</p></td>
</tr>
<tr class="odd">
<td><p>Proxy</p></td>
<td><p>EdgeServer</p></td>
<td><p>Edge</p></td>
<td><p>Kerberos 和 NTLM</p></td>
</tr>
<tr class="even">
<td><p>Proxy</p></td>
<td><p>登錄器</p></td>
<td><p>前端</p></td>
<td><p>Kerberos 和 NTLM</p></td>
</tr>
</tbody>
</table>


除非於服務層級停用這些驗證類型，否則一旦在您的部署內啟用雙因素驗證，所有其他 Lync 用戶端版本都將無法成功登入。

## Lync 服務探索

內部和/或外部用戶端用以探索 Lync 服務的 DNS 記錄應設為解析成未啟用雙因素驗證的 Lync 伺服器。使用此一組態，未啟用雙因素驗證的 Lync 集區使用者將不需要輸入 PIN 進行驗證，而啟用了雙因素驗證的 Lync 集區使用者會需要輸入 PIN 進行驗證。

## Exchange 驗證

為 Microsoft Exchange 部署了雙因素驗證的客戶可能會發現 Lync 用戶端中的某些功能無法使用。現階段而言，這是特意的設計，因為 Lync 用戶端並未針對相依於 Exchange 整合的功能支援雙因素驗證。

## Lync 連絡人

設為運用整合連絡人存放區功能的 Lync 使用者會發現使用雙因素驗證登入後無法使用本身的連絡人。

您應在啟用雙因素驗證之前，使用 **Invoke-CsUcsRollback** Cmdlet 從整合連絡人存放區移除現有的使用者連絡人，並將連絡人儲存於 Lync Server 2013。

## 技能搜尋

已於本身 Lync 環境中設定技能搜尋功能的客戶，會發現當 Lync 啟用雙因素驗證時，無法使用此功能。這是特意的設計，因為 Microsoft SharePoint 目前不支援雙因素驗證。

## Lync 認證

有一些和儲存之 Lync 認證相關的部署考量，可能會對設定為使用雙因素驗證的使用者有所影響。

## 刪除儲存的認證

使用者應在 Lync 用戶端上使用 **\[刪除我的登入資訊\]** 選項，並在第一次嘗試使用雙因素驗證登入前，從 %localappdata%\\Microsoft\\Office\\15.0\\Lync 刪除自己的 SIP 設定檔資料夾。

## DisableNTCredentials

採用 Kerberos 或 NTLM 驗證方法，就會自動使用 Windows 認證來進行驗證。在啟用 Kerberos 和/或 NTLM 驗證的典型 Lync Server 2013 部署中，使用者應不需在每次登入時輸入認證。

如果系統在提示使用者輸入 PIN 之前，意外提示使用者輸入認證，代表可能不慎透過群組原則在用戶端電腦上設定了 **DisableNTCredentials** 登錄機碼。

若要避免出現額外的輸入認證提示，請於本機工作站上建立下列登錄項目，或使用 Lync 系統管理範本透過群組原則套用到特定集區的所有使用者。

HKEY\_LOCAL\_MACHINE\\Software\\Policies\\Microsoft\\Office\\15.0\\Lync

REG\_DWORD：DisableNTCredentials

數值：0x0

## SavePassword

當使用者第一次登入 Lync 時，會提示使用者儲存密碼。如果選取此選項，會允許使用者將用戶端憑證儲存於個人憑證存放區，並將使用者的 Windows 認證儲存於本機電腦的認證管理員。

當 Lync 設為支援雙因素驗證時，應停用 **SavePassword** 登錄設定。若要防止使用者儲存密碼，請變更本機工作站上的下列登錄項目，或使用 Lync 系統管理範本透過群組原則套用到特定集區的所有使用者。

HKEY\_CURRENT\_USER\\Software\\Microsoft\\Office\\15.0\\Lync

REG\_DWORD：SavePassword

數值：0x0

## AD FS 2.0 權杖重播

AD FS 2.0 提供稱為權杖重播偵測的功能，該功能可以偵測出多個使用相同權杖的權杖要求並加以捨棄。當此功能啟用時，權杖重播偵測可以透過確保相同權杖不會重複使用，保護 WS-同盟被動式設定檔和 SAML WebSSO 設定檔中驗證要求的完整性。

此功能應於需要較高安全性的情況 (例如使用資訊站) 下啟用。如需更多有關權杖重播偵測的資訊，請參閱＜AD FS 2.0 安全規劃與部署最佳做法＞(英文)，網址為：[http://go.microsoft.com/fwlink/p/?LinkId=309215](http://go.microsoft.com/fwlink/p/?linkid=309215)。

## 外部使用者存取

上述主題並不包括設定 ADFS Proxy 或反向 Proxy 從外部網路支援 Lync 雙因素驗證等內容。

