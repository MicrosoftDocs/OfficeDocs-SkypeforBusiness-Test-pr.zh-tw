---
title: Get-CsDeviceUpdateConfiguration
TOCTitle: Get-CsDeviceUpdateConfiguration
ms:assetid: e7adc8a7-616a-41b1-8f4b-5f8778e46f55
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399030(v=OCS.15)
ms:contentKeyID: 49292656
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsDeviceUpdateConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織目前所部署之裝置更新組態設定的資訊。這些設定可用於管理 裝置更新 Web 服務，亦即可以讓系統管理員將韌體更新散發到電話與其他執行 Lync Server 之裝置的 Lync Server 元件。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsDeviceUpdateConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsDeviceUpdateConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回組織目前使用之所有裝置更新組態設定的集合。呼叫不含任何其他參數的 **Get-CsDeviceUpdateConfiguration** Cmdlet 會傳回目前使用的所有裝置更新設定。

    Get-CsDeviceUpdateConfiguration 

## 範例 2

範例 2 會傳回全域裝置更新組態設定的資訊。

    Get-CsDeviceUpdateConfiguration -Identity Global

## 範例 3

範例 3 會示範 Filter 參數的使用方法。篩選值 "site:\*" 可傳回在網站範圍套用之所有裝置更新組態設定的集合；這是因為這些設定都包含開頭為字串值 "site:" 開頭的 Identity。

    Get-CsDeviceUpdateConfiguration -Filter site:*

## 範例 4

範例 4 會傳回 MaxLogFileSize 屬性大於 2048000 位元組的所有裝置更新組態設定。為達成此目的，會使用 **Get-CsDeviceUpdateConfiguration** Cmdlet，以傳回目前使用之所有裝置更新組態設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 MaxLogFileSize 屬性大於 2048000 的設定。

    Get-CsDeviceUpdateConfiguration | Where-Object {$_.MaxLogFileSize -gt 2048000}

## 範例 5

範例 5 所示的命令會傳回包含 "Watson" 以做為有效記錄檔類型的所有裝置更新組態設定。為了完成此工作，會使用 **Get-CsDeviceUpdateConfiguration** Cmdlet 以傳回所有裝置更新組態設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出有效記錄檔類型集中包含 "Watson" 的裝置設定。

    Get-CsDeviceUpdateConfiguration | Where-Object {$_.ValidLogFileTypes -like "*Watson*"}

## 詳細描述

裝置更新 Web 服務提供方法讓系統管理員將韌體更新分送到執行 Lync Server 的裝置。系統管理員會定期將一組裝置更新規則上傳到 Lync Server。在測試和核准這些規則之後，便可在適當裝置連線至系統時套用到這些裝置。裝置在最初開啟電源時會檢查更新，然後在使用者登入時再次檢查。之後裝置也會每 24 小時檢查一次更新。

裝置更新 Web 服務是使用裝置組態設定來管理；這些設定會在全域範圍或網站範圍套用。您可使用 **Get-CsDeviceUpdateConfiguration** Cmdlet，以傳回目前使用於您組織中之裝置更新組態設定的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsDeviceUpdateConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Approve-CsDeviceUpdateRule"}

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
<td><p>讓您可以在指定裝置更新組態設定時使用萬用字元。例如，若要傳回已在網站範圍套用之所有組態設定的集合，請使用下列語法：-Filter &quot;site:*&quot;。若要傳回 Identity 中具有術語 &quot;EMEA&quot; 的所有設定，請使用這個語法：-Filter &quot;*EMEA*&quot;。請注意，Filter 參數僅在設定的 Identity 上執行；您無法在其他裝置更新組態屬性上進行篩選。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>表示要擷取之裝置更新組態設定的 Identity。若要參照全域設定，請使用下列語法：-Identity global。若要參照網站設定，請使用類似下列的語法：-Identity site:Redmond。請注意，如有指定 Identity，即無法使用萬用字元。如果您需要使用萬用字元，請改用 Filter 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區本機複本擷取裝置更新組態資料，而不從 中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Get-CsDeviceUpdateConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsDeviceUpdateConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.DeviceUpdateConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsDeviceUpdateConfiguration](new-csdeviceupdateconfiguration.md)  
[Remove-CsDeviceUpdateConfiguration](remove-csdeviceupdateconfiguration.md)  
[Set-CsDeviceUpdateConfiguration](set-csdeviceupdateconfiguration.md)

