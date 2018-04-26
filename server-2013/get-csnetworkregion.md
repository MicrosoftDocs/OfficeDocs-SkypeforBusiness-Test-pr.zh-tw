---
title: Get-CsNetworkRegion
TOCTitle: Get-CsNetworkRegion
ms:assetid: 5c9eef10-16c1-45f7-ae7b-2bee0965b421
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398406(v=OCS.15)
ms:contentKeyID: 49291044
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkRegion

 

_**上次修改主題的時間：** 2015-03-09_

擷取一或多個網路區域。網路區域代表企業網路中的網路集線器或骨幹。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsNetworkRegion [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkRegion [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 會擷取針對組織定義的所有網路區域。

    Get-CsNetworkRegion

## 範例 2

範例 2 會擷取 Identity 為 NorthAmerica 的網路區域。因為 Identity 是唯一的，因此，此命令最多只會擷取一個網路區域。

    Get-CsNetworkRegion -Identity NorthAmerica

## 範例 3

此範例會擷取 Identity 結尾為字串 "America" 的所有網路區域。這樣會擷取 Identity 為 NorthAmerica、SouthAmerica 以及 CentralAmerica 之類的區域。

    Get-CsNetworkRegion | Where-Object {$_.CentralSite -eq "site:Redmond"}

## 範例 4

此範例會擷取與中央網站 Redmond 相關聯的所有網路區域。命令會先呼叫不含任何參數的 **Get-CsNetworkRegion** Cmdlet，以擷取為 Lync Server 部署定義的所有網路區域集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet。**Where-Object** Cmdlet 會篩選此集合，而只傳回 CentralSite 值等於 (-eq) site:Redmond 的項目 (網路區域)。

    Get-CsNetworkRegion | Where-Object {$_.CentralSite -eq "site:Redmond"}

## 詳細描述

網路區域會與跨多個地理區域的網路不同部分交互連線。每個網路區域都必須與中央網站產生關聯。使用此 Cmdlet 來擷取一個或多個網路區域的資訊 (包括相關聯的中央網站)、擷取判斷是否允許針對音訊和視訊連線使用替代路徑的設定，以及將該區域內的網站與媒體旁路組態產生關聯的設定。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsNetworkRegion** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkRegion"}

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
<td><p>此參數可讓您針對為組織設定之所有網路區域的 Identity 執行萬用字元搜尋。使用萬用字元針對 Identity 的任何部分進行篩選。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>您要擷取之網路區域的唯一識別碼。Identity 的格式會是可唯一識別該區域的字串 (請注意，Identity 與 NetworkRegionID 相同)。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取網路區域資訊，而非從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

傳回 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType 類型的一個或多個物件。

## 請參閱

#### 其他資源

[New-CsNetworkRegion](new-csnetworkregion.md)  
[Remove-CsNetworkRegion](remove-csnetworkregion.md)  
[Set-CsNetworkRegion](set-csnetworkregion.md)

