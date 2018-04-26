---
title: Set-CsNetworkBandwidthPolicyProfile
TOCTitle: Set-CsNetworkBandwidthPolicyProfile
ms:assetid: 519916b9-d5a0-476e-a516-9b8a3058daf2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398338(v=OCS.15)
ms:contentKeyID: 49290908
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkBandwidthPolicyProfile

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的網路頻寬原則設定檔。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsNetworkBandwidthPolicyProfile [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkBandwidthPolicyProfile [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AudioBWLimit <String>] [-AudioBWSessionLimit <String>] [-BWPolicy <PSListModifier>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-VideoBWLimit <String>] [-VideoBWSessionLimit <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會修改 Identity 為 LowBWProfile 之頻寬原則設定檔的描述。其執行方法為呼叫 **Set-CsNetworkBandwidthPolicyProfile** Cmdlet 並搭配兩個參數：Identity 指定要修改之設定檔的名稱；Description 指定設定檔的新描述。

    Set-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile -Description "Policy for links of less than 10MB"

## 範例 2

範例 2 會修改含有 Identity 為 LowBWLimit 之頻寬原則設定檔的整體限制和視訊傳輸的工作階段限制。指定要幽改之設定檔的 Identity 後，接著使用 VideoBWLimit 參數，將整體視訊限制設定為 2500。使用 VideoBWSessionLimit 參數，將個別工作階段限制設定為 300。此命令會為 LowBWLimit 頻寬原則設定檔新增視訊設定檔或更新現有視訊設定檔。不會影響任何現有的音訊設定檔。

    Set-CsNetworkBandwidthPolicyProfile -Identity LowBWLimit -VideoBWLimit 2500 -VideoBWSessionLimit 300

## 範例 3

在此範例中會建立新頻寬原則，並指派給含有 Identity 為 LowBWLimit 的頻寬原則設定檔。此範例的第一行為呼叫 **New-CsNetworkBWPolicy** Cmdlet。此 Cmdlet 會建立新設定檔，在此範例中為具有 5000 kbps (-BWLimit 5000) 限制和 200 kbps (-BWSessionLimit 200) 工作階段限制的視訊設定檔 (-BWPolicyModality video)。此新設定檔物件會儲存在變數 $bp 中。範例中的下一行則呼叫 **Set-CsNetworkBandwidthPolicyProfile** Cmdlet 以修改設定檔 LowBWLimit (-Identity LowBWLimit)。BWPolicy 參數搭配 $bp 的值使用。它以儲存在 $bp 變數中的新建原則，取代此設定檔的任何現有原則。

    $bp = New-CsNetworkBWPolicy -BWLimit 5000 -BWSessionLimit 200 -BWPolicyModality video
    Set-CsNetworkBandwidthPolicyProfile -Identity LowBWLimit -BWPolicy $bp

## 範例 4

範例 4 會新增音訊頻寬原則至設定檔 LowBWProfile 的現有原則集合。在第一行中呼叫 **Get-CsNetworkBandwidthPolicyProfile** Cmdlet 以擷取含有 Identity 為 LowBWProfile 的設定檔。將該設定檔會儲存在變數 $a 中。在下一行中會呼叫 **New-CsNetworkBWPolicy** Cmdlet 以建立新頻寬原則。此原則為含有 2000 kbps (-BWLimit 2000) 限制，以及 300 kbps (-BWSessionLimit 300) 的工作階段限制的音訊原則 (-BWPolicyModality audio)。此新原則會儲存在變數 $ap 中。

第 3 行會將音訊原則 (儲存在 $ap 中) 加入第 1 行所擷取的設定檔 (儲存在變數 $a 中)。作法是呼叫設定檔之 BWPolicy 屬性的 Add 方法傳遞 $ap 的值。這可以解讀為「新增儲存在 $ap 中的新原則至 LowBWProfile 設定檔 (儲存在 $a 中) 的 BWPolicy」。

最後，呼叫 **Set-CsNetworkBandwidthPolicyProfile** Cmdlet 以更新 LowBWProfile 設定檔。我們使用 Instance 參數，傳遞 $a 值，該值包含我們所修改的設定檔。

    $a = Get-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile
    $ap = New-CsNetworkBWPolicy -BWLimit 2000 -BWSessionLimit 300 -BWPolicyModality audio
    $a.BWPolicy.Add($ap)
    Set-CsNetworkBandwidthPolicyProfile -Instance $a

## 範例 5

範例 5 的作用和範例 4 相同：它會新增音訊原則至設定檔 LowBWProfile 的現有原則清單。這個方法需要的行數較少，但可能不太清楚。這裡所包含的只是示範以不同方式執行同樣的事情。

第一行中，我們建立新的音訊頻寬原則，設定頻寬限制 (2000) 和工作階段限制 (300)，然後將新物件儲存在變數 $ap 中。接著呼叫 **Set-CsNetworkBandwidthPolicyProfile** Cmdlet 以修改含有 Identity 為 LowBWProfile 的設定檔。使用 BWPolicy 參數修改設定檔內的原則清單。請注意，我們已經傳遞值給此參數：@{add=$ap}。在 Windows PowerShell 中，這只是新增資料至清單的一種方法。以 @ 符號後面跟隨著一組大括號 {} 開始。在大括號內指定您要在清單上採取的動作，在此範例中為我們要新增至清單 (您也可以移除或取代)。在動作 (add) 後加上等號，再加上要加入清單的物件 (在此範例中是指儲存在變數 $ap 中的新原則)。

    $ap = New-CsNetworkBWPolicy -BWLimit 2000 -BWSessionLimit 300 -BWPolicyModality audio
    Set-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile -BWPolicy @{add=$ap}

## 詳細描述

頻寬原則為通話許可控制 (CAC) 的一部分，用於定義某些形式的頻寬限制(在 Lync Server 中，只會指派音訊與視訊形式的頻寬限制)。此 Cmdelt 會修改這些原則的容器設定檔。

重要事項：如果設定檔包含多個原則 (例如，一個音訊原則和一個視訊原則)，使用 AudioBWLimit、AudioBWSessionLimit、VideoBWLimit 或 VideoBWSessionLimit 等屬性來修改設定檔會移除設定檔中全部的現有原則，並以新值取代。如果設定檔包含限制視訊的原則，並且您只設定 AudioBWLimit 參數，則會移除視訊原則並建立音訊原則。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsNetworkBandwidthPolicyProfile** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkBandwidthPolicyProfile"}

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
<td><p><em>AudioBWLimit</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>配置給所有音訊連線的最大頻寬量。如果單一音訊工作階段會導致超出音訊頻寬限制，則不會允許啟動該工作階段。</p>
<p>以 kbps 為單位傳送。例如，數值 1000 表示 1000 kbps。</p>
<p>如果您提供值給此參數，則無法提供值給 BWPolicy 參數。</p>
<p>預設值：如果您將值提供給 AudioBWSessionLimit 參數但未提供給 AudioBWLimit，AudioBWLimit 會使用預設值 0。</p></td>
</tr>
<tr class="even">
<td><p><em>AudioBWSessionLimit</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>每個音訊工作階段所配置的最大頻寬量。以 kbps 為單位傳送。值必須為 40 或更大。</p>
<p>如果您提供值給此參數，則無法提供值給 BWPolicy 參數。</p>
<p>預設值：如果您將值提供給 AudioBWLimit 參數但未提供給 AudioBWSessionLimit，AudioBWSessionLimit 會使用預設值 175。</p></td>
</tr>
<tr class="odd">
<td><p><em>BWPolicy</em></p></td>
<td><p>選用</p></td>
<td><p>PSListModifier</p></td>
<td><p>包含頻寬原則設定檔的物件清單。清單中的每一個物件都是由頻寬模式 (音訊或視訊)、頻寬限制和頻寬工作階段限制組成。</p>
<p>如果您提供值給此參數，則無法提供值給 AudioBWLimit、AudioBWSessionLimit、VideoBWLimit 或 VideoBWSessionLimit 參數。</p>
<p>清單中的物件類型必須為 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyType。可透過呼叫 <strong>New-CsNetworkBWPolicy</strong> Cmdlet 來建立此類型的物件，並且可將產生的原則指派為此參數的值，新增至設定檔。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>頻寬原則設定檔的描述。例如，您可以使用此參數闡明期望的設定檔用法。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>您要修改之頻寬原則設定檔的唯一識別字串值。它和設定檔的 BWPolicyProfileID 屬性相同，並且可以透過變更該屬性的值來變更。相當於「剪下和貼上」作業：設定檔的所有屬性維持原樣，只有名稱變更。不過，如果設定檔已指派給網站，則無法變更此值。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>BWPolicyProfileType</p></td>
<td><p>包含您用來修改設定檔之設定的頻寬原則設定檔參考 (Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType 類型的物件)。您可以呼叫 <strong>Get-CsNetworkBandwidthPolicyProfile</strong> Cmdlet 來擷取此物件。</p></td>
</tr>
<tr class="odd">
<td><p><em>VideoBWLimit</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>配置給所有視訊連線的最大頻寬量。如果單一視訊工作階段會導致超出視訊頻寬限制，則不會允許啟動該工作階段。</p>
<p>以 kbps 為單位傳送。例如，數值 1000 表示 1000 kbps。</p>
<p>如果您提供值給此參數，則無法提供值給 BWPolicy 參數。</p>
<p>預設值：如果您將值提供給 VideoBWSessionLimit 參數但未提供給 VideoBWLimit，VideoBWLimit 會使用預設值 0。</p></td>
</tr>
<tr class="even">
<td><p><em>VideoBWSessionLimit</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>每個視訊工作階段所配置的最大頻寬量。以 kbps 為單位傳送。值必須為 100 或更大。</p>
<p>如果您提供值給此參數，則無法提供值給 BWPolicy 參數。</p>
<p>預設值：如果您將值提供給 VideoBWLimit 參數但未提供給 VideoBWSessionLimit，VideoBWSessionLimit 會使用預設值 700。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType 物件。接受管線傳送的網路頻寬原則設定檔物件輸入。

## 傳回類型

此 Cmdlet 不會傳回值，而會修改 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType 類型的物件。

## 請參閱

#### 其他資源

[New-CsNetworkBandwidthPolicyProfile](new-csnetworkbandwidthpolicyprofile.md)  
[Remove-CsNetworkBandwidthPolicyProfile](remove-csnetworkbandwidthpolicyprofile.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkBWPolicy](new-csnetworkbwpolicy.md)

