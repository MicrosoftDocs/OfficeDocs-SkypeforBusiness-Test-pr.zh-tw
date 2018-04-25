---
title: Invoke-CsPoolFailBack
TOCTitle: Invoke-CsPoolFailBack
ms:assetid: 4e58d0b5-4353-4de8-b242-2a4553c3371e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204873(v=OCS.15)
ms:contentKeyID: 49290877
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Invoke-CsPoolFailBack

 

_**上次修改主題的時間：** 2015-03-09_

叫用 Lync Server 2013 集區的容錯回復程序。當集區容錯移轉時，會使用容錯回復將該集區的使用者容錯移轉到備份集區 (亦即登入失敗集區的使用者會自動登入備份集區)。當失敗的集區還原之後，容錯移轉程序會再將使用者容錯移轉回原來的集區。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Invoke-CsPoolFailBack -PoolFqdn <Fqdn> [-Confirm [<SwitchParameter>]] [-DisasterMode <SwitchParameter>] [-Force <SwitchParameter>] [-WaitTime <TimeSpan>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會為 atl-cs-001.litwareinc.com 集區叫用容錯回復程序。

    Invoke-CsPoolFailback -PoolFqdn "atl-cs-001.litwareinc.com"

## 詳細描述

集區容錯移轉程序可讓系統管理員在使用者登入的登錄器集區突然失效時，快速地為使用者還原服務。當集區失敗時，使用者會自動從 Lync Server 2013 登出。若使用者隨即登入，則會重新導向至指定的備份集區。

若要為使用者還原服務，系統管理員可以對目前無法使用的集區執行 **Invoke-CsPoolFailOver** Cmdlet。如此使用者便可登入使用指定備份集區的 Lync Server，且能夠存取所有 Lync Server 服務及功能。請注意，使用者無法再以備份集區做為主集區；他們將只能在主集區還原運作時，登入並使用該集區。例如，當集區 A 失敗時，使用者在集區 A 還原運作之前，只能登入集區 B (包含完整功能)。

當失敗的集區回復運作時，系統管理員接著可以執行 **Invoke-CsPoolFailBack** Cmdlet，將使用者「容錯回復」為該集區。如果目前有使用者登入備份集區，則會在還原服務之後，將該使用者重新導向回其主集區。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Invoke-CsPoolFailback"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Invoke-CsPoolFailback** Cmdlet 所執行的功能。

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
<td><p>進行容錯回復之集區的完整網域名稱。例如：-PoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p>
<p>容錯回復期間與容錯移轉期間所使用的集區 FQDN 必須相同。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>DisasterMode</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>可讓系統管理員叫用集區容錯回復功能，即使目前無法使用備份集區亦然。使用此參數時，備份集區上的容錯移轉使用者所產生的資料都會遺失。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>WaitTime</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>指定 Cmdlet 最多等待多久之後，要同步處理資料。時間值必須以時:分:秒的格式表示；例如，下列語法將等待時間設為 1 分鐘 30 秒 (00 時:01 分:30 秒)：</p>
<p>00:01:30</p>
<p>預設值為 15 秒。</p></td>
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

無。**Invoke-CsPoolFailBack** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。

## 請參閱

#### 其他資源

[Invoke-CsPoolFailOver](invoke-cspoolfailover.md)

