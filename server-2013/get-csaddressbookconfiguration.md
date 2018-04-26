---
title: Get-CsAddressBookConfiguration
TOCTitle: Get-CsAddressBookConfiguration
ms:assetid: 07757a19-f819-4d65-82da-50bf2f157a9b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398132(v=OCS.15)
ms:contentKeyID: 49289993
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAddressBookConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回通訊錄組態設定的資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsAddressBookConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsAddressBookConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 會傳回有關組織使用中之所有通訊錄組態設定的資訊。若呼叫不含任何參數的 **Get-CsAddressBookConfiguration** Cmdlet，則此為預設行為。

    Get-CsAddressBookConfiguration

## 範例 2

範例 2 會傳回 Identity 為 site:Redmond 的通訊錄組態設定相關資訊。

    Get-CsAddressBookConfiguration -Identity site:Redmond

## 範例 3

在此範例中，使用 Filter 參數與篩選值 "site:\*" 傳回已在網站範圍套用的所有通訊錄組態設定相關資訊。提供的篩選值會傳回 Identity 開頭為 "site:" 字串值的所有通訊錄設定資訊。

    Get-CsAddressBookConfiguration -Filter site:*

## 範例 4

範例 4 會傳回已設定為使用正規化規則剖析電話號碼的所有通訊錄組態設定資訊。為達成此目的，命令會先使用 **Get-CsAddressBookConfiguration** Cmdlet 傳回組織中所有通訊錄設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 UseNormalizationRules 屬性等於 True 的設定。

    Get-CsAddressBookConfiguration | Where-Object {$_.UseNormalizationRules -eq $True}

## 詳細描述

Address Book Server 是 Active Directory 網域服務 與 Lync Server 之間的媒介。Address Book Server 可確保儲存在 Lync Server 的使用者資訊會與儲存在 Active Directory 的使用者資訊同步。其作法是定期將通訊錄檔案與使用者資料庫中儲存的資訊同步化。

此外，Address Book Server 會定期產生索引檔案，這些索引檔案可下載到執行 Lync 的電腦上。當使用者搜尋連絡人時，通常會透過這些索引檔案來搜尋，或搜尋儲存在中央管理存放區中的通訊錄索引檔案。

Address Book Server 使用通訊錄組態設定進行管理，這些設定可決定通訊錄檔案每隔多久會與使用者資料庫同步，以及每隔多久便會產生這些通訊錄索引檔案等作業。當您在安裝 Lync Server 時，系統會為您建立一組全域通訊錄設定。您也可以建立可套用到各個網站的自訂組態設定。這些設定 (如其存在) 會套用到在網站運作的任何 Address Book Server，而且優先順序高於全域設定。

您可以使用 **Get-CsAddressBookConfiguration** Cmdlet 傳回您組織目前所使用之任何 (或所有)通訊錄設定的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsAddressBookConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有已接受此 Cmdlet 指派的角色型存取控制 (RBAC) 角色清單 (包括任何由您自行建立的 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsAddressBookConfiguration"}

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
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您使用萬用字元傳回一或多個通訊錄設定集合。例如，若要傳回在此網站範圍所設定之所有設定集合，請使用下列語法：-Filter site:*。若要傳回在 Identity 中任何位置出現字串值 &quot;EMEA&quot; 的所有設定集合，請使用下列語法：-Filter *EMEA*。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要傳回之通訊錄設定集合的唯一識別碼。若要參照全域設定，請使用下列語法：-Identity global。若要參照在此網站範圍設定的集合，請使用如下語法：-Identity site:Redmond。</p>
<p>請注意，如有指定 Identity，即無法使用萬用字元。如果您必須使用萬用字元，請改為包含 Filter 參數。</p>
<p>若未指定此參數，則 <strong>Get-CsAddressBookConfiguration</strong> Cmdlet 會傳回組織目前所使用之所有通訊錄設定的集合。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區本機複本擷取通訊錄組態資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsAddressBookConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsAddressBookConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.AddressBook.AddressBookSettings 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsAddressBookConfiguration](new-csaddressbookconfiguration.md)  
[Remove-CsAddressBookConfiguration](remove-csaddressbookconfiguration.md)  
[Set-CsAddressBookConfiguration](set-csaddressbookconfiguration.md)

