---
title: Remove-CsNetworkSite
TOCTitle: Remove-CsNetworkSite
ms:assetid: 07b543a6-3aa0-4fce-85f9-9ddc75d7b14f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398135(v=OCS.15)
ms:contentKeyID: 49289997
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkSite

 

_**上次修改主題的時間：** 2015-03-09_

移除為通話許可控制 (CAC) 或增強型 9-1-1 (E9-1-1) 所定義的網站。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsNetworkSite -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會從 CAC 或 E9-1-1 組態移除 Identity 為 Vancouver 的網站。

    Remove-CsNetworkSite -Identity Vancouver

## 範例 2

範例 2 會從 CAC 或 E9-1-1 組態移除使用名為 LowBWProfile 之頻寬原則設定檔的所有網站。此範例會先呼叫 **Get-CsNetworkSite** Cmdlet 擷取所有網站。然後再將該網站集合管線傳送到 **Where-Object** Cmdlet，以將集合限縮在 BWPolicyProfileID 等於 (-eq) LowBWProfile 的網站。接著將新集合管線傳送到 **Remove-CsNetworkSite** Cmdlet，以移除這些網站。

    Get-CsNetworkSite | Where-Object {$_.BWPolicyProfileID -eq "LowBWProfile"} | Remove-CsNetworkSite

## 詳細描述

網站是指在 CAC 或 E9-1-1 部署的每一個區域內設定的辦公室或位置。此 Cmdlet 會從 CAC 或 E9-1-1 組態移除網站。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsNetworkSite** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkSite"}

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
<td><p>您要移除之網站的唯一識別碼。網站只可以在全域範圍建立，因此您不需要指定範圍，唯一需要指定的是網站識別碼。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType 物件。接受管線傳送的Select a Site物件輸入。

## 傳回類型

此 Cmdlet 不會傳回值，而會移除 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType 類型的物件。

## 請參閱

#### 其他資源

[New-CsNetworkSite](new-csnetworksite.md)  
[Set-CsNetworkSite](set-csnetworksite.md)  
[Get-CsNetworkSite](get-csnetworksite.md)

