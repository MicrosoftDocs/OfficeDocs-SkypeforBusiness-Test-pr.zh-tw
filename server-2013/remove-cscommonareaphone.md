---
title: Remove-CsCommonAreaPhone
TOCTitle: Remove-CsCommonAreaPhone
ms:assetid: f2c93bec-4b99-4b69-abe0-d2d9e33dcadd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413016(v=OCS.15)
ms:contentKeyID: 49292795
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsCommonAreaPhone

 

_**上次修改主題的時間：** 2015-03-09_

將現有的公用區電話從 Lync Server 所管理的電話集合中移除。公共區域電話是位於大樓大廳、員工休息室，或其他可能由許多不同人使用之區域內的電話，用途可能各異。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsCommonAreaPhone -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會刪除顯示名稱為 "Building 14 Lobby" 的公用區電話。為達成此目的，命令會先呼叫 **Get-CsCommonAreaPhone** Cmdlet 搭配 Filter 參數和篩選值 "{DisplayName -eq "Building 14 Lobby"}"。然後再將傳回的物件管線傳送到 **Remove-CsCommonAreaPhone** Cmdlet 加以刪除。

    Get-CsCommonAreaPhone -Filter {DisplayName -eq "Building 14 Lobby"} | Remove-CsCommonAreaPhone

## 範例 2

在範例 2 中，命令會刪除已指派撥號對應表的所有公用區電話。為達此目的，會先使用 **Get-CsCommonAreaPhone** Cmdlet 搭配 Filter 參數傳回指定的項目；篩選值 {DialPlan -eq $Null} 可將傳回的資料限制在未指派撥號對應表的公用區電話。然後將篩選後的集合管線傳送到 **Remove-CsCommonAreaPhone** Cmdlet，以刪除集合中的每個電話。

    Get-CsCommonAreaPhone -Filter {DialPlan -eq $Null} | Remove-CsCommonAreaPhone

## 範例 3

範例 3 會刪除其連絡人物件位於 Active Directory 之 Redmond OU 中的所有公用區電話。為了執行此工作，會先呼叫 **, Get-CsCommonAreaPhone** Cmdlet 傳回 Redmond OU 中具有連絡人物件的所有公用區電話；OU 參數和參數值 "ou=Redmond,dc=litwareinc,dc=com" 可將傳回的資料限制在指定的組織單位。接著將傳回的集合管線傳送到 **Remove-CsCommonAreaPhone** Cmdlet，接著將刪除集合中的每一個電話。

    Get-CsCommonAreaPhone -OU "ou=Redmond,dc=litwareinc,dc=com" | Remove-CsCommonAreaPhone

## 詳細描述

公用區電話是未與個別使用者相關聯的 IP 電話。公用區電話不是位於某個人的辦公室中，通常是位於建築物大廳、餐廳、員工休息室、會議室以及其他一群人可能聚集的地點。這對系統管理員而言是一個管理上的挑戰；這是因為在 Lync Server 中使用的電話通常是靠各種語音原則和撥號對應表在維護，而原則和對應表是指派給個別使用者。公用區電話不會被指派個別使用者。

解決此難題的方法是，針對所有的公用區電話建立 Active Directory 連絡人物件 (使用 **New-CsCommonAreaPhone** Cmdlet 建立這些連絡人物件)。就像使用者帳戶一樣，可以指派原則和語音對應表給這些連絡人物件。這樣一來，您就能夠對公用區電話保持控制，即使這些電話與個別使用者無關聯。例如，如果不要讓人從公用區電話轉接或保留通話，唯一要做的就是建立禁止通話轉接和保留通話的語音原則，然後將原則指派給公用區電話。(或者，更正確的說法是指派給代表公用區電話的連絡人物件)。例如，這個命令會指派語音原則 CommonAreaPhoneVoicePolicy 給您所有的公用區電話：

Get-CsCommonAreaPhone | Grant-CsVoicePolicy –PolicyName "CommonAreaPhoneVoicePolicy"

有時，您可能需要刪除與公用區電話相關聯的連絡人物件。例如，如果您移除了員工休息室的電話，就不再需要與該電話相關聯的連絡人物件。**Remove-CsCommonAreaPhone** Cmdlet 為您提供一個刪除公用區電話的方式。當您執行此 Cmdlet 時，將會從 **Get-CsCommonAreaPhone** Cmdlet 傳回的公用區電話清單中刪除該電話。此外，也會從 Active Directory 網域服務中刪除與該電話相關聯的連絡人物件。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsCommonAreaPhone** Cmdlet：RTCUniversalUserAdmins。可以使用 **Grant-CsOUPermission** Cmdlet，為特定網站或特定 Active Directory 組織單位 (OU) 指派執行此 Cmdlet 的權限。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsCommonAreaPhone"}

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
<td><p>公共區域電話的唯一識別碼。識別公共區域電話是使用相關聯連絡人物件的 Active Directory 辨別名稱。根據預設，公用區電話會使用全域唯一識別碼 (GUID) 做為其一般名稱，這表示這類電話的 Identity 通常會如下所示：CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com。因此，您可能會發現使用 <strong>Get-CsCommonAreaPhone</strong> Cmdlet，然後將傳回的物件傳送到 <strong>Remove-CsCommonAreaPhone</strong> Cmdlet，能夠更輕易地擷取公用區電話。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
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

Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact 物件。**Remove-CsCommonAreaPhone** Cmdlet 會接受管線傳送的公用區電話物件執行個體。

## 傳回類型

**Remove-CsCommonAreaPhone** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsCommonAreaPhone](get-cscommonareaphone.md)  
[Move-CsCommonAreaPhone](move-cscommonareaphone.md)  
[New-CsCommonAreaPhone](new-cscommonareaphone.md)  
[Set-CsCommonAreaPhone](set-cscommonareaphone.md)

