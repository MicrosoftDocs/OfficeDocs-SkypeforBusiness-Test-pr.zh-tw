---
title: Set-CsCommonAreaPhone
TOCTitle: Set-CsCommonAreaPhone
ms:assetid: 765ab74c-33ca-4b17-ba15-edb2fe559ebb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398579(v=OCS.15)
ms:contentKeyID: 49291355
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCommonAreaPhone

 

_**上次修改主題的時間：** 2015-03-09_

修改 Lync Server 所管理之公共區域電話的屬性值。公共區域電話是位於大樓大廳、員工休息室，或其他可能由許多不同人使用之區域內的電話，用途可能各異。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsCommonAreaPhone -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-Description <String>] [-DisplayName <String>] [-DisplayNumber <String>] [-DomainController <Fqdn>] [-Enabled <$true | $false>] [-EnterpriseVoiceEnabled <$true | $false>] [-ExchangeArchivingPolicy <Uninitialized | UseLyncArchivingPolicy | NoArchiving | ArchivingToExchange>] [-LineURI <String>] [-PassThru <SwitchParameter>] [-SipAddress <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會修改電話號碼為 1-425-555-6710 之公共區域電話的 Active Directory 顯示名稱。為達成此目的，會先呼叫 **Get-CsCommonAreaPhone** Cmdlet 並搭配 Filter 參數；篩選值 {LineUri -eq "tel:+14255556710"} 會將傳回的資料限制在 LineUri 屬性等於 tel:+14255556710 的公共區域電話。接著將傳回的物件管線傳送到 **Set-CsCommonAreaPhone** Cmdlet，這會將 DisplayName 屬性的值設為 "Employee Lounge"。

    Get-CsCommonAreaPhone -Filter {LineUri -eq "tel:+14255556710"} | Set-CsCommonAreaPhone -DisplayName "Employee Lounge"

## 範例 2

範例 2 所示的命令會啟用所有目前設定供組織使用的公共區域電話。為了執行此工作，命令會呼叫不含任何參數的 **Get-CsCommonAreaPhone** Cmdlet，以傳回所有公共區域電話的集合。然後，此集合會管線傳送到 **Set-CsCommonAreaPhone** Cmdlet，以針對集合中的每個項目，將 Enabled 屬性設為 True。

    Get-CsCommonAreaPhone | Set-CsCommonAreaPhone -Enabled $True

## 範例 3

範例 3 會在所有尚未指派 Description 屬性值的公共區域電話上新增一般描述。為達成此目的，會呼叫 **Get-CsCommonAreaPhone** Cmdlet 並搭配 Filter 參數；{Description -eq $Null} 篩選值可確保只傳回 Description 屬性等於 Null 值的公共區域電話。接著將篩選後的集合管線傳送到 **Set-CsCommonAreaPhone** Cmdlet，以將一般描述 "Common area phone" 指派給集合中的每個項目。

    Get-CsCommonAreaPhone -Filter {Description -eq $Null} | Set-CsCommonAreaPhone -Description "Common area phone"

## 詳細描述

公共區域電話是未與個別使用者相關聯的 IP 電話。公共區域電話不是位於某個人的辦公室中，通常是位於建築物大廳、餐廳、員工休息室、會議室以及其他一群人可能聚集的地點。這對系統管理員而言是一個管理上的挑戰；這是因為在 Lync Server 中使用的電話通常是靠各種語音原則和撥號對應表在維護，而原則和對應表是指派給個別使用者。公共區域電話不會獲指派個別使用者。

解決此難題的方法是，針對所有的公用區電話建立 Active Directory 連絡人物件 (使用 **New-CsCommonAreaPhone** Cmdlet 建立這些連絡人物件)。就像使用者帳戶一樣，可以指派原則和語音對應表給這些連絡人物件。這樣一來，您就能夠對公用區電話保持控制，即使這些電話與個別使用者無關聯。例如，如果不要讓人從公用區電話轉接或保留通話，唯一要做的就是建立禁止通話轉接和保留通話的語音原則，然後將原則指派給公用區電話。(或者，更正確的說法是指派給代表公用區電話的連絡人物件)。這個命令會指派語音原則 CommonAreaPhoneVoicePolicy 給您所有的公用區電話：

Get-CsCommonAreaPhone | Grant-CsVoicePolicy –PolicyName "CommonAreaPhoneVoicePolicy"

**Set-CsCommonAreaPhone** Cmdlet 可以用來修改與公共區域電話關聯的連絡人物件的屬性。總而言之，您可以變更連絡人的 Active Directory 顯示名稱或與此電話關聯的線路統一資源識別元 (URI)。您也可以使用 Enabled 參數啟用和停用用於 Lync Server 的帳戶。

此外，您可以使用 CsClientPolicy Cmdlet 設定公共區域電話的「公用辦公桌」功能。當電話設為公用辦公桌電話時，使用者可以使用其 Lync Server 認證登入電話。這可讓使用者輕鬆存取其連絡人，以及執行其他功能。如需詳細資訊，請參閱 [Set-CsClientPolicy](set-csclientpolicy.md) Cmdlet 說明主題。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsCommonAreaPhone** Cmdlet：RTCUniversalUserAdmins。可以使用 **Grant-CsOUPermission** Cmdlet，為特定網站或特定 Active Directory 組織單位 (OU) 指派執行此 Cmdlet 的權限。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCommonAreaPhone"}

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
<td><p>公共區域電話的唯一識別碼。識別公共區域電話是使用相關聯連絡人物件的 Active Directory 辨別名稱。根據預設，公共區域電話會使用全域唯一識別碼 (GUID) 做為其一般名稱；這表示電話的識別身分通常是像這樣：CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com。因此，您可能會發現使用 <strong>Get-CsCommonAreaPhone</strong> Cmdlet 能夠更輕易地擷取公共區域電話，然後再將傳回的物件管線傳送到 <strong>Set-CsCommonAreaPhone</strong> Cmdlet。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>讓您可以修改公用區電話的 Active Directory 描述屬性。這是一個為電話額外提供資訊的方法；例如，您可以提供資訊說明電話故障時要連絡的人。</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayName</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>讓您可以修改公用區電話的 Active Directory 顯示名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayNumber</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>在 Lync 中顯示的電話號碼。DisplayNumber 屬性可設為任何您偏好的格式，例如 1-800-555-1234、1-(800)-555-1234、1.800.555.1234 等。選擇顯示號碼時，請記住，此號碼只有經過正規化後才會顯示在公共區域電話的顯示畫面上 (正規化是將號碼字串轉譯為標準電話號碼格式的程序)。設定顯示號碼時，如果使用的電話號碼格式沒有正規化規則，則公共區域電話的顯示畫面會顯示 LineUri 屬性的值，而非 DisplayNumber 屬性的值。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Fqdn</p></td>
<td><p>可讓您連線至指定的網域控制站，以修改連絡人資訊。若要連線至特定的網域控制站，請加入 DomainController 參數，後面加上電腦名稱 (例如，atl-mcs-001) 或其完整網域名稱；例如：atl-mcs-001.litwareinc.com。</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>指出是否已啟用 Lync Server 的公共區域電話連絡人物件。</p>
<p>如果使用 Enabled 參數來停用連絡人，則會保留與該帳戶相關聯的資訊 (包括指派的原則以及連絡人是否已啟用 Enterprise Voice、遠端呼叫控制，和/或語音信箱整合)。如果之後使用 Enabled 參數來重新啟用帳戶，將會還原相關聯的帳戶資訊。</p></td>
</tr>
<tr class="even">
<td><p><em>EnterpriseVoiceEnabled</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>指出是否為 Enterprise Voice 啟用公用區電話的連絡人物件，Enterprise Voice 是 Microsoft 提供的 Voice over Internet Protocol (VoIP) 解決方案。透過 Enterprise Voice，便可使用網際網路撥打電話，而非使用標準電話網路。</p></td>
</tr>
<tr class="odd">
<td><p><em>ExchangeArchivingPolicy</em></p></td>
<td><p>選用</p></td>
<td><p>ExchangeArchivingPolicyOptionsEnum</p></td>
<td><p>指出連絡人的立即訊息工作階段封存位置。允許的值為：</p>
<p>* Uninitialized</p>
<p>* UseLyncArchivingPolicy</p>
<p>* ArchivingToExchange</p>
<p>* NoArchiving</p></td>
</tr>
<tr class="even">
<td><p><em>LineURI</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>公用區電話的電話號碼。指定線路統一資源識別元 (URI) 時應該採用 E.164 格式，並在開頭加上 &quot;TEL:&quot;首碼。例如：TEL:+14255551297。任何分機號碼都應該新增至線路 URI 的尾端；例如：TEL:+14255551297; ext=51297。</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>傳回代表一般區域電話的物件。</p></td>
</tr>
<tr class="even">
<td><p><em>SipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>唯一識別碼讓公共區域電話可以和 SIP 裝置通訊，如 Lync。SIP 位址的開頭必須是 sip: 首碼且包含有效的 SIP 網域。例如：sip:bldg14lobby@litwareinc.com。</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact 物件。

## 傳回類型

根據預設，**Set-CsCommonAreaPhone** Cmdlet 不會傳回任何物件或值。但是，如果加入 PassThru 參數，Cmdlet 就會傳回 Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsCommonAreaPhone](get-cscommonareaphone.md)  
[Move-CsCommonAreaPhone](move-cscommonareaphone.md)  
[New-CsCommonAreaPhone](new-cscommonareaphone.md)  
[Remove-CsCommonAreaPhone](remove-cscommonareaphone.md)

