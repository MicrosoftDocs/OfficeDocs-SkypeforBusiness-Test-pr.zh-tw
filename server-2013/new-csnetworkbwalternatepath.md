---
title: New-CsNetworkBWAlternatePath
TOCTitle: New-CsNetworkBWAlternatePath
ms:assetid: 9017378e-4583-42bc-9572-aa8e9571cfe3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398732(v=OCS.15)
ms:contentKeyID: 49291650
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkBWAlternatePath

 

_**上次修改主題的時間：** 2015-03-09_

建立新的設定，以定義當連線受到頻寬限制時，是否可以透過網際網路將媒體路由到替代路徑。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsNetworkBWAlternatePath -AlternatePath <$true | $false> -BWPolicyModality <Audio | Video>

## 範例

## 範例 1

此範例會建立新的網路頻寬替代路徑，並將這些設定指派給新建立的地區。範例中的第一行會呼叫 **New-CsNetworkBWAlternatePath** Cmdlet，以建立新的替代路徑。替代路徑只有兩個屬性：BWPolicyModality (必須設為 audio 或 video，在此範例中為 audio) 和 AlternatePath (必須為 True 或 False，在此範例中為 True)。我們會將此 Cmdlet 的輸出 (新建立之替代路徑物件的參考) 指派給變數 $a。

在此範例中的第 2 行，我們會使用此新建立的替代路徑來建立新的網路地區。為達成此目的，我們會呼叫 **New-CsNetworkRegion** Cmdlet，並傳遞指定為 NorthAmerica 的 Identity。我們會指派必要參數 CentralSite 的值 (在此範例中，此地區的中央網站名稱為 Redmond-NA-MLS)，然後指定 BWAlternatePaths 參數，並將包含剛建立之替代路徑物件的變數 ($a) 傳遞給它。

    $a = New-CsNetworkBWAlternatePath -BWPolicyModality "audio" -AlternatePath $true
    New-CsNetworkRegion -Identity NorthAmerica -CentralSite Redmond-NA-MLS -BWAlternatePaths $a

## 詳細描述

Lync Server 中的通話許可控制 (CAC) 組態內有兩種可能的模式：音訊和視訊。這兩種模式都可以設定頻寬限制。當頻寬限制使得通話無法完成時，可以透過網際網路採取替代路徑，讓通話得以建立。此 Cmdlet 可讓您建立設定，定義是否可以根據模式將通話透過網際網路轉接至替代路徑。這些設定是以 CAC 組態內的個別地區為單位套用。

此 Cmdlet 不會立即儲存新建立的設定，而是將設定建立在記憶體內。若要對網路內的某個地區套用這些設定，您需要將 Cmdlet 的輸出指派給某個變數，然後使用該變數做為 **New-CsNetworkRegion** Cmdlet 或 **Set-CsNetworkRegion** Cmdlet 的 BWAlternatePaths 參數值。請注意，您可以使用 **New-CsNetworkRegion** Cmdlet 和 **Set-CsNetworkRegion** Cmdlet 的 AudioAlternatePath 與 VideoAlternatePath 參數直接套用這些設定，而無須呼叫 **New-CsNetworkBWAlternatePath** Cmdlet 來建立新的物件。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsNetworkBWAlternatePath** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkBWAlternatePath"}

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
<td><p><em>AlternatePath</em></p></td>
<td><p>必要</p></td>
<td><p>Boolean</p></td>
<td><p>將參數設為 True，以在主要路徑無法提供適當的頻寬時，讓以 BWPolicyModality 參數所指定模式的媒體 (音訊或視訊) 建立的通話能夠轉接經替代路徑。</p></td>
</tr>
<tr class="even">
<td><p><em>BWPolicyModality</em></p></td>
<td><p>必要</p></td>
<td><p>BWPolicyModality</p></td>
<td><p>套用替代路徑設定的模式。</p>
<p>有效值：Audio、Video</p>
<p>完整資料類型：Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyModality</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

建立 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWAlternatePathType 類型的物件。

## 請參閱

#### 其他資源

[New-CsNetworkRegion](new-csnetworkregion.md)  
[Set-CsNetworkRegion](set-csnetworkregion.md)

