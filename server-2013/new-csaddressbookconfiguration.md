---
title: New-CsAddressBookConfiguration
TOCTitle: New-CsAddressBookConfiguration
ms:assetid: 5a92a2b0-c46e-44e3-b07c-fc9ff0d33b2b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398395(v=OCS.15)
ms:contentKeyID: 49291020
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsAddressBookConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

建立新的通訊錄組態設定集合。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsAddressBookConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-EnableFileGeneration <$true | $false>] [-EnablePhotoSearch <$true | $false>] [-Force <SwitchParameter>] [-IgnoreGenericRules <$true | $false>] [-InMemory <SwitchParameter>] [-KeepDuration <UInt32>] [-MaxDeltaFileSizePercentage <UInt32>] [-MaxFileShareThreadCount <Int32>] [-RunTimeOfDay <DateTime>] [-SynchronizePollingInterval <TimeSpan>] [-UseNormalizationRules <$true | $false>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會建立 Identity 為 site:Redmond 的新通訊錄組態設定集合。若要建立新集合，您必須呼叫 **New-CsAddressBookConfiguration** Cmdlet，並搭配 Identity 參數和任何其他選用的參數 (例如 KeepDuration 和 SynchronizePollingInterval 參數)。

    New-CsAddressBookConfiguration -Identity site:Redmond -KeepDuration 15 -SynchronizePollingInterval 00:10:00

## 範例 2

範例 2 會針對 Paris 網站建立新的通訊錄設定集合；這個新集合會使用從通訊錄設定 (針對 Redmond 網站所設定) 複製的兩個值 (KeepDuration 和 SynchronizePollingInterval)。為了執行此工作，第一個命令會使用 **Get-CsAddressBookConfiguration** Cmdlet 傳回為 Redmond 網站所設定之所有通訊錄設定的集合；此資訊會儲存在名為 $x 的變數中。

接著，第二個命令會使用 **New-CsAddressBookConfiguration** Cmdlet 建立 Paris 網站的通訊錄設定。這個命令包含兩個選用的參數 (KeepDuration 和 SynchronizePollingInterval)，其中包括從 site:Redmond 複製的值。例如，KeepDuration 會使用參數值 $x.KeepDuration；該參數值代表從 Redmond 網站複製的 KeepDuration 資訊。

    $x = Get-CsAddressBookConfiguration -Identity site:Redmond
    New-CsAddressBookConfiguration -Identity site:Paris -KeepDuration $x.KeepDuration -SynchronizePollingInterval $x.SynchronizePollingInterval

## 範例 3

範例 3 會示範如何使用 InMemory 參數建立通訊錄設定集合的僅記憶體中執行個體、修改記憶體中的這些設定，然後使用 **Set-CsAddressBookConfiguration** Cmdlet 建立 Identity 為 site:Redmond 的實際集合。為達成以上所有目的，第一個命令會建立通訊錄設定組態的新僅記憶體中執行個體，並將該執行個體儲存在名稱為 $x 的變數中。InMemory 參數會確保這些通訊錄設定僅存在於記憶體中；如果您終止 Lync Server 工作階段，或刪除 $x 變數，這些設定將會消失，而不會套用到 Redmond 網站。

命令 2 和 3 會修改這些虛擬通訊錄設定的兩個屬性：命令 2 會將 KeepDuration 屬性的值設為 15 天，而命令 3 會將 SynchronizePollingInterval 設為 10 分鐘 (00:10:00)。接著，第四個和最後一個命令會使用 **Set-CsAddressBookConfiguration** Cmdlet 與 Instance 參數，將虛擬通訊錄設定轉換為在 Redmond 網站設定的實際設定集合。

    $x = New-CsAddressBookConfiguration -Identity site:Redmond -InMemory
    $x.KeepDuration = 15
    $x.SynchronizePollingInterval = "00:10:00"
    Set-CsAddressBookConfiguration -Instance $x

## 詳細描述

Address Book Server 是 AD DS 與 Lync Server 之間的中介伺服器。Address Book Server 可確保儲存在 Lync Server 的使用者資訊會與儲存在 AD DS 的使用者資訊同步。其作法是定期將通訊錄檔案與使用者資料庫中儲存的資訊同步化。

此外，Address Book Server 會定期產生索引檔案，這些索引檔案可下載到執行 Lync 的電腦上。當使用者搜尋連絡人時，通常會透過這些索引檔案來搜尋，或搜尋儲存在 中央管理存放區中的通訊錄索引檔案。

Address Book Server 使用通訊錄組態設定進行管理，這些設定可決定通訊錄檔案每隔多久會與使用者資料庫同步，以及每隔多久便會產生這些通訊錄索引檔案等作業。安裝 Lync Server 時，系統會為您建立一組全域的通訊錄設定。您也可以建立能夠套用到個別網站的自訂組態設定。這些設定 (如其存在) 會套用到在網站運作的任何 Address Book Server，而且優先順序高於全域設定。

網站層級的設定是使用 **New-CsAddressBookConfiguration** Cmdlet 所建立。您只能建立網站範圍的設定；如果嘗試在其他範圍建立新設定 (包括在全域範圍)，則命令會失敗。如果上述網站已經包含通訊錄設定集合，您的命令也會失敗。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsAddressBookConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsAddressBookConfiguration"}

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
<td><p>要指派給新的通訊錄設定集合的唯一識別碼。由於您只能在網站範圍建立新集合，因此，Identity 一律是首碼 &quot;site:&quot;，後面緊接著網站名稱，例如 &quot;site:Redmond&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableFileGeneration</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True (預設值) 時，Address Book Server 會產生用戶端可以下載的通訊錄索引檔案。設為 False 時，不會產生這些索引檔案。這表示用戶端應用程式在搜尋連絡人時，必須使用 通訊錄 Web 查詢服務。</p></td>
</tr>
<tr class="even">
<td><p><em>EnablePhotoSearch</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若設為 True，搜尋結果中就會顯示使用者相片。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreGenericRules</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>表示 Address Book Server 是否會忽略剖析電話號碼時所使用的一般正規化規則。一般規則就是 Lync Server 內建的規則。這些規則不能變更；但是，藉由將此屬性的值設為 True，即可指示您的 Address Book Server 忽略這些規則，改使用您自己建立的自訂規則。預設值為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
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
<p>MaxDeltaFileSizePercentage 必須輸入為百分比值，從 1 到 100 (含)。</p></td>
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

無。**New-CsAddressBookConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

建立 Microsoft.Rtc.Management.WritableConfig.Settings.AddressBook.AddressBookSettings 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsAddressBookConfiguration](get-csaddressbookconfiguration.md)  
[Remove-CsAddressBookConfiguration](remove-csaddressbookconfiguration.md)  
[Set-CsAddressBookConfiguration](set-csaddressbookconfiguration.md)

