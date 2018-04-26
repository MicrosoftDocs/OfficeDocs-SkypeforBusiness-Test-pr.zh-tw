---
title: Publish-CsLisConfiguration
TOCTitle: Publish-CsLisConfiguration
ms:assetid: 54f9d653-075d-4533-b508-231f53b54db4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398364(v=OCS.15)
ms:contentKeyID: 49290947
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Publish-CsLisConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

將位置資訊伺服器 (LIS) 組態發佈到中央管理存放區。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Publish-CsLisConfiguration [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此命令會認可 中央管理存放區 的 LIS 組態。

    Publish-CsLisConfiguration

## 詳細描述

您必須建立一個位置對應 (稱為線路圖)，才可以在 Lync Server 中實作增強型 9-1-1 (E9-1-1)。此對應包含將實體位址與連接埠、子網路、交換器以及無線存取點進行比對，因此，透過企業語音連線撥打的任何電話都會連接到最近的緊急服務接線生，並將來電者的正確位置提供給該接線生。透過呼叫 **Set-CsLisPort** Cmdlet 和 **Set-CsLisSubnet** Cmdlet 之類的 Cmdlet 而建立的此對應組態會儲存在中央位置資料庫中。此 Cmdlet 會認可在中央位置資料庫中對中央管理存放區所進行的任何變更，讓資訊可以複寫到位置資訊伺服器，如此即可將位置轉譯至用戶端。您可以透過呼叫 **Unpublish-CsLisConfiguration** Cmdlet，從中央管理存放區移除組態。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Publish-CsLisConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Publish-CsLisConfiguration"}

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
<td><p>隱藏變更前所顯示的確認提示。</p></td>
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

這個 Cmdlet 不會傳回值。

## 請參閱

#### 其他資源

[Debug-CsLisConfiguration](debug-cslisconfiguration.md)  
[Unpublish-CsLisConfiguration](unpublish-cslisconfiguration.md)  
[Import-CsLisConfiguration](import-cslisconfiguration.md)  
[Export-CsLisConfiguration](export-cslisconfiguration.md)  
[Test-CsLisConfiguration](test-cslisconfiguration.md)

