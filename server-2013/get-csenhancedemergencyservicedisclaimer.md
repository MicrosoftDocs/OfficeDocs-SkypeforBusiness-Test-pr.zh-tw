---
title: Get-CsEnhancedEmergencyServiceDisclaimer
TOCTitle: Get-CsEnhancedEmergencyServiceDisclaimer
ms:assetid: b5e3a01e-4056-47a0-9c3c-efdf55a08f69
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412877(v=OCS.15)
ms:contentKeyID: 49292073
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsEnhancedEmergencyServiceDisclaimer

 

_**上次修改主題的時間：** 2015-03-09_

擷取用以提示增強型 9-1-1 (E9-1-1) 實作中之位置資訊的全域免責聲明文字。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsEnhancedEmergencyServiceDisclaimer [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsEnhancedEmergencyServiceDisclaimer [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

此命令會擷取增強型緊急服務免責聲明的文字。

    Get-CsEnhancedEmergencyServiceDisclaimer

## 詳細描述

為了讓企業語音實作提供 E9-1-1 服務，必須將位置對應到連接埠、子網路、交換器及無線存取點，才能辨別來電者的位置。若來電者是從這些對應點之外連線，就必須手動輸入其位置，緊急服務才能接收連線。此 Cmdlet 會擷取文字字串，系統將會為決定不輸入其位置資訊的使用者顯示此文字字串。只有當使用者的位置原則的 LocationRequired 屬性設為 Disclaimer 時，才會顯示這個訊息 (您可呼叫 **Get-CsLocationPolicy** Cmdlet 來擷取位置原則設定)。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsEnhancedEmergencyServiceDisclaimer** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsEnhancedEmergencyServiceDisclaimer"}

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
<td><p>此參數可以使用萬用字元搜尋 Identity。但是，因為 Identity 的唯一有效值是 Global，所以此參數對於此 Cmdlet 沒有用。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>這個值必須是 Global。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區本機複本擷取免責聲明資訊，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

傳回 Microsoft.Rtc.Management.WritableConfig.Policy.Location.EnhancedEmergencyServiceDisclaimer 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsEnhancedEmergencyServiceDisclaimer](remove-csenhancedemergencyservicedisclaimer.md)  
[Set-CsEnhancedEmergencyServiceDisclaimer](set-csenhancedemergencyservicedisclaimer.md)  
[Get-CsLocationPolicy](get-cslocationpolicy.md)

