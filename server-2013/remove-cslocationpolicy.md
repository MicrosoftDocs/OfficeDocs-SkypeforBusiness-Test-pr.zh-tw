---
title: Remove-CsLocationPolicy
TOCTitle: Remove-CsLocationPolicy
ms:assetid: 8fb98533-6474-4071-a74c-ce3f6fa2d326
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398727(v=OCS.15)
ms:contentKeyID: 49291644
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsLocationPolicy

 

_**上次修改主題的時間：** 2015-03-09_

移除指定的位置原則 (增強型 911 服務會使用位置原則讓接聽 119 電話的人員，可以根據電話號碼或撥打電話的裝置判別來電者的地理位置)。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsLocationPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會使用 **Remove-CsLocationPolicy** Cmdlet 刪除 Identity 為 Reno 的位置原則。移除個別使用者原則時，獲指派該原則的使用者或群組將會自動改用針對其網站所設定的原則。如果未針對其網站設定原則，這些使用者及群組將會使用全域位置原則。

    Remove-CsLocationPolicy -Identity Reno

## 範例 2

範例 2 會刪除 EnhancedEmergencyServicesEnabled 屬性為 False 的所有位置原則 (換句話說，它會刪除未啟用 E9-1-1 的所有位置原則)。為達成此目的，命令會先使用 **Get-CsLocationPolicy** Cmdlet 擷取組織目前所使用的所有位置原則。然後，此集合會管線傳送到 **Where-Object** Cmdlet 套用篩選，以將擷取的資料限制在 EnhancedEmergencyServicesEnabled 屬性等於 (-eq) False ($False) 的原則。最後將篩選後的集合傳遞到 **Remove-CsLocationPolicy** Cmdlet，以進行刪除集合中的每個原則。

    Get-CsLocationPolicy | Where-Object {$_.EnhancedEmergencyServicesEnabled -eq $false} | Remove-CsLocationPolicy

## 詳細描述

位置原則用來套用與 E9-1-1 功能相關的設定。位置原則會判斷使用者是否已啟用 E9-1-1，如果是，則會決定緊急電話的行為。例如，您可以使用位置原則來定義組成緊急電話的數字 (在美國為 911)、是否應自動告知公司的安全部門，以及應如何路由傳送來電。此 Cmdlet 會移除現有的位置原則。

除了移除網站和個別使用者位置原則之外，此 Cmdlet 也可以用來移除全域位置原則。但在此情況下，不會真的移除原則；而只是將原則設定重設為預設值。

如果是針對指派給使用者的個別使用者位置原則執行此 Cmdlet，系統會提示您確認刪除。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsLocationPolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsLocationPolicy"}

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
<td><p>您要移除之位置原則的唯一識別碼。若要移除全域位置原則 (只是將該原則重設為其預設值)，請使用 Global 的值。對於在網站範圍建立的原則，此值的格式將為 site:&lt;網站名稱&gt;。其中網站名稱是指在 Lync Server 部署中定義之網站的名稱 (例如 site:Redmond)。針對在個別使用者範圍建立的原則，此值即為原則名稱，例如 Bldg30Floor3Sector1。</p></td>
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
<td><p>指定此參數將會略過所有確認提示，而且會在毫無警告通知的狀況下進行刪除。例如，如果有一個個別使用者位置原則指派給一或多個使用者，當命令中沒有加入此參數時，將會在刪除之前顯示確認提示。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Location.LocationPolicy 物件。接受管線傳送的位置原則物件輸入。

## 傳回類型

此 Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Policy.Location.LocationPolicy 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsLocationPolicy](new-cslocationpolicy.md)  
[Set-CsLocationPolicy](set-cslocationpolicy.md)  
[Get-CsLocationPolicy](get-cslocationpolicy.md)  
[Grant-CsLocationPolicy](grant-cslocationpolicy.md)  
[Test-CsLocationPolicy](test-cslocationpolicy.md)

