---
title: New-CsNetworkBWPolicy
TOCTitle: New-CsNetworkBWPolicy
ms:assetid: bbc91bd1-453c-4ae6-bb77-3b6be9429ed0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412916(v=OCS.15)
ms:contentKeyID: 49292155
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkBWPolicy

 

_**上次修改主題的時間：** 2015-03-09_

在記憶體中建立可套用至頻寬原則設定檔的頻寬原則。在 Lync Server，原則可套用至音訊或視訊頻寬。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsNetworkBWPolicy -BWLimit <UInt32> -BWPolicyModality <Audio | Video> -BWSessionLimit <UInt32>

## 範例

## 範例 1

此範例會建立新頻寬原則，並指定給變數 $bwp。需要 **New-CsNetworkBWPolicy** Cmdlet 的所有參數。在此範例中，我們指定總頻寬限制 (BWLimit) 為 2000 kbps、頻寬工作階段限制 (BWSessionLimit) 為 300 kbps，且我們將這些限制套用到視訊工作階段 (-BWPolicyModality video)。

    $bwp = New-CsNetworkBWPolicy -BWLimit 200 -BWSessionLimit 3000 -BWPolicyModality video

## 範例 2

範例 2 是範例 1 的延伸，可將新的頻寬原則指派給原則設定檔。第 1 行的命令與範例 1 的命令相同：這會建立視訊頻寬限制。接著第 2 行會呼叫 **New-CsNetworkBandwidthPolicyProfile** Cmdlet，將該原則加入新的設定檔。新的設定檔接收到的 Identity 為 LowBWLimit。然後使用 BWPolicy 參數，給予其 $bwp 值，此為包含我們剛在第 1 行建立的新頻寬原則的變數。

    $bwp = New-CsNetworkBWPolicy -BWLimit 200 -BWSessionLimit 3000 -BWPolicyModality video
    New-CsNetworkBandwidthPolicyProfile -Identity LowBWLimit -BWPolicy $bwp

## 詳細描述

此 Cmdlet 會建立新的頻寬原則。頻寬原則是用於定義特定形式的頻寬限制 (在 Lync Server 中，只會指派音訊與視訊形式的頻寬限制)。頻寬原則只會建立於記憶體中，因此必須將輸出指派給變數，然後將該變數當做值傳遞給 **New-CsNetworkBandwidthPolicyProfile** Cmdlet 或 **Set-CsNetworkBandwidthPolicyProfile** Cmdlet 的 BWPolicy 參數。頻寬原則會套用到原則設定檔，可在單一設定檔中儲存多個原則，且其為通話許可控制 (CAC) 全域網路組態的一部分。

請注意，指派音訊和視訊原則的建議方法是，呼叫 **New-CsNetworkBandwidthPolicyProfile** 或 **Set-CsNetworkBandwidthPolicyProfile** Cmdlet，並為 AudioBWLimit、AudioBWSessionLimit、VideoBWLimit 及 VideoBWSessionLimit 參數指定值，直接將它們指派給頻寬原則設定檔。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsNetworkBWPolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkBWPolicy"}

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
<td><p><em>BWLimit</em></p></td>
<td><p>必要</p></td>
<td><p>System.UInt32</p></td>
<td><p>總頻寬的上限，單位為 kbps，用於所有同時連線且是 BWPolicyModality 參數指定類型的工作階段。</p></td>
</tr>
<tr class="even">
<td><p><em>BWPolicyModality</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyModality</p></td>
<td><p>決定何種類型的頻寬要加以限制。</p>
<p>有效值：Audio、Video</p></td>
</tr>
<tr class="odd">
<td><p><em>BWSessionLimit</em></p></td>
<td><p>必要</p></td>
<td><p>System.UInt32</p></td>
<td><p>BWPolicyModality 參數指定類型的單一工作階段的頻寬的上限，單位為 kbps。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

建立 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyType 類型的物件。

## 請參閱

#### 其他資源

[New-CsNetworkBandwidthPolicyProfile](new-csnetworkbandwidthpolicyprofile.md)  
[Set-CsNetworkBandwidthPolicyProfile](set-csnetworkbandwidthpolicyprofile.md)

