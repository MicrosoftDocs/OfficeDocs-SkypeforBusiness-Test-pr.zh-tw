---
title: Get-CsUserPoolInfo
TOCTitle: Get-CsUserPoolInfo
ms:assetid: 7be81a85-c536-4d5c-b866-af7380e45c0f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398615(v=OCS.15)
ms:contentKeyID: 49291424
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsUserPoolInfo

 

_**上次修改主題的時間：** 2015-03-09_

傳回指派以使用者之登錄器集區、備份登錄器集區及服務集區的資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsUserPoolInfo -Identity <UserIdParameter> [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

此命令會傳回下列單一使用者 (SIP 位址為 sip:kenmyer@litwareinc.com 的使用者) 的使用者集區資訊。

    Get-CsUserPoolInfo "sip:kenmyer@litwareinc.com"

## 範例 2

範例 2 會傳回所有啟用 Lync Server 之使用者的使用者集區資訊。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsUser** Cmdlet，以傳回所有啟用 Lync Server 之使用者的集合。然後，此集合會管線傳送到 **Get-CsUserPoolInfo** Cmdlet，以顯示集合中每位使用者的集區資訊。

    Get-CsUser | Get-CsUserPoolInfo

## 範例 3

範例 3 所示的命令是範例 2 中所使用的命令變化。範例 2 會傳回啟用 Lync Server 之所有使用者的集區資訊。但可能會有使用者已啟用 Lync Server，但未獲指派登錄器集區。範例 2 所示的命令會顯示符合這些準則之每位使用者的錯誤訊息；這些錯誤訊息會在範例 3 中隱藏。

為了隱藏錯誤訊息，範例 3 再次使用 **Get-CsUser** Cmdlet 傳回所有啟用 Lync Server 之使用者的集合。但這次會將集合管線傳送到 **Where-Object** Cmdlet，這會只挑出 RegistrarPool 屬性不等於 Null 值的使用者。(換言之，為已指派登錄器集區的使用者)。接著將篩選後的集合管線傳送到 **Get-CsUserPoolInfo** Cmdlet，以顯示篩選後集合中每位使用者的集區資訊。

    Get-CsUser | Where-Object {$_.RegistrarPool -ne $Null} | Get-CsUserPoolInfo

## 範例 4

在範例 4 中，會顯示獲指派主要集區 redmond-cs-001.litwareinc.com 之所有使用者的集區資訊。為達成此目的，會呼叫 **Get-CsUser** Cmdlet 並搭配 Filter 參數。篩選值 {{RegistrarPool -eq "redmond-cs-001.litwareinc.com"} 只會傳回 RegistrarPool 屬性的完整網域名稱等於 redmond-cs-001.litwareinc.com 的使用者。然後，該集合會傳送到 **Get-CsUserPoolInfo** Cmdlet，以擷取集合中每位使用者的集區資訊。

    Get-CsUser -Filter {RegistrarPool -eq "redmond-cs-001.litwareinc.com"} | Get-CsUserPoolInfo

## 範例 5

範例 5 所示的命令會傳回所有尚未獲指派備份登錄器集區之使用者的集區資訊。為了執行此工作，命令會先呼叫 **Get-CsUser** Cmdlet，以傳回所有啟用 Lync Server 之使用者的集合。然後再將該資訊管線傳送到 **Get-CsUserPoolInfo** Cmdlet，以擷取集合中每位使用者的集區資訊。最後將該集區資訊管線傳送到 **Where-Object** Cmdlet，以只顯示 BackupPoolFqdn 內容等於 Null 值之使用者的資料。

    Get-CsUser | Get-CsUserPoolInfo | Where-Object {$_.BackupPoolFqdn -eq $Null}

## 詳細描述

如果使用者已啟用 Lync Server，則該使用者必須隸屬於登錄器集區。該集區負責驗證使用者，並追蹤使用者目前的狀態與位置。如果您需要知道使用者被指派的登錄集區，您可以使用類似下列的命令來擷取該資訊：

    Get-CsUser "Ken Myer" | Select-Object RegistrarPool

在許多情況下，只知道使用者的登錄集區可能就是您需要的所有資訊。在其他情況下，您可能也想要知道使用者已被指派之備份登錄器集區 (也就是，當主要登錄器集區無法使用時要使用的集區)、組成這些集區之個別電腦的名稱，以及使用者已被指派的 User Services 集區等等。您可以執行 **Get-CsUserPoolInfo** Cmdlet 來傳回該類型的詳細資訊。

Lync Server 2013 已將 Get-CsUserPoolInfo Cmdlet 修改為傳回使用者主要集區與複本集區中之主要前端伺服器的資訊。當集區有多部前端伺服器時，會將每位使用者指派給路由群組，然後再將路由群組指派到主要前端伺服器與複本前端伺服器。根據預設，使用者在登入時即已登錄在主要前端伺服器之中。在 Get-CsUserPoolInfo 輸出中，該伺服器會列為 PrimaryPoolPrimaryRegistrar。當使用者的主要集區容錯移轉時，會將該使用者登錄在備份 (複本) 集區的主要前端伺服器之中。在輸出中，該伺服器會列為 BackupPoolPrimaryRegistrar。

請注意，必須已為使用者的主要集區指派備份集區，才會顯示複本資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權在本機上執行 **Get-CsUserPoolInfo** Cmdlet：RTCUniversalReadOnlyAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsUserPoolInfo"}

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
<td><p>表示要擷取其使用者集區資訊之使用者的 Identity。您可以使用下列四種格式的其中一種來指定 Identity：1) 使用者的 SIP 位址；2) 使用者的使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (例如 litwareinc\kenmyer)；4) 使用者的 Active Directory 網域服務 顯示名稱 (如 Ken Myer)。您也可以利用使用者的 Active Directory 辨別名稱來參考使用者帳戶。</p>
<p>使用「顯示名稱」做為使用者 Identity 時，可以使用星號 (*) 萬用字元。例如，Identity &quot;* Smith&quot; 會傳回姓氏結尾為字串值 &quot; Smith&quot; 之使用者的資訊。</p></td>
</tr>
<tr class="even">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取使用者集區資訊，而非從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

字串或 Microsoft.Rtc.Management.ADConnect.Schema.ADUser 物件。**Get-CsUserPoolInfo** Cmdlet 接受管線傳送的字串值，該值代表已經針對 Lync Server 啟用之使用者帳戶的 SamAccountName。此 Cmdlet 也接受管線傳送的 Active Directory 使用者物件執行個體。

## 傳回類型

**Get-CsUserPoolInfo** Cmdlet 會傳回 Microsoft.Rtc.Management.Xds.GetOCsUserPoolInfoCmdlet+UserInformation 物件的執行個體。

