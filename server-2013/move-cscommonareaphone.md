---
title: Move-CsCommonAreaPhone
TOCTitle: Move-CsCommonAreaPhone
ms:assetid: af5f832c-1be9-4495-ba1a-c10ca50d7b29
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412837(v=OCS.15)
ms:contentKeyID: 49292003
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Move-CsCommonAreaPhone

 

_**上次修改主題的時間：** 2015-04-02_

將一或多個公用區電話移至新的登錄器集區。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Move-CsCommonAreaPhone -Identity <UserIdParameter> -Target <Fqdn> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-IgnoreBackendStoreException <SwitchParameter>] [-PassThru <SwitchParameter>] [-ProxyPool <Fqdn>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將 Identity 為 CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com 的公用區電話移至登錄器集區 atl-cs-001.litwareinc.com。

    Move-CsCommonAreaPhone -Identity "CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com" -Target atl-cs-001.litwareinc.com

## 範例 2

範例 2 會將 Active Directory 顯示名稱為 "Building 31 Cafeteria" 的公用區電話移至登錄器集區 atl-cs-001.litwareinc.com。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsCommonAreaPhone** Cmdlet，以傳回組織目前使用的所有公用區電話集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 DisplayName 屬性等於 "Building 31 Cafeteria" 的電話。接著將該篩選後的集合管線傳送到 **Move-CsCommonAreaPhone** Cmdlet，以將集合中的每個電話移至 atl-cs-001.litwareinc.com。

    Get-CsCommonAreaPhone | Where-Object {$_.DisplayName -eq "Building 31 Cafeteria"} | Move-CsCommonAreaPhone -Target atl-cs-001.litwareinc.com

## 範例 3

範例 3 會將目前隸屬於登錄器集區 dublin-cs-001.litwareinc.com 的所有公用區電話移至登錄器集區 atl-cs-001.litwareinc.com。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsCommonAreaPhone** Cmdlet，以傳回設定供組織使用之所有公用區電話的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會挑出 RegistrarPool 等於 dublin-cs-001.litwareinc.com 的所有公用區電話。接著將此集合管線傳送到 **Move-CsCommonAreaPhone** Cmdlet，以將集合中的每個電話移至新的登錄器集區 atl-cs-001.litwareinc.com。

    Get-CsCommonAreaPhone | Where-Object {$_.RegistrarPool -match "dublin-cs-001.litwareinc.com"} | Move-CsCommonAreaPhone -Target atl-cs-001.litwareinc.com

## 範例 4

範例 4 是範例 3 命令的變化；但在此範例中，不只會將公用區電話移至新的登錄器集區，還會指派新的個別使用者語音原則。為達成此目的，會呼叫 **Move-CsCommonAreaPhone** Cmdlet 搭配PassThru 參數；需要有此參數，才能透過管線傳送公用區電話物件 (根據預設，**Move-CsCommonAreaPhone** Cmdlet 不會透過管線傳送物件)。移動電話之後，會將電話物件管線傳送到 **Grant-CsVoicePolicy** Cmdlet，以將語音原則 AtlantaVoicePolicy 指派給每個新移動的電話。

    Get-CsCommonAreaPhone | Where-Object {$_.RegistrarPool -match "dublin-cs-001.litwareinc.com"} | Move-CsCommonAreaPhone -Target atl-cs-001.litwareinc.com -PassThru | Grant-CsVoicePolicy -PolicyName AtlantaVoicePolicy

## 詳細描述

公用區電話是未與個別使用者相關聯的 IP 電話。公用區電話不是位於某個人的辦公室中，通常是位於建築物大廳、餐廳、員工休息室、會議室以及其他一群人可能聚集的地點。這對系統管理員而言是一個管理上的挑戰；這是因為在 Lync Server 中使用的電話通常是靠各種語音原則和撥號對應表在維護，而原則和對應表是指派給個別使用者。公用區電話不會被指派個別使用者。

解決此難題的方法是，針對所有的公用區電話建立 Active Directory 連絡人物件。(使用 **New-CsCommonAreaPhone** Cmdlet 建立這些連絡人物件)。就像使用者帳戶一樣，可以指派原則和語音對應表給這些連絡人物件。這樣一來，您就能夠對公用區電話保持控制，即使這些電話與個別使用者無關聯。例如，如果不要讓人從公用區電話轉接或保留通話，唯一要做的就是建立禁止通話轉接和保留通話的語音原則，然後將原則指派給公用區電話。(或者，更正確的說法是指派給代表公用區電話的連絡人物件)。

**Move-CsCommonAreaPhone** Cmdlet 讓您能夠將現有的公用區電話移至新的登錄器集區。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Move-CsCommonAreaPhone** Cmdlet：RTCUniversalUserAdmins。可以使用 **Grant-CsOUPermission** Cmdlet，為特定網站或特定 Active Directory 組織單位 (OU) 指派執行此 Cmdlet 的權限。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Move-CsCommonAreaPhone"}

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
<td><p>公用區電話的唯一識別碼。識別公用區電話要使用相關聯連絡人物件的 Active Directory 辨別名稱。根據預設，公用區電話會使用全域唯一識別碼 (GUID) 做為其一般名稱，這表示這類電話的 Identity 通常會如下所示：CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com。</p></td>
</tr>
<tr class="even">
<td><p><em>Target</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>應移動其公用區電話之登錄器集區的完整網域名稱 (FQDN)；例如：atl-cs-001.litwareinc.com。除了登錄器集區外，Target 也可以是主機供應商的 FQDN。</p></td>
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
<td><p>讓您連線至指定的網域控制站，以移動使公用區電話。若要連線至特定的網域控制站，請加入 DomainController 參數，後面加上電腦名稱 (例如，atl-cs-001) 或其 FQDN (例如，atl-cs-001.litwareinc.com)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定，會移動公用區電話，但刪除任何關聯的資料 (例如，已指派給裝置的原則)。若未設定，則會連同任何關聯的資料一起移動電話。</p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreBackendStoreException</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定此參數，會指示電腦忽略後端資料庫可能發生的任何錯誤，並嘗試移動公用區電話而不管這些錯誤。</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>讓您透過管線傳遞使用者物件，代表被移動的使用者帳戶。根據預設，<strong>Move-CsCommonAreaPhone</strong> Cmdlet 不會透過管線傳遞任何物件。</p></td>
</tr>
<tr class="even">
<td><p><em>ProxyPool</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>此參數只能用於 Lync Online。請勿用於 Lync Server 的內部部署實作。</p></td>
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

字串。**Move-CsCommonAreaPhone** Cmdlet 接受代表公用區電話之 Identity 的管線傳送字串值。

## 傳回類型

根據預設，**Move-CsCommonAreaPhone** Cmdlet 不會傳回任何物件或值。但是，如果加入 PassThru 參數，Cmdlet 就會傳回 Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsCommonAreaPhone](get-cscommonareaphone.md)  
[New-CsCommonAreaPhone](new-cscommonareaphone.md)  
[Remove-CsCommonAreaPhone](remove-cscommonareaphone.md)  
[Set-CsCommonAreaPhone](set-cscommonareaphone.md)

