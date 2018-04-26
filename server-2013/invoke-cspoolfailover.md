---
title: Invoke-CsPoolFailOver
TOCTitle: Invoke-CsPoolFailOver
ms:assetid: b5c30438-0553-41f4-b856-68c1ec0deff7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205189(v=OCS.15)
ms:contentKeyID: 49292077
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Invoke-CsPoolFailOver

 

_**上次修改主題的時間：** 2015-03-09_

叫用 Lync Server 2013 集區的容錯移轉程序。容錯移轉是集區失敗時，該集區目前的使用者登入備份集區的程序。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Invoke-CsPoolFailOver -PoolFqdn <Fqdn> [-Confirm [<SwitchParameter>]] [-DisasterMode <SwitchParameter>] [-FlushStorageService <SwitchParameter>] [-Force <SwitchParameter>] [-WaitTime <TimeSpan>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會呼叫集區 atl-cs-001.litwareinc.com 的集區容錯移轉。

    Invoke-CsPoolFailOver -PoolFqdn "atl-cs-001.litwareinc.com"

## 範例 2

範例 2 會呼叫集區 atl-cs-001.litwareinc.com 的災害模式容錯移轉。

    Invoke-CsPoolFailOver -PoolFqdn "atl-cs-001.litwareinc.com" -DisasterMode

## 詳細描述

集區容錯移轉程序可讓系統管理員在使用者登入的登錄器集區突然失效時，快速地為使用者還原服務。當集區失敗時，使用者會自動從 Lync Server 2013 登出。若使用者隨即登入，則會重新導向至指定的備份集區。

若要為使用者還原服務，系統管理員可以對目前無法使用的集區執行 **Invoke-CsPoolFailOver** Cmdlet。如此使用者便可登入使用指定備份集區的 Lync Server，且能夠存取所有 Lync Server 服務及功能。請注意，使用者無法再以備份集區做為主集區；他們將只能在主集區還原運作時，登入並使用該集區。例如，當集區 A 失敗時，使用者在集區 A 還原運作之前，只能登入集區 B (包含完整功能)。

當失敗的集區回復運作時，系統管理員接著可以執行 **Invoke-CsPoolFailBack** Cmdlet，將使用者「容錯回復」為該集區。如果目前有使用者登入備份集區，則會在還原服務之後，將該使用者重新導向回其主集區。

必須要先指定失敗集區的備份集區，才可叫用集區容錯移轉。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Invoke-CsPoolFailover"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Invoke-CsPoolFailOver** Cmdlet 所執行的功能。

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
<td><p>正在容錯移轉自之集區的完整網域名稱。例如：</p>
<p>-PoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p></td>
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
<td><p>如有指定此參數，表示正以「災害模式」執行容錯移轉。如果再也無法存取集區，那麼為使用者還原該集區完整功能的唯一方法，就是使用 DisasterMode 參數來容錯移轉集區。</p>
<p>若未指定此參數，表示集區仍啟動且正在執行，但是系統管理員選擇執行容錯移轉；例如，可能會暫時容錯移轉集區，以便在伺服器上執行硬體或軟體升級。</p></td>
</tr>
<tr class="even">
<td><p><em>FlushStorageService</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定， <strong>Invoke-CsPoolFailOver</strong> Cmdlet 會容錯移轉集區中的所有使用者，同時呼叫 <a href="invoke-csstorageserviceflush.md">Invoke-CsStorageServiceFlush</a> Cmdlet，以排清集區中每一部前端伺服器上的存放區服務資料庫。排清資料庫必須先將所有佇列中的資料寫入磁碟，然後清除資料庫快取。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>WaitTime</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>指定此 Cmdlet 等候的時間 (秒)，在這之後，假設資料已從容錯移轉集區同步處理至備份集區。</p></td>
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

無。**Invoke-CsPoolFailOver** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。

## 請參閱

#### 其他資源

[Invoke-CsPoolFailBack](invoke-cspoolfailback.md)

