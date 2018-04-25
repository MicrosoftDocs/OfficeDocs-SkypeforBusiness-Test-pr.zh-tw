---
title: Get-CsDeviceUpdateRule
TOCTitle: Get-CsDeviceUpdateRule
ms:assetid: 14291802-a833-4f5f-8b4b-a465de6f7f2b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398215(v=OCS.15)
ms:contentKeyID: 49290172
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsDeviceUpdateRule

 

_**上次修改主題的時間：** 2015-03-09_

傳回設定供組織使用之裝置更新規則的資訊。裝置更新規則可用於將韌體更新關聯到執行 Lync Server 的裝置。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsDeviceUpdateRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsDeviceUpdateRule [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 詳細描述

Lync Server 利用裝置更新規則為執行 Lync Phone Edition 的裝置提供韌體更新。系統管理員會定期將一組裝置更新規則上傳到 Lync Server；待這些規則通過測試與核准後，會在裝置連線到系統時，自動下載並套用到裝置。根據預設，裝置每次開啟並連線到 Lync Server 時，都會檢查新的更新規則。在最初登入之後，裝置每隔 24 小時也會檢查一次更新。

可匯入 (及套用至) Web 服務服務的裝置更新規則。**Get-CsDeviceUpdateRule** Cmdlet 可讓您傳回已匯入之用於組織的裝置更新規則相關資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsDeviceUpdateRule** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsDeviceUpdateRule"}

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
<td><p>可讓您在指定裝置更新規則或一組規則的 Identity 時使用萬用字元。例如，若要傳回 WebServer:atl-cs-001.litwareinc.com 的所有裝置更新規則，請使用此篩選值：&quot;service:WebServer:atl-cs-001.litwareinc.com*&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>裝置更新規則的唯一識別碼。裝置更新規則 Identity 由兩個部分組成：已套用規則的服務範圍 (例如 service:WebServer:atl-cs-001.litwareinc.com) 和預先指派給規則的全域唯一識別碼 (GUID) (例如 d5ce3c10-2588-420a-82ac-dc2d9b1222ff9)。基於此，所指定裝置更新規則 Identity 如下所示：&quot;service:WebServer:atl-cs-001.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9 &quot;。</p>
<p>指定 Identity 時不允許使用萬元字元。如果您在指定規則時要使用萬用字元，請使用 Filter 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區本機複本擷取裝置更新規則資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsDeviceUpdateRule** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsDeviceUpdateRule** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.DeviceUpdate.Rule 物件的執行個體。

## 範例

## 範例 1

範例 1 中的命令會傳回組織中套用之所有裝置更新規則的資訊。直接呼叫不含任何參數的 **Get-CsDeviceUpdateRule** Cmdlet 一律會傳回裝置更新規則的完整集合。

    Get-CsDeviceUpdateRule

## 範例 2

範例 2 所示的命令會傳回 Identity 為 "WebServer:atl-cs-001.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9" 之裝置更新規則的資訊。

    Get-CsDeviceUpdateRule -Identity service:WebServer:atl-cs-001.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9

## 範例 3

範例 3 會傳回為 WebServer:atl-cs-001.litwareinc.com 服務設定之所有裝置更新規則的資訊。若要執行此作業，請使用 Filter 參數搭配篩選值 "WebServer:atl-cs-001.litwareinc.com \*"。該篩選會將傳回的資料限制為 Identity 開頭字串值是 "service:WebServer:atl-cs-001.litwareinc.com" 的裝置更新規則。

    Get-CsDeviceUpdateRule -Filter service:WebServer:atl-cs-001.litwareinc.com*

## 範例 4

範例 4 會傳回 Brand 屬性等於 "LG-Nortel" 的所有裝置更新規則。為達成此目的，會呼叫 **Get-CsDeviceUpdateRule** Cmdlet 以傳回組織中所有裝置更新規則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 Brand 等於 "LG-Nortel" 的規則。

    Get-CsDeviceUpdateRule | Where-Object {$_.Brand -eq "LG-Nortel"}

## 範例 5

範例 5 會傳回所有尚未核准之裝置更新規則的集合。作法是使用 **Get-CsDeviceUpdateRules** Cmdlet 傳回所有規則的集合，然後，此集合會管線傳送到 **Where-Object** Cmdlet。接著，**Where-Object** Cmdlet 會只選取 Approved 屬性等於 Null 值 的規則。如果 Approved 屬性為 Null，則表示這些規則都未經過核准。

    Get-CsDeviceUpdateRule | Where-Object {$_.ApprovedVersion -eq $Null}

## 範例 6

此命令會傳回所有符合兩個條件的裝置更新規則集合：一是已核准的規則，另一個則是與 LG-Nortel 裝置相關的規則。為達此目的，會先呼叫 **Get-CsDeviceUpdateRule** Cmdlet 傳回組織中所有裝置更新規則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，並根據下列兩項條件篩選集合：Approved 屬性不得為 Null (亦即此屬性必須有某種值)；Brand 則必須等於 "LG-Nortel"。

    Get-CsDeviceUpdateRule | Where-Object {$_.ApprovedVersion -ne $Null -and $_.Brand -eq "LG-Nortel"}

## 請參閱

#### 其他資源

[Approve-CsDeviceUpdateRule](approve-csdeviceupdaterule.md)  
[Remove-CsDeviceUpdateRule](remove-csdeviceupdaterule.md)  
[Reset-CsDeviceUpdateRule](reset-csdeviceupdaterule.md)  
[Restore-CsDeviceUpdateRule](restore-csdeviceupdaterule.md)

