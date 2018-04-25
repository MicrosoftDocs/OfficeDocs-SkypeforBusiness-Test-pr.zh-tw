---
title: New-CsTrustedApplicationEndpoint
TOCTitle: New-CsTrustedApplicationEndpoint
ms:assetid: 78b34ba4-4c31-4f68-9069-3c7e7c162fbf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398594(v=OCS.15)
ms:contentKeyID: 49291388
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsTrustedApplicationEndpoint

 

_**上次修改主題的時間：** 2015-03-09_

建立信任之應用程式的新端點連絡人。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsTrustedApplicationEndpoint -ApplicationId <String> -TrustedApplicationPoolFqdn <Fqdn> [-Confirm [<SwitchParameter>]] [-DisplayName <String>] [-DisplayNumber <String>] [-LineURI <String>] [-PassThru <SwitchParameter>] [-PrimaryLanguage <String>] [-SecondaryLanguages <MultiValuedProperty>] [-SipAddress <String>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

這個範例為應用程式識別碼 tapp1 設在 TrustPool.litwareinc.com 集區之應用程式建立信任的應用程式端點。ApplicationID 和 TrustedApplicationPoolFqdn 是唯一需要建立信任的應用程式端點的參數。不過，請記住，只將值指派給這兩個參數會自動產生連絡人的 SIP 位址。為了確保 SIP 位址是唯一的，自動產生位址會加入全域唯一識別碼 (GUID)，如以下範例所示：sip:RtcApplication-fbf9e2d1-c6aa-45a3-a045-b92d4ef961b2@litwareinc.com。如果您希望 SIP 位址更方便讀取，請參閱範例 2。

    New-CsTrustedApplicationEndpoint -ApplicationId tapp1 -TrustedApplicationPoolFqdn TrustPool.litwareinc.com

## 範例 2

範例 2 與範例 1 的相同點在於其為應用程式識別碼 tapp1 設在 TrustPool.litwareinc.com 集區之應用程式建立信任的應用程式端點。但與範例 1 不同的是，我們在建立端點時多加了一個參數：SipAddress。我們指定了 endpoint1@litwareinc.com 的位址，而非容許系統產生 SIP 位址。

    New-CsTrustedApplicationEndpoint -ApplicationId tapp1 -TrustedApplicationPoolFqdn TrustPool.litwareinc.com -SipAddress sip:endpoint1@litwareinc.com

## 詳細描述

信任的應用程式端點是 Active Directory 連絡人物件，可讓呼叫路由傳送至信任的應用程式。這個 Cmdlet 會在指定的應用程式的 Active Directory 網域服務 中建立新端點連絡人物件。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsTrustedApplicationEndpoint** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsTrustedApplicationEndpoint"}

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
<td><p><em>ApplicationId</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要為其建立端點連絡人的信任的應用程式之應用程式識別碼。具有此識別碼的應用程式必須已經存在。請注意，您只能加入應用程式識別碼的名稱部分，無需加入首碼資訊。例如，如果應用程式識別碼為 urn:application:TrustedApp1，則只需傳遞字串 TrustedApp1 至此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>TrustedApplicationPoolFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>與應用程式相關聯的信任應用程式集區的完整網域名稱 (FQDN)。應用程式必須已經和此集區相關聯才能建立端點。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>端點連絡人物件的顯示名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayNumber</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>將在通訊錄中顯示的連絡人電話號碼。</p></td>
</tr>
<tr class="even">
<td><p><em>LineURI</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>連絡人的電話號碼。格式必須為 TEL:&lt;number&gt;，例如 TEL:+14255551212。</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回此命令的結果。執行此 Cmdlet 會顯示新建立的物件；加上此參數只會重複該輸出，導致此參數變得多餘。</p></td>
</tr>
<tr class="even">
<td><p><em>PrimaryLanguage</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>受信任應用程式所使用的主要語言。必須使用有效的語言代碼來設定該語言，例如 en-US (美國英文)、fr-FR (法文) 等等。</p></td>
</tr>
<tr class="odd">
<td><p><em>SecondaryLanguages</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.MultiValuedProperty</p></td>
<td><p>也可用於受信任應用程式的語言集合。必須將值設定為以逗號分隔的語言代碼清單。例如，下列語法可將法文 (加拿大) 和法文設為次要語言：-SecondaryLanguages &quot;fr-CA&quot;,&quot;fr-FR&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>SipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>新連絡人物件的 SIP 位址。如果您沒有加入此參數值，會以格式 sip:RtcApplication-&lt;GUID&gt;.&lt;domain&gt; 自動產生 SIP 位址，例如，sip:RtcApplication-fbf9e2d1-c6aa-45a3-a045-b92d4ef961b2@litwareinc.com。該網域為預設的 SIP 網域。</p></td>
</tr>
<tr class="odd">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要為其建立新受信任應用程式集區端點之 Office 365 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行此命令來傳回每位租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName，TenantID</p></td>
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

無。

## 傳回類型

建立 Microsoft.Rtc.Management.ADConnect.Schema.OCSADApplicationContact 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsTrustedApplicationEndpoint](remove-cstrustedapplicationendpoint.md)  
[Set-CsTrustedApplicationEndpoint](set-cstrustedapplicationendpoint.md)  
[Get-CsTrustedApplicationEndpoint](get-cstrustedapplicationendpoint.md)

