---
title: Set-CsAddressBookConfiguration
TOCTitle: Set-CsAddressBookConfiguration
ms:assetid: a700328b-c738-447a-a03c-319852b42240
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412784(v=OCS.15)
ms:contentKeyID: 49291920
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsAddressBookConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的通訊錄組態設定集合。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsAddressBookConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsAddressBookConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-EnableFileGeneration <$true | $false>] [-EnablePhotoSearch <$true | $false>] [-Force <SwitchParameter>] [-IgnoreGenericRules <$true | $false>] [-KeepDuration <UInt32>] [-MaxDeltaFileSizePercentage <UInt32>] [-MaxFileShareThreadCount <Int32>] [-RunTimeOfDay <DateTime>] [-SynchronizePollingInterval <TimeSpan>] [-UseNormalizationRules <$true | $false>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

RunTimeOfDay 屬性決定「通訊錄」的同步處理在一天中的什麼時候發生，此範例將此屬性設定為 23:00 (11:00 PM 以 24 小時制表示)。使用 Identity 參數，限制變更 Identity 為 site:Redmond 的「通訊錄」組態設定。

    Set-CsAddressBookConfiguration -identity site:Redmond -RunTimeOfDay 23:00

## 範例 2

在範例 2 中，將已在網站範圍設定的所有通訊錄設定集合的 RunTimeOfDay 屬性設為 11:00 PM (23:00)。為達成此目的，命令會先使用 **Get-CsAddressBookConfiguration** Cmdlet 搭配 Filter 參數，以傳回所有網站特定設定的集合；篩選值 "site:\*" 可將傳回的資料限制為在網站範圍所設定的集合。然後再將該資訊管線傳送到 **Set-CsAddressBookConfiguration** Cmdlet，以修改集合中每一個項目的 RunTimeOfDay 屬性值。

    Get-CsAddressBookConfiguration -Filter site:* | Set-CsAddressBookConfiguration -RunTimeOfDay 23:00

## 範例 3

範例 3 會修改任何 KeepDuration 少於 30 天之通訊錄設定集合中的 KeepDuration 屬性。為了執行此工作，命令會使用不含任何參數的 **Get-CsAddressBookConfiguration** Cmdlet，以傳回設定供組織使用之所有通訊錄設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 KeepDuration 屬性少於 30 天的設定。接著將此篩選後的集合管線傳送到 **Set-CsAddressBookConfiguration** Cmdlet，以將集合中每個項目的 KeepDuration 屬性值變更為 30 天。

    Get-CsAddressBookConfiguration | Where-Object {$_.KeepDuration -lt 30} | Set-CsAddressBookConfiguration -KeepDuration 30

## 詳細描述

Address Book Server 是 AD DS 與 Lync Server 之間的中介伺服器。Address Book Server 可確保儲存在 Lync Server 的使用者資訊會與儲存在 AD DS 的使用者資訊同步。其作法是定期將通訊錄檔案與使用者資料庫中儲存的資訊同步化。

此外，Address Book Server 會定期產生索引檔案，這些索引檔案可下載到執行 Lync 的電腦上。當使用者搜尋連絡人時，通常會透過這些索引檔案來搜尋，或搜尋儲存在 中央管理存放區中的通訊錄索引檔案。

Address Book Server 使用通訊錄組態設定進行管理，這些設定可決定通訊錄檔案每隔多久會與使用者資料庫同步，以及每隔多久便會產生這些通訊錄索引檔案等作業。安裝 Lync Server 時，系統會為您建立一組全域的通訊錄設定。您也可以建立能夠套用到個別網站的自訂組態設定。這些設定 (如其存在) 會套用到在網站運作的任何 Address Book Server，而且優先順序高於全域設定。

**Set-CsAddressBookConfiguration** Cmdlet 讓您可以修改您的組織中目前使用的任何「通訊錄」組態設定集合。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsAddressBookConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsAddressBookConfiguration"}

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
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableFileGeneration</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True (預設值) 時，Address Book Server 會產生用戶端可以下載的通訊錄索引檔案。設為 False 時，不會產生這些索引檔案。這表示用戶端應用程式在搜尋連絡人時，必須使用 通訊錄 Web 查詢服務。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePhotoSearch</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若設為 True，搜尋結果中就會顯示使用者相片。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>指派給通訊錄設定集合的唯一識別碼。若要參考全域設定，請使用下列語法：-Identity global。若要參照在此網站範圍設定的集合，請使用如下語法：-Identity site:Redmond。指定 Identity 時，您無法使用萬用字元。</p>
<p>如果省略此參數，則 <strong>Set-CsAddressBookConfiguration</strong> Cmdlet 將修改全域設定。</p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreGenericRules</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>表示 Address Book Server 是否會忽略剖析電話號碼時所使用的一般正規化規則。一般規則就是 Lync Server 內建的規則。這些規則不能變更；但是，藉由將此屬性的值設為 True，即可指示您的 Address Book Server 忽略這些規則，改使用您自己建立的自訂規則。預設值為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>AddressBookSettings 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="even">
<td><p><em>KeepDuration</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>指定 Address Book Server 將保留變更檔案的時間長度 (天數)。早於 KeepDuration 屬性值的變更檔案將被刪除。KeepDuration 可以設為 1 和 90 (含) 之間的任何整數值。預設值是 30 天。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxDeltaFileSizePercentage</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>變更 Active Directory (例如，針對 Lync Server 啟用的新使用者) 時，Address Book Server 通常會在「Delta 檔案」中記錄這些變更，這個檔案僅包含更新的資訊；接著， Lync 可以下載 Delta 檔案，而不是完整的通訊錄檔案。MaxDeltaFileSizePercentage 屬性會決定 Delta 檔案在併入完整的通訊錄檔案之前，可以取得的大小。根據預設，在產生新的通訊錄檔案之前，Delta 檔案的大小可以是完整通訊錄檔案的 20%。到時候 Lync 用戶端將會下載完整檔案而不是 Delta 檔案。</p>
<p>MaxDeltaFileSizePercentage 必須輸入介於 1 和 100 (含) 之間的值來表示百分比。</p></td>
</tr>
<tr class="even">
<td><p><em>MaxFileShareThreadCount</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>指定無法存取服務檔案共用時 Address Book Server 可以使用的系統資源數量上限。預設值為 300。</p></td>
</tr>
<tr class="odd">
<td><p><em>RunTimeOfDay</em></p></td>
<td><p>選用</p></td>
<td><p>System.DateTime</p></td>
<td><p>表示一天中伺服器產生新通訊錄檔案的時間。RunTimeOfDay 屬性使用 24 小時制的時間 (hours:minutes:seconds)，00:00:00 代表午夜，23:59:00 代表 11:59 PM。</p>
<p>預設值是 01:30:00 (1:30 A.M.)。</p></td>
</tr>
<tr class="even">
<td><p><em>SynchronizePollingInterval</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>表示 Address Book Server 將其資訊與 使用者資料庫中儲存之資訊進行同步的頻率。SynchronizePollingInterval 可設為介於 5 秒 (00:00:05) 到 3 小時 (03:00:00) 之間的任何值。預設值為 5 分鐘 (00:05:00)。</p></td>
</tr>
<tr class="odd">
<td><p><em>UseNormalizationRules</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>表示擷取電話號碼時，Address Book Server 是否應該使用電話的正規化規則。如果設為 False，將擷取電話號碼原本的格式，交由用戶端應用程式決定在顯示這些號碼時是否要套用正規化規則。</p>
<p>預設值為 True。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.AddressBook.AddressBookSettings 物件。 **Set-CsAddressBookConfiguration** Cmdlet 接受通訊錄組態物件管線傳送的輸入。

## 傳回類型

**Set-CsAddressBookConfiguration** Cmdlet 不會傳回值或物件，而是會設定 Microsoft.Rtc.Management.WritableConfig.Settings.AddressBook.AddressBookSettings 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsAddressBookConfiguration](get-csaddressbookconfiguration.md)  
[New-CsAddressBookConfiguration](new-csaddressbookconfiguration.md)  
[Remove-CsAddressBookConfiguration](remove-csaddressbookconfiguration.md)

