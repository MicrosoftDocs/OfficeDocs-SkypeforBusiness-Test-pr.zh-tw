---
title: Move-CsExUmContact
TOCTitle: Move-CsExUmContact
ms:assetid: 35ed6bdc-95ea-4bf8-84ce-c4256dc2c4e5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425842(v=OCS.15)
ms:contentKeyID: 49290565
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Move-CsExUmContact

 

_**上次修改主題的時間：** 2015-03-09_

將一或多位 Exchange 整合通訊 (UM) 連絡人移至新的登錄器集區。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Move-CsExUmContact -Identity <UserIdParameter> -Target <Fqdn> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-IgnoreBackendStoreException <SwitchParameter>] [-PassThru <SwitchParameter>] [-ProxyPool <Fqdn>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會將 SIP 位址為 exum1@fabrikam.com 的 Exchange UM 連絡人物件移到 FQDN 為 atl-cs-001.litwareinc.com 的登錄器集區。請注意，執行此命令時，即使未加入 Confirm 參數也會在畫面上顯示確認提示。即使加入 Force 參數，一樣會出現此提示。

    Move-CsExUmContact -Identity "sip:exum1@fabrikam.com" -Target atl-cs-001.litwareinc.com

## 範例 2

此範例會將屬於「自動語音應答」的所有 Exchange UM 連絡人物件移到 FQDN 為 atl-cs-001.litwareinc.com 的登錄器集區。範例會先呼叫 **Get-CsExUmContact** Cmdlet，以擷取已經定義的所有 Exchange UM 連絡人。然後將這個連絡人集合管線傳送到 **Where-Object** Cmdlet，以在集合中尋找 AutoAttendant 內容值為 True ($True) 的所有連絡人，該值表示連絡人屬於「自動語音應答」。

最後，會將 AutoAttendant 為 True 的連絡人集合傳送到 **Move-CsExUmContact** Cmdlet，以將這些連絡人移到 Target 參數中指定的登錄器集區。

如範例 1 所示，執行此命令時，會出現確認提示。

    Get-CsExUmContact | Where-Object {$_.AutoAttendant -eq $True} | Move-CsExUmContact -Target atl-cs-001.litwareinc.com

## 詳細描述

Lync Server 搭配 Exchange UM 運作提供多項語音相關功能，包括自動語音應答和訂閱者存取。**Move-CsExUmContact** Cmdlet 提供一個方法，讓您將現有的 Exchange UM 連絡人物件移到新的登錄器集區。

移動 Exchange UM 連絡人物件時，會根據該物件的 OtherIpPhone 內容值適當地設定 AutoAttendant 和 IsSubscriberAccess 內容。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Move-CsExUmContact** Cmdlet：RTCUniversalUserAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Move-CsExUmContact"}

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
<td><p>您要移動之連絡人物件的唯一識別碼。可以使用下列四種格式的其中一種來指定連絡人識別身分：1) 連絡人的 SIP 位址；2) 連絡人的使用者主體名稱 (UPN)；3) 連絡人的網域名稱和登入名稱，必須是「網域\登入」格式 (例如，litwareinc\exum1)；以及 4) 連絡人的 Active Directory 顯示名稱 (例如，Team Auto Attendant)。</p></td>
</tr>
<tr class="even">
<td><p><em>Target</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>連絡人要移往之登錄器集區的完整網域名稱 (FQDN)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>可讓您連線至指定的網域控制站。若要連線至特定的網域控制站，請加入 DomainController 參數，後面加上電腦名稱 (例如，atl-mcs-001) 或其 FQDN (例如，atl-mcs-001.litwareinc.com)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreBackendStoreException</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定此參數，會指示電腦忽略後端資料庫可能發生的任何錯誤，並嘗試移動連絡人，而不管那些錯誤。</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>讓您透過管線傳遞連絡人物件，代表被移動的連絡人帳戶。根據預設，<strong>Move-CsExUmContact</strong> Cmdlet 不會透過管線傳遞物件。</p></td>
</tr>
<tr class="even">
<td><p><em>ProxyPool</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>此參數只能用於主控的 Lync Server 執行個體。請勿用於 Lync Server 的內部部署實作。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

字串。接受管線傳送的字串值，代表要移動之 Exchange UM 物件的 Identity。

## 傳回類型

使用 PassThru 參數呼叫時，會傳回 Microsoft.Rtc.Management.ADConnect.Schema.OCSADExUmContact 類型的物件。

## 請參閱

#### 其他資源

[New-CsExUmContact](new-csexumcontact.md)  
[Remove-CsExUmContact](remove-csexumcontact.md)  
[Set-CsExUmContact](set-csexumcontact.md)  
[Get-CsExUmContact](get-csexumcontact.md)

