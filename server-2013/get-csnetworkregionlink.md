---
title: Get-CsNetworkRegionLink
TOCTitle: Get-CsNetworkRegionLink
ms:assetid: dc5cb988-13e2-4af4-8b36-0aaa58ebf1c5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398972(v=OCS.15)
ms:contentKeyID: 49292526
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkRegionLink

 

_**上次修改主題的時間：** 2015-03-09_

擷取通話許可控制 (CAC) 所設定之區域間的一或多個連結。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsNetworkRegionLink [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkRegionLink [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 會擷取定義於 Lync Server 部署中的所有網路區域連結。

    Get-CsNetworkRegionLink

## 範例 2

範例 2 會擷取 (最多) 一個網路區域連結 (與 Identity NA\_EMEA 的連結) 的資訊。

    Get-CsNetworkRegionLink -Identity NA_EMEA

## 範例 3

在此範例中，我們會使用 Filter 參數擷取其連結名稱 (Identity) 中包含字串 EMEA 的所有網路區域連結。請注意，\* 字元一個在字串 EMEA 之前，一個在之後。這表示任何字元皆可以放在字串的前後；字串 EMEA 只是必須內含於 Identity 中的某處即可。這將會擷取含名稱的連結，例如，NA\_EMEA、EMEA\_APAC，與 EMEA2\_SA。

    Get-CsNetworkRegionLink -Filter *EMEA*

## 範例 4

此範例會擷取包含 EMEA 做為連結兩個區域之一的所有網路區域連結。範例會先呼叫不含任何參數的 **Get-CsNetworkRegionLink** Cmdlet，以擷取所有區域連結。然後將此連結集合管線傳送到 **Where-Object** Cmdlet。**Where-Object** Cmdlet 會逐一查看集合的每一個成員，檢查 NetworkRegionID1 與 NetworkRegionID2 屬性的值。如果其中一個屬性等於 EMEA (亦即，若 NetworkRegionID1 等於 (-eq) EMEA 或 (-or) NetworkRegionID2 等於 (-eq) EMEA)，則會將該項目保留於集合中並加以顯示。

    Get-CsNetworkRegionLink | Where-Object {$_.NetworkRegionID1 -eq "EMEA" -or $_.NetworkRegionID2 -eq "EMEA"}

## 詳細描述

網路之中的地區是透過實體 WAN 連線相連結。這個 Cmdlet 會擷取定義於 Lync Server 部署之網路組態設定內的一或多個區域連結。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsNetworkRegionLink** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkRegionLink"}

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
<td><p>根據與萬用字元字串相符的 Identity 值，接受用來擷取網路連結的萬用字元字串。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>您要擷取之網路區域連結的唯一識別碼。網路區域連結只會建立在全域範圍，因此不需要為此識別碼指定範圍。而是用它包含的唯一名稱字串來識別該連結。(請注意，這個值與 NetworkRegionLinkID 相同)。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區本機複本擷取網路區域連結資訊，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

擷取 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType 類型的一或多個物件。

## 請參閱

#### 其他資源

[New-CsNetworkRegionLink](new-csnetworkregionlink.md)  
[Remove-CsNetworkRegionLink](remove-csnetworkregionlink.md)  
[Set-CsNetworkRegionLink](set-csnetworkregionlink.md)

