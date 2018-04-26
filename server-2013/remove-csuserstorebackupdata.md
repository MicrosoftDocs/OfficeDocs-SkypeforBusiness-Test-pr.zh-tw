---
title: Remove-CsUserStoreBackupData
TOCTitle: Remove-CsUserStoreBackupData
ms:assetid: 71c8e8ee-61c7-4737-bdac-8cfc80bac126
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205003(v=OCS.15)
ms:contentKeyID: 49291289
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsUserStoreBackupData

 

_**上次修改主題的時間：** 2015-03-09_

從指定的使用者存放區移除逾期的資訊。「逾期的資訊」是登錄器集區中，不再與指定使用者存放區成對的使用者資料。例如，假設集區 A 與 B 先前曾經配對，但之間的關聯後來有所變更，改為集區 A 與 C 配對。此時若對集區 A 執行 Remove-CsUserStoreBackupData Cmdlet，便會移除集區 B 使用者的資訊。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Remove-CsUserStoreBackupData -PoolFqdn <Fqdn> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會移除 atl-cs-001.litwareinc.com 集區及其相關聯的備份集區所儲存的逾期使用者存放區資訊。

    Remove-CsUserStoreBackupData -PoolFqdn "atl-cs-001.litwareinc.com"

## 詳細描述

Lync Server 2013 可讓您關聯配對的集區。當您關聯配對的集區之後，每個集區會維護兩組使用者資訊：一組資訊與要處理之集區上的使用者相關，一組資訊與所關聯之集區上的使用者相關。維護這兩組使用者資訊可讓集區 B 在集區 A 需要容錯移轉時，登錄及服務集區 A 的使用者。

之後您若是變更了這兩個集區間的關聯，該「多出的」使用者資料並不會自動從這兩個集區中刪除。例如，集區 A 會繼續儲存集區 B 的使用者資料 (但此資料不會再更新及複寫)。**Remove-CsUserStoreBackupData** Cmdlet 可讓您從集區 B 刪除集區 A 不再需要的資料。

若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsUserStoreBackupData"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Remove-CsUserStoreBackupData** Cmdlet 所執行的功能。

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
<td><p><em>PoolFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>應移除「逾期」使用者資訊之集區的完整網域名稱。例如：</p>
<p>–PoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的任何非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>描述執行命令後的結果，但無須實際執行命令。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Remove-CsUserStoreBackupData** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。

## 請參閱

#### 其他資源

[Get-CsBackupServiceStatus](get-csbackupservicestatus.md)

