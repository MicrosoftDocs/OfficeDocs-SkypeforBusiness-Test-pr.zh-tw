---
title: Remove-CsRgsQueue
TOCTitle: Remove-CsRgsQueue
ms:assetid: 7613e72c-f330-4560-88d4-a7386cd18975
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398576(v=OCS.15)
ms:contentKeyID: 49291343
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsRgsQueue

 

_**上次修改主題的時間：** 2015-03-09_

刪除現有的回應群組佇列。回應群組應用程式會將來電放入佇列加以保留，直到回應群組代理可接聽來電為止。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsRgsQueue -Instance <Queue> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會刪除在 ApplicationServer:atl-cs-001.litwareinc.com 服務上找到的所有回應群組佇列。為達此目的，命令會先使用 **Get-CsRgsQueue** 傳回在 ApplicationServer:atl-cs-001.litwareinc.com 上找到之所有佇列的集合。然後再將該集合管線傳送到 **Remove-CsRgsQueue**，以刪除集合中的每一個佇列。

    Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com | Remove-CsRgsQueue

## 範例 2

在範例 2 中，單一回應群組佇列會被刪除：位於 ApplicationServer:atl-cs-001.litwareinc.com 服務上，名為 "Help Desk Queue" 的佇列。若要刪除此佇列，會呼叫 **Get-CsRgsQueue** 並搭配 Identity 及 Name 參數；由此呼叫傳回的單一佇列會被傳送到 **Remove-CsRgsQueue**，並予以刪除。

    Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk Queue" | Remove-CsRgsQueue

## 範例 3

範例 3 會刪除在 ApplicationServer:atl-cs-001.litwareinc.com 服務上找到的所有回應群組佇列 (如果這些佇列的 OverflowCandidate 屬性設定為 NewestCall)。為達此目的，會先呼叫 **Get-CsRgsQueue** 傳回在 ApplicationServer:atl-cs-001.litwareinc.com 上找到的所有回應群組佇列集合。然後再該集合管線傳送到 **Where-Object** Cmdlet，以選取 OverflowCandidate 屬性等於 "NewestCall" 的佇列。接著將篩選後的集合管線傳送到 **Remove-CsRgsQueue**，以刪除集合中的每一個佇列。

    Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com | Where-Object {$_.OverflowCandidate -eq "NewestCall"} | Remove-CsRgsQueue

## 詳細描述

如果某人撥打與 回應群組應用程式 相關聯的電話號碼，通常會發生下列兩件事的其中之一：來電會被轉接至一個問題，而來電者必須回答才能繼續 (例如，「硬體支援請按 1；軟體支援請按 2」)，或來電會被放置在佇列中，直到回應群組代理可接聽來電。

回應群組應用程式 可讓您建立與不同工作流程和不同回應群組代理群組相關聯的多個佇列，而不是所有來電者都使用單一佇列。這表示佇列可以分別回應事件，例如佇列會同時保留指定數目的來電，或回應已保留了指定時間的來電者。

除了建立新佇列，您也可以移除現有佇列；這就是 **Remove-CsRgsQueue** Cmdlet 的功能。請注意，根據預設，如果您嘗試移除目前指派給作用中工作流程的佇列，系統會出現提示；該提示會要求您確認是否要刪除佇列，在回答提示之前，Windows PowerShell 會暫停 (且沒有佇列會被刪除)。若要略過提示，並刪除正由作用中工作流程使用的佇列，請新增 Force 參數。例如：

Get-CsRgsQueue –Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" | Remove-CsRgsQueue –Force

**Remove-CsRgsQueue** 在刪除佇列之前，一律會檢查使用中工作流程是否正在使用該佇列。不過，此 Cmdlet 不會驗證該佇列是否由另一個佇列用作逾時或溢位佇列。這表示可能會刪除另一個佇列所需的佇列。因此，在執行 **Remove-CsRgsQueue** 以刪除佇列之前，您可能想要使用 **Get-CsRgsQueue** Cmdlet 來檢查其他回應群組佇列的 OverflowAction 和 TimeoutAction 內容。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsRgsQueue** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsRgsQueue"}

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
<td><p><em>Instance</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.Queue</p></td>
<td><p>指向要移除之佇列的物件參考。將工作流程物件傳送到 <strong>Remove-CsRgsQueue</strong> 時，您可以省略 Instance 參數。</p>
<p>若要使用 Instance 參數，請使用類似下列的命令：</p>
<p>$x = Get-CsRgsQueue –Identity ApplicationServer:atl-cs-001.litwareinc.com /1987d3c2-4544-489d-bbe3-59f79f530a83</p>
<p>Remove-CsRgsQueue –Instance $x</p>
<p>請注意，使用 Instance 參數時，您一次只能移除一個佇列。這表示物件參考 ($x) 不能包含多個佇列物件。</p></td>
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
<td><p>強制刪除回應群組佇列。如有設定此參數，即使已將佇列指派給作用中的工作流程，仍會將佇列刪除而不發出任何警告。若未設定此參數，將會要求您確認是否要刪除作用中工作流程目前所使用的佇列。</p></td>
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

Microsoft.Rtc.Rgs.Management.WritableSettings.Queue 物件。**Remove-CsRgsQueue** 接受管線傳送的回應群組佇列物件執行個體。

## 傳回類型

**Remove-CsRgsQueue** 會刪除現有的 Microsoft.Rtc.Rgs.Management.WritableSettings.Queue 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsRgsQueue](get-csrgsqueue.md)  
[New-CsRgsQueue](new-csrgsqueue.md)  
[Set-CsRgsQueue](set-csrgsqueue.md)

