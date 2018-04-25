---
title: Update-CsAdminRole
TOCTitle: Update-CsAdminRole
ms:assetid: 42cc9cc2-c408-4d0c-814a-6c6367cba834
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204851(v=OCS.15)
ms:contentKeyID: 49290740
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Update-CsAdminRole

 

_**上次修改主題的時間：** 2015-03-09_

更新儲存在中央管理資料庫中的角色型存取控制 (RBAC) 定義，而不影響其他資料庫表格。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Update-CsAdminRole [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會 1 會更新儲存在中央管理資料庫中的 RBAC 定義。

    Update-CsAdminRole

## 詳細描述

**Update-CsAdminRole** Cmdlet 可讓您更新儲存在中央管理資料庫中的 RBAC 角色定義。通常是中央管理資料庫位於 Microsoft Lync Server 2010 集區的共存/移轉案例才需使用此 Cmdlet。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Update-CsAdminRole"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Update-CsAdminRole** Cmdlet 所執行的功能。

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
<td><p>執行命令前先要求您確認。</p></td>
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
<td><p>描述執行命令後的結果，但無須實際執行命令。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Update-CsAdminRole** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。**Update-CsAdminRole** Cmdlet 不會傳回任何資料或物件。

