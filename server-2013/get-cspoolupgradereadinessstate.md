---
title: Get-CsPoolUpgradeReadinessState
TOCTitle: Get-CsPoolUpgradeReadinessState
ms:assetid: 127c718e-8949-4bcd-b954-5182b8730820
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204689(v=OCS.15)
ms:contentKeyID: 49290155
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPoolUpgradeReadinessState

 

_**上次修改主題的時間：** 2015-03-09_

傳回指出 商務用 Skype Online 登錄器集區是否可以升級的資訊。集區的升級整備狀態是以設定供該集區使用的升級網域為主。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsPoolUpgradeReadinessState [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會傳回本機登錄器集區的升級整備狀態。請注意，此命令必須在集區內的前端伺服器上執行。

    Get-CsPoolUpgradeReadinessState

## 詳細描述

The **Get-CsPoolUpgradeReadinessState** Cmdlet 會傳回 Lync Server 2013 集區的升級整備資訊。傳回的資訊包含指派給集區的前端伺服器數量；目前所使用之前端伺服器的數量；升級網域的名稱；以及指出集區目前的狀態是否可以升級的 True/False 值。請注意，此 Cmdlet 必須在進行檢查之集區的前端伺服器上執行。您無法從遠端執行 **Get-CsPoolUpgradeReadinessState** Cmdlet。

**Lync Server 控制台：**Lync Server 控制台不提供 **Get-CsPoolUpgradeReadinessState** Cmdlet 所執行的功能。

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
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
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

無。**Get-CsPoolUpgradeReadinessState** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsPoolUpgradeReadinessState** Cmdlet 會傳回 Microsoft.Rtc.Management.Hadr.PoolUpgradeState 物件的執行個體。

