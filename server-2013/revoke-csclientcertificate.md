---
title: Revoke-CsClientCertificate
TOCTitle: Revoke-CsClientCertificate
ms:assetid: 27d6d4d9-f8ed-4942-b7cf-dd308dafb5bc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425748(v=OCS.15)
ms:contentKeyID: 49290415
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Revoke-CsClientCertificate

 

_**上次修改主題的時間：** 2015-03-09_

用戶端憑證可讓使用者在登入 Lync Server 時通過驗證。對於電話和其他執行 Lync Mobile 的裝置而言，因為輸入使用者名稱和/或密碼不易，所以更顯憑證的實用。**Revoke-CsClientCertificate** Cmdlet 可讓系統管理員撤銷發行給使用者的用戶端憑證。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Revoke-CsClientCertificate -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會撤銷目前指派給 Ken Myer 的所有用戶端憑證；作法是呼叫 **Revoke-CsClientCertificate** Cmdlet 加上要撤銷憑證之使用者的 Identity。

    Revoke-CsClientCertificate -Identity "Ken Myer"

## 範例 2

範例 2 撤銷組織中已發行的所有用戶端憑證。為達成此目的，會先呼叫 **Get-CsUser** Cmdlet 以傳回組織中已啟用 Lync Server 之所有使用者的集合。接著，此集合會管線傳送到 **Revoke-CsClientCertificate** Cmdlet，以刪除集合中每位使用者的憑證。

    Get-CsUser | Revoke-CsClientCertificate

## 詳細描述

用戶端憑證提供使用者另一種獲得 Lync Server 驗證的方法。使用者向系統出示 X.509 憑證，而不提供使用者名稱和密碼 (此憑證必須具有可識別使用者的主體名稱或主體別名)。若要獲得驗證，使用者只需要輸入個人識別碼 (PIN)；通常，對於行動電話使用者而言，輸入 PIN 比輸入英數字元使用者名稱和/或密碼容易。

系統管理員隨時可以使用 **Revoke-CsClientCertificate** Cmdlet，撤銷已發行給使用者的用戶端憑證。**Revoke-CsClientCertificate** Cmdlet 會從伺服器撤銷已發行給不確定使用者的所有用戶端憑證。

**Revoke-CsClientCertificate** Cmdlet 不會從用戶端裝置本身刪除憑證；而是只從伺服器刪除憑證。不過，這已足夠防止用戶端使用憑證進行驗證：因為如果在伺服器上找不到憑證，則驗證要求將會遭到拒絕。

請注意，當您安裝 Lync Server 標準版時，預設不會啟用 SQL Server Express 的防火牆例外。因此，這表示您無法從 Windows PowerShell 的遠端執行個體執行 **Revoke-CsClientCertificate** Cmdlet，因為您的命令無法周遊防火牆並存取 SQL Server Express 資料庫 (不過，您仍可在本機執行 Cmdlet；亦即，在 Standard Edition Server 本身)。如果使用標準版且必須從遠端執行 **Revoke-CsClientCertificate** Cmdlet，您必須手動啟用 SQL Server Express 的防火牆例外。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Revoke-CsClientCertificate** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Revoke-CsClientCertificate"}

## 參數


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>必要</th>
<th>類型</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>表示要撤銷憑證之使用者帳戶的 Identity。可以使用下列四種格式的其中一種來指定使用者識別：1) 使用者的工作階段初始通訊協定 (SIP) 位址；2) 使用者的主體名稱；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (例如，litwareinc\kenmyer)；以及 4) 使用者的 Active Directory 顯示名稱 (例如，Ken Myer)。也可以透過使用者的 Active Directory 辨別名稱來參考使用者識別。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

字串值或 Microsoft.Rtc.Management.ADConnect.Schema.ADUser 物件。**Revoke-CsClientCertificate** Cmdlet 接受代表使用者帳戶 Identity 之字串值的管線傳送資料。Cmdlet 也接受管線傳送的使用者物件輸入。

## 傳回類型

無。反之，**Revoke-CsClientCertificate** Cmdlet 會撤銷 Microsoft.Rtc.Management.UserPinService.CertInfoDetails 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsClientCertificate](get-csclientcertificate.md)

