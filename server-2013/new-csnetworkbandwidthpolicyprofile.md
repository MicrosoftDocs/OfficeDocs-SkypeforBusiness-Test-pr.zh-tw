---
title: New-CsNetworkBandwidthPolicyProfile
TOCTitle: New-CsNetworkBandwidthPolicyProfile
ms:assetid: 84940891-37a6-45fc-972d-05b95aa71ba9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398675(v=OCS.15)
ms:contentKeyID: 49291539
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkBandwidthPolicyProfile

 

_**上次修改主題的時間：** 2015-03-09_

建立新的網路頻寬原則設定檔。此 Cmdlet 也可用於設定設定檔內的頻寬原則。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsNetworkBandwidthPolicyProfile -Identity <XdsGlobalRelativeIdentity> [-AudioBWLimit <String>] [-AudioBWSessionLimit <String>] [-BWPolicy <PSListModifier>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-VideoBWLimit <String>] [-VideoBWSessionLimit <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會建立名為 LowBWLimits 的新頻寬原則設定檔。這個新設定檔中將已指派兩個原則，音訊原則和視訊原則 (Lync Server 中唯一可能有的兩個原則)。此音訊原則新增至設定檔時，會使用 AudioBWLimit 參數指派 2000 kbps (這是此範例使用的值) 做為整體音訊連線的限制，並使用 AudioBWSessionLimit 參數指派 200 kbps 做為個別音訊工作階段的限制。建立視訊工作階段限制時也是用相同的方式，但是會使用 VideoBWLimit 和 VideoBWSessionLimit 參數。

    New-CsNetworkBandwidthPolicyProfile -Identity LowBWLimits -AudioBWLimit 2000 -AudioBWSessionLimit 200 -VideoBWLimit 1400 -VideoBWSessionLimit 500

## 詳細描述

頻寬原則為通話許可控制 (CAC) 的一部分，用於定義某些形式的頻寬限制 (在 Lync Server 中，只會指派音訊與視訊形式的頻寬限制)。此 Cmdlet 會建立一個容器設定檔來存放這些原則。您可以在呼叫此 Cmdlet 時指定音訊與視訊頻寬限制，藉以定義容器內的個別原則。

頻寬原則設定檔是藉由呼叫 **New-CsNetworkSite** Cmdlet 或 **Set-CsNetworkSite** Cmdlet 來套用至網路網站。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsNetworkBandwidthPolicyProfile** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkBandwidthPolicyProfile"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>原則的唯一識別字串值。所有的頻寬原則設定檔都是在全域範圍建立。因此，建立新的頻寬原則設定檔時，基於範圍已經暗定的緣故，您只需要指定唯一的名稱。請注意，這個值也會填入到設定檔的 BWPolicyProfileID 屬性。</p></td>
</tr>
<tr class="even">
<td><p><em>AudioBWLimit</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>配置給所有音訊連線的最大頻寬量。如果單一音訊工作階段會導致超出音訊頻寬限制，則不會允許啟動該工作階段。</p>
<p>以 kbps 為單位傳送。例如，數值 1000 表示 1000 kbps。</p>
<p>如果您提供值給此參數，則無法提供值給 BWPolicy 參數。</p>
<p>預設值：如果您將值提供給 AudioBWSessionLimit 參數但未提供給 AudioBWLimit，AudioBWLimit 會使用預設值 0。</p></td>
</tr>
<tr class="odd">
<td><p><em>AudioBWSessionLimit</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>每個音訊工作階段所配置的最大頻寬量。以 kbps 為單位傳送。值必須為 40 或更大。</p>
<p>如果您提供值給此參數，則無法提供值給 BWPolicy 參數。</p>
<p>預設值：如果您將值提供給 AudioBWLimit 參數但未提供給 AudioBWSessionLimit，AudioBWSessionLimit 會使用預設值 175。</p></td>
</tr>
<tr class="even">
<td><p><em>BWPolicy</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>包含頻寬原則設定檔的物件清單。清單中的每一個物件都是由頻寬模式 (音訊或視訊)、頻寬限制和頻寬工作階段限制組成。</p>
<p>如果您提供值給此參數，則無法提供值給 AudioBWLimit、AudioBWSessionLimit、VideoBWLimit 或 VideoBWSessionLimit 參數。</p>
<p>清單中的物件是呼叫 <strong>New-CsNetworkBWPolicy</strong> Cmdlet 來建立的。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>頻寬原則設定檔的描述。例如，您可以使用此參數來闡明期望的設定檔用法。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="odd">
<td><p><em>VideoBWLimit</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>配置給所有視訊連線的最大頻寬量。如果單一視訊工作階段會導致超出視訊頻寬限制，則不會允許啟動該工作階段。</p>
<p>以 kbps 為單位傳送。例如，數值 1000 表示 1000 kbps。</p>
<p>如果您提供值給此參數，則無法提供值給 BWPolicy 參數。</p>
<p>預設值：如果您將值提供給 VideoBWSessionLimit 參數但未提供給 VideoBWLimit，VideoBWLimit 會使用預設值 0。</p></td>
</tr>
<tr class="even">
<td><p><em>VideoBWSessionLimit</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>每個視訊工作階段所配置的最大頻寬量。以 kbps 為單位傳送。值必須為 100 或更大。</p>
<p>如果您提供值給此參數，則無法提供值給 BWPolicy 參數。</p>
<p>預設值：如果您將值提供給 VideoBWLimit 參數但未提供給 VideoBWSessionLimit，VideoBWSessionLimit 會使用預設值 700。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

建立 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsNetworkBandwidthPolicyProfile](remove-csnetworkbandwidthpolicyprofile.md)  
[Set-CsNetworkBandwidthPolicyProfile](set-csnetworkbandwidthpolicyprofile.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkBWPolicy](new-csnetworkbwpolicy.md)

