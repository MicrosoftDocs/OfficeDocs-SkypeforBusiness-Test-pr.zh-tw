---
title: New-CsExUmContact
TOCTitle: New-CsExUmContact
ms:assetid: 085d0a0f-0efb-4c65-b742-2c1cb7a5ae8f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398139(v=OCS.15)
ms:contentKeyID: 49290006
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsExUmContact

 

_**上次修改主題的時間：** 2015-03-09_

為代管的 Exchange 整合通訊 (UM) 建立新的自動語音應答或使用者存取連絡人物件。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsExUmContact -DisplayNumber <String> -OU <OUIdParameter> -RegistrarPool <Fqdn> -SipAddress <String> [-AutoAttendant <$true | $false>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會呼叫 **New-CsExUmContact** Cmdlet，以建立新的 Exchange UM Active Directory 連絡人物件。若要建立新連絡人，您必須提供自動語音應答或使用者存取的 SIP 位址 (此範例中為 sip:exumsa1@fabrikam.com)。此外，您必須提供正在執行 Lync Server 登錄器服務之集區的名稱 (RedmondPool.litwareinc.com)、將儲存此資訊的 OU (OU=ExUmContacts,DC=litwareinc,DC=com)，以及自動語音應答或使用者存取 (2065554567) 的電話號碼。因為我們未明確設定 AutoAttendant 參數，所以會套用預設值 False，且會假設此連絡人物件為使用者存取連絡人。

    New-CsExUmContact -SipAddress sip:exumsa1@fabrikam.com -RegistrarPool RedmondPool.litwareinc.com -OU "OU=ExUmContacts,DC=litwareinc,DC=com" -DisplayNumber 2065554567

## 範例 2

此範例與範例 1 類似，會呼叫 **New-CsExUmContact** Cmdlet 建立新的 Exchange UM 連絡人。我們再次建立新的自動語音應答或使用者存取連絡人，這一次使用 SIP 位址 sip:exumaa1@fabrikam.com。接著會提供正在執行 Lync Server 登錄器服務之集區的名稱 (RedmondPool.litwareinc.com)、將儲存此資訊的 OU (OU=ExUmContacts,DC=litwareinc,DC=com)，以及自動語音應答或使用者存取 (2065554567) 的電話號碼。此範例中的差別在於將選用參數 AutoAttendant 設為 True ($True)，以表示此物件實際上是自動語音應答連絡人。

    New-CsExUmContact -SipAddress sip:exumaa1@fabrikam.com -RegistrarPool RedmondPool.litwareinc.com -OU "OU=ExUmContacts,DC=litwareinc,DC=com" -DisplayNumber 2065559876 -AutoAttendant $True

## 詳細描述

Lync Server 搭配 Exchange UM 一起提供多項語音相關功能，包括自動語音應答和使用者存取。以託管服務 (非內部部署) 形式提供 Exchange UM 時，必須以此 Cmdlet 建立連絡人物件，以套用自動語音應答和使用者存取功能。您可以呼叫 **New-CsExUmContact** Cmdlet 來建立這些物件。

必須套用設定連絡人路由的託管語音信箱原則，使用此 Cmdlet 所建立的連絡人物件才可在系統內使用。您可以呼叫 **Get-CsHostedVoicemailPolicy** Cmdlet 來擷取託管的語音信箱原則。從擷取的原則中，您可以判斷是否存在適當的全域或網站原則，或是否存在需要授與此連絡人的個別使用者原則。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsExUmContact** Cmdlet：RTCUniversalUserAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsExUmContact"}

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
<td><p><em>DisplayNumber</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>連絡人的電話號碼。每一個連絡人的顯示號碼必須是唯一的 (例如，兩個 Exchange UM 連絡人不能有相同的顯示號碼)。</p>
<p>此值的開頭可以是加號 (+) 且可以包含任何數目的數字。第一個位數不能為零。</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>此連絡人在 Active Directory 中所在的組織單位 (OU)。</p>
<p>完整資料類型：Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPool</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>正在執行登錄器服務之集區的完整網域名稱 (FQDN)。</p>
<p>請注意，Lync Server 中的 Exchange UM 連絡人不能移至 Microsoft Office Communications Server 2007 或 Microsoft Office Communications Server 2007 R2 部署的集區。</p>
<p>完整資料類型：Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
</tr>
<tr class="even">
<td><p><em>SipAddress</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>連絡人的 SIP 位址。這必須是尚未以使用者或連絡人形式存在 Active Directory 網域服務 中的新位址。此值的開頭必須是 sip: 字串，後面再接著 SIP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><em>AutoAttendant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指定此連絡人物件是否為自動語音應答 (自動語音應答提供一組語音提示，可讓來電者瀏覽電話系統並連絡上預期的通話方)。</p>
<p>預設值：False</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此連絡人的描述。描述可供系統管理員用來識別連絡人的類型 (自動語音應答或使用者存取)、位置、供應商，或可識別每一個 Exchange UM 連絡人目的之其他任何資訊。</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回此命令的結果。執行此 Cmdlet 會顯示新建立的物件；加上此參數只會重複該輸出，導致此參數變得多餘。</p></td>
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

無。

## 傳回類型

建立 Microsoft.Rtc.Management.ADConnect.Schema.OCSADExUmContact 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsExUmContact](remove-csexumcontact.md)  
[Set-CsExUmContact](set-csexumcontact.md)  
[Get-CsExUmContact](get-csexumcontact.md)  
[Move-CsExUmContact](move-csexumcontact.md)  
[Get-CsHostedVoicemailPolicy](get-cshostedvoicemailpolicy.md)

