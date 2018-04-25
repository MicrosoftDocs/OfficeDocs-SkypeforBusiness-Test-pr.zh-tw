---
title: Remove-CsLisServiceProvider
TOCTitle: Remove-CsLisServiceProvider
ms:assetid: d26302bf-7794-4125-af80-ba7c92096b6d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398904(v=OCS.15)
ms:contentKeyID: 49292396
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsLisServiceProvider

 

_**上次修改主題的時間：** 2015-03-09_

移除由增強型 9-1-1 (E9-1-1) 網路路由提供者所提供用於驗證位置之 Web 服務的資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsLisServiceProvider [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會移除 E9-1-1 實作中的服務提供者 Web 服務。這項實作最多只會定義一個服務提供者，而此 Cmdlet 將會移除該服務提供者。

    Remove-CsLisServiceProvider

## 詳細描述

在啟用 E9-1-1 的 Enterprise Voice 實作中，系統必須先透過 E9-1-1 網路路由提供者來路由傳送緊急通話，以確保將通話路由傳送至合適的公眾安全回應點 (PSAP) (PSAP 是一家位在美國國內的機構，此機構負責將通話引導至最接近的緊急服務，如警察、消防及救護車等服務)。為了完成這項作業，提供者必須先取得組織周圍的位置清單，然後再比對位置清單和主要街道地址指南中的內容，以確保所有位置的有效性。此 Cmdlet 可移除提供者的項目。執行此 Cmdlet 後，您將無法存取提供者的 Web 服務。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsLisServiceProvider** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsLisServiceProvider"}

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
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
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

接受位置資訊伺服器 (LIS) 服務提供者物件管線傳送的輸入。

## 傳回類型

這個 Cmdlet 不會傳回物件或值。它會移除 System.Management.Automation.PSCustomObject 類型的物件。

## 請參閱

#### 其他資源

[Set-CsLisServiceProvider](set-cslisserviceprovider.md)  
[Get-CsLisServiceProvider](get-cslisserviceprovider.md)

