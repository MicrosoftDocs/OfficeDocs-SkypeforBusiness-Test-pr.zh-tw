---
title: Remove-CsAddressBookConfiguration
TOCTitle: Remove-CsAddressBookConfiguration
ms:assetid: d634abc2-988a-48f9-ad11-903759516082
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398934(v=OCS.15)
ms:contentKeyID: 49292472
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsAddressBookConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除指定的通訊錄組態設定集合。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsAddressBookConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會使用 **Remove-CsAddressBookConfiguration** Cmdlet，來刪除 Identity 為 site:Redmond 的通訊錄組態設定。使用 Identity 參數可確保系統只會移除指定的通訊錄設定。

    Remove-CsAddressBookConfiguration -Identity site:Redmond

## 範例 2

範例 2 會移除在網站範圍所設定之所有通訊錄設定的集合。為達此目的，會使用 **Get-CsAddressBookConfiguration** Cmdlet 擷取在網站範圍所設定之所有通訊錄設定的集合；作法是使用 Filter 參數搭配篩選值 "site:\*"。然後再將擷取的集合管線傳送到 **Remove-CsAddressBookConfiguration** Cmdlet，以移除集合中的所有項目。

    Get-CsAddressBookConfiguration -Filter site:* | Remove-CsAddressBookConfiguration

## 範例 3

範例 3 會移除所有變更檔案之保留時間少於 30 天的通訊錄設定。為了執行此工作，會使用 **Get-CsAddressBookConfiguration** Cmdlet，以傳回組織目前使用之所有通訊錄設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 KeepDuration 屬性少於 30 天的設定 (請注意，語法中的 30.，在天數之後必須加上句號)。接著將篩選後的集合管線傳送到 **Remove-CsAddressBookConfiguration** Cmdlet，以刪除該集合中的每一個項目。

    Get-CsAddressBookConfiguration | Where-Object {$_.KeepDuration -lt 30.} | Remove-CsAddressBookConfiguration

## 詳細描述

Address Book Server 是 AD DS 與 Lync Server 之間的中介伺服器。Address Book Server 可確保儲存在 Lync Server 的使用者資訊會與儲存在 AD DS 的使用者資訊同步。其作法是定期將通訊錄檔案與使用者資料庫中儲存的資訊同步化。

此外，Address Book Server 會定期產生索引檔案，這些索引檔案可下載到執行 Lync Server 的電腦上。當使用者搜尋連絡人時，通常會透過這些索引檔案來搜尋，或搜尋儲存在中央管理存放區中的通訊錄索引檔案。

Address Book Server 由通訊錄組態設定管理。這些設定可指定通訊錄與使用者資料庫同步的時間間隔，以及產生通訊錄索引檔案的頻率等等。當您在安裝 Lync Server 時，會建立全域的通訊錄設定。您也可以建立自訂的組態設定套用到各個網站。這些設定 (如其存在) 會套用到網站中所執行的 Address Book Server，且其優先順序高於全域設定。

**New-CsAddressBookConfiguration** Cmdlet 可讓您建立網站層級的通訊錄組態設定。若要移除在網站範圍設定的通訊錄設定，請使用 **Remove-CsAddressBookConfiguration** Cmdlet。請注意，您也可以針對全域設定執行 **Remove-CsAddressBookConfiguration** Cmdlet，不過無法真正移除全域設定。反之，針對全域設定執行 **Remove-CsAddressBookConfiguration** Cmdlet 會將所有全域屬性重設為預設值。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsAddressBookConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsAddressBookConfiguration"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要移除之通訊錄組態設定集合的唯一識別碼。若要移除全域集合，請使用下列語法：-Identity global。(當您「移除」全域設定時，只需將所有內容重設回預設值)。若要移除網站集合，請使用類似下列的語法：-Identity site:Redmond。請注意，您在指定原則的 Identity 時，無法使用萬用字元。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.AddressBook.AddressBookSettings 物件。**Remove-CsAddressBookConfiguration** Cmdlet 接受通訊錄組態物件管線傳送的輸入。

## 傳回類型

**Remove-CsAddressBookConfiguration** Cmdlet 不會傳回值或物件，而會移除 Microsoft.Rtc.Management.WritableConfig.Settings.AddressBook.AddressBookSettings 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsAddressBookConfiguration](get-csaddressbookconfiguration.md)  
[New-CsAddressBookConfiguration](new-csaddressbookconfiguration.md)  
[Set-CsAddressBookConfiguration](set-csaddressbookconfiguration.md)

