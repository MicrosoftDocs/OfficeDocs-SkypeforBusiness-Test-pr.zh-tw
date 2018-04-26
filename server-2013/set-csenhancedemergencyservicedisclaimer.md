---
title: Set-CsEnhancedEmergencyServiceDisclaimer
TOCTitle: Set-CsEnhancedEmergencyServiceDisclaimer
ms:assetid: 7c7f5594-4014-4ae0-afe1-6f73340be08c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398620(v=OCS.15)
ms:contentKeyID: 49291431
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsEnhancedEmergencyServiceDisclaimer

 

_**上次修改主題的時間：** 2015-03-09_

設定要在全域使用以針對增強型 9-1-1 (E9-1-1) 實作提示位置資訊的免責聲明文字。Lync Server 2010 中已導入此 Cmdlet。Lync Server 2013 已淘汰此 Cmdlet。若為 Lync Server 2013，應使用 [New-CsLocationPolicy](new-cslocationpolicy.md) Cmdlet 和 [Set-CsLocationPolicy](set-cslocationpolicy.md) Cmdlet 設定 E9-1-1 免責聲明。

## 語法

    Set-CsEnhancedEmergencyServiceDisclaimer [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsEnhancedEmergencyServiceDisclaimer [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Body <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會以傳遞給 Body 參數之字串中提供的文字取代全域增強型緊急服務免責宣告的文字。這個設定只能在全域範圍套用，此為 Identity 的預設值，因此不需要指定。

    Set-CsEnhancedEmergencyServiceDisclaimer -Body "Warning: If you do not provide a location, emergency services may be delayed in reaching your location should you need to call for help."

## 詳細描述

為了讓企業語音實作提供 E9-1-1 服務，位置必須對應到連接埠、子網路、交換器及無線存取點，才能辨別來電者的位置。當來電者從這些對應點之外連線時，必須手動輸入位置供緊急服務接收。對於決定不輸入位置資訊的使用者，此 Cmdlet 會設定對其顯示的文字字串。只有在使用者位置原則的 LocationRequired 屬性設為 Disclaimer 時，此訊息才會顯示 (您可呼叫 **Get-CsLocationPolicy** Cmdlet 擷取位置原則設定)。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsEnhancedEmergencyServiceDisclaimer** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsEnhancedEmergencyServiceDisclaimer"}

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
<td><p><em>Body</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>包含將向從無法由位置對應 (線路圖) 解析的位置連線，且選擇不手動輸入其位置之使用者顯示之資訊的字串。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>這個值必須是 Global。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>EnhancedEmergencyServiceDisclaimer</p></td>
<td><p>增強型緊急服務免責聲明物件的參考。必須屬於 EnhancedEmergencyServiceDisclaimer 類型。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Location.EnhancedEmergencyServiceDisclaimer 物件。接受增強型緊急服務免責聲明物件的管線傳送輸入。

## 傳回類型

此 Cmdlet 不會傳回值或物件，而會修改 Microsoft.Rtc.Management.WritableConfig.Policy.Location.EnhancedEmergencyServiceDisclaimer 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsEnhancedEmergencyServiceDisclaimer](remove-csenhancedemergencyservicedisclaimer.md)  
[Get-CsEnhancedEmergencyServiceDisclaimer](get-csenhancedemergencyservicedisclaimer.md)  
[Get-CsLocationPolicy](get-cslocationpolicy.md)

