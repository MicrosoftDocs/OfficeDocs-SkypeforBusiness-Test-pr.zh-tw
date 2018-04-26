---
title: Remove-CsEnhancedEmergencyServiceDisclaimer
TOCTitle: Remove-CsEnhancedEmergencyServiceDisclaimer
ms:assetid: 30a5aa8c-04b8-4c1f-92b3-88c86bf69a52
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425810(v=OCS.15)
ms:contentKeyID: 49290496
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsEnhancedEmergencyServiceDisclaimer

 

_**上次修改主題的時間：** 2015-03-09_

移除用以提示增強型 9-1-1 (E9-1-1) 實作中之位置資訊的全域免責聲明文字。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsEnhancedEmergencyServiceDisclaimer -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此命令會移除增強型緊急服務免責聲明的文字。請注意，此命令並不會移除全域免責聲明，該免責聲明仍然存在。它只是將 Body 屬性設為空白字串。

    Remove-CsEnhancedEmergencyServiceDisclaimer -Identity global

## 詳細描述

為了讓 Enterprise Voice 實作提供 E9-1-1 服務，必須將位置對應到連接埠、子網路、交換器及無線存取點，才能辨別來電者的位置。當來電者從這些對應點之外連線，必須手動輸入其位置，緊急服務才能接收連線。此 Cmdlet 會移除向選擇不輸入其位置資訊之使用者顯示的文字字串。只有在使用者位置原則的 LocationRequired 屬性設為 Disclaimer 時，才會顯示此訊息 (您可呼叫 **Get-CsLocationPolicy** Cmdlet 擷取位址原則設定)。在此範例中，呼叫此 Cmdlet 後，會向使用者顯示空白訊息。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsEnhancedEmergencyServiceDisclaimer** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsEnhancedEmergencyServiceDisclaimer"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>這是必要的值，而且必須設為 Global。</p></td>
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

[Set-CsEnhancedEmergencyServiceDisclaimer](set-csenhancedemergencyservicedisclaimer.md)  
[Get-CsEnhancedEmergencyServiceDisclaimer](get-csenhancedemergencyservicedisclaimer.md)  
[Get-CsLocationPolicy](get-cslocationpolicy.md)

