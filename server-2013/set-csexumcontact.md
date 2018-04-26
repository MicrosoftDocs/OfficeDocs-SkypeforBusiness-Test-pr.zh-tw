---
title: Set-CsExUmContact
TOCTitle: Set-CsExUmContact
ms:assetid: c0fe0fdc-6fea-4334-8645-24ffd494db07
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412944(v=OCS.15)
ms:contentKeyID: 49292195
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsExUmContact

 

_**上次修改主題的時間：** 2015-03-09_

修改代管之 Exchange 整合通訊 (UM) 現有的自動語音應答或使用者存取連絡人物件。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsExUmContact -Identity <UserIdParameter> [-AutoAttendant <$true | $false>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-DisplayNumber <String>] [-DomainController <Fqdn>] [-Enabled <$true | $false>] [-EnterpriseVoiceEnabled <$true | $false>] [-ExchangeArchivingPolicy <Uninitialized | UseLyncArchivingPolicy | NoArchiving | ArchivingToExchange>] [-PassThru <SwitchParameter>] [-SipAddress <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會將 SIP 位址為 exumsa4@fabrikam.comis 的 Exchange UM 連絡人的 AutoAttendant 屬性設為 True。我們會先呼叫 **Get-CsExUmContact** Cmdlet 以擷取連絡人物件 (可能也會使用連絡人的 Active Directory 顯示名稱、連絡人的使用者主體名稱或連絡人的登入名稱)。此命令會擷取具有所提供 Identity 的連絡人。然後將該連絡人管線傳送到 **Set-CsExUmContact** Cmdlet，以將 AutoAttendant 參數設為 True。

    Get-CsExUmContact -Identity sip:exumsa4@fabrikam.com | Set-CsExUmContact -AutoAttendant $True

## 範例 2

此範例和範例 1 相同，但在擷取連絡人時，並未呼叫 **Get-CsExUmContact** Cmdlet，也未將該物件管線傳送到 **Set-CsExUmContact** Cmdlet，而是將要修改之連絡人的 Identity 提供給 **Set-CsExUmContact** Cmdlet。請注意 Identity 的格式：此案例使用的是連絡人物件的完整辨別名稱，包括自動產生的 GUID (在建立連絡人時產生)。然後將連絡人的 AutoAttendant 參數設為 True。

    Set-CsExUmContact -Identity "CN={1bf6208d-2847-45d0-828f-636f14da858b},OU=ExUmContacts,DC=litwareinc,DC=com" -AutoAttendant $True

## 詳細描述

Lync Server 搭配 Exchange UM 一起提供多項語音相關功能，包括自動語音應答和使用者存取。以主控服務 (非內部實作) 形式提供 Exchange UM 時，必須使用 Windows PowerShell 建立連絡人物件以套用「自動語音應答」和「使用者存取」功能。這些物件可透過呼叫 **New-CsExUmContact** Cmdlet 來建立，而且以後可以使用 **Set-CsExUmContact** Cmdlet 修改。

通常使用此 Cmdlet 的最簡單方法是先呼叫 **Get-CsExUmContact** Cmdlet，以擷取要修改之連絡人物件的執行個體。只要將 **Get-CsExUmContact** Cmdlet 命令的輸出管線傳送到 **Set-CsExUmContact** Cmdlet，並將值指派給要變更之屬性的參數 (如需詳細資訊，請參閱本主題的＜範例＞一節)。或者，可以呼叫 **Set-CsExUmContact** Cmdlet，將要修改之連絡人物件的 Identity 傳遞給它。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsExUmContact** Cmdlet：RTCUniversalUserAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsExUmContact"}

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
<td><p>UserIdParameter</p></td>
<td><p>您要修改之連絡人物件的唯一識別碼。可以使用下列四種格式的其中一種來指定連絡人識別身分：1) 連絡人的 SIP 位址；2) 連絡人的使用者主體名稱 (UPN)；3) 連絡人的網域名稱和登入名稱，必須是「網域\登入」格式 (例如 litwareinc\exum1)；和 4) 連絡人的 Active Directory 顯示名稱 (例如 Team Auto Attendant)。</p>
<p>完整資料類型：Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
</tr>
<tr class="even">
<td><p><em>AutoAttendant</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>如果連絡人物件是自動語音應答，將參數設定為 True。此參數預設為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>此連絡人的描述。描述可供系統管理員用來識別連絡人的類型 (自動語音應答或使用者存取)、位置、供應商，或可識別每一個 Exchange UM 連絡人目的的其他任何資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayNumber</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>連絡人的電話號碼。每位連絡人的顯示號碼都必須是唯一的 (任兩位 Exchange UM 連絡人不能擁有相同的顯示號碼)。變更這個值也會變更 LineURI 屬性的值。</p>
<p>此值的開頭可以是加號 (+) 且可以包含任何數目的數字。第一個位數不能為零。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Fqdn</p></td>
<td><p>容許您指定網域控制站。若未指定網域控制站，則會使用第一個可用的網域控制站。</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>表示是否已為 Lync Server 啟用連絡人。將此參數設定為 False 會停用連絡人，而且與這個連絡人相關聯的自動語音應答或使用者存取將不再作用。</p>
<p>如果您使用 Enabled 參數停用帳戶，將會保留與該帳戶相關聯的資訊 (包括指定的主控語音信箱原則)。如果稍後使用 Enable 參數重新啟用帳戶，將會還原相關聯的帳戶資訊。</p></td>
</tr>
<tr class="even">
<td><p><em>EnterpriseVoiceEnabled</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>表示是否已為 Enterprise Voice 啟用連絡人。如果這個值設定為 False，將無法再使用與這個連絡人相關聯的自動語音應答或使用者存取功能。</p></td>
</tr>
<tr class="odd">
<td><p><em>ExchangeArchivingPolicy</em></p></td>
<td><p>選用</p></td>
<td><p>ExchangeArchivingPolicyOptionsEnum</p></td>
<td><p>表示連絡人之立即訊息工作階段的封存位置。允許的值為：</p>
<p>* Uninitialized</p>
<p>* UseLyncArchivingPolicy</p>
<p>* ArchivingToExchange</p>
<p>* NoArchiving</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>witchParameter</p></td>
<td><p>傳回命令的結果。根據預設，這個 Cmdlet 不會產生任何輸出。</p></td>
</tr>
<tr class="odd">
<td><p><em>SipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>連絡人的 SIP 位址。這必須是尚未以使用者或連絡人形式存在 Active Directory 網域服務 中的新位址。</p>
<p>變更這個值也會變更儲存在 OtherIpPhone 屬性中的 SIP 位址。</p>
<p>可以使用 SipAddress 做為 Identity 值，讓 <strong>Get-CsExUmContact</strong> Cmdlet 命令能夠擷取特定的連絡人。呼叫該 Cmdlet 時，會使用新的 SipAddress；查詢舊的 SIP 位址不會傳回任何物件。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.ADConnect.Schema.OCSADExUmContact 物件。接受 Exchange UM 連絡人物件管線傳送的輸入。

## 傳回類型

此 Cmdlet 會修改類型為 Microsoft.Rtc.Management.ADConnect.Schema.OCSADExUmContact 的物件。使用 PassThru 參數時，也會傳回此類型的物件。

## 請參閱

#### 其他資源

[New-CsExUmContact](new-csexumcontact.md)  
[Remove-CsExUmContact](remove-csexumcontact.md)  
[Get-CsExUmContact](get-csexumcontact.md)  
[Move-CsExUmContact](move-csexumcontact.md)

