---
title: Set-CsRgsQueue
TOCTitle: Set-CsRgsQueue
ms:assetid: c1656757-c1d9-4e63-947d-99bd331da210
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412947(v=OCS.15)
ms:contentKeyID: 49292202
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsRgsQueue

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的回應群組佇列。回應群組應用程式會將來電會放入佇列加以保留，直到回應群組代理可接聽來電為止。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsRgsQueue -Instance <Queue> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會修改 ApplicationServer:atl-cs-001.litwareinc.com 服務找到的 Help Desk 回應群組佇列的 OverflowCandidate 屬性。為達此目的，範例中的第一個命令會使用 **Get-CsRgsQueue** 從 ApplicationServer:atl-cs-001.litwareinc.com 擷取指定的佇列 (-Name "Help Desk")。擷取的佇列會儲存在名為 $x 的變數中。

在擷取佇列後，範例中的第二個命令會將這個虛擬佇列的 OverflowCandidate 屬性值設為 NewestCall。該命令一旦完成，範例中的最後一個命令就會使用 **Set-CsRgsQueue** 將這些變更寫入真正的 Help Desk 佇列。請注意，到此刻為止，變更只在記憶體中發生，ApplicationServer:atl-cs-001.litwareinc.com 的實際回應群組佇列會一直維持不變，直到您呼叫 **Set-CsRgsQueue** 為止。

    $x = Get-CsRgsQueue -Identity Service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk"
    $x.OverflowCandidate = "NewestCall"
    Set-CsRgsQueue -Instance $x

## 範例 2

範例 2 所示的命令會示範如何建立新的回應群組來電動作，然後將該動作指派給現有的回應群組佇列。為達此目的，第一個步驟是使用 **Get-CsRgsQueue** 從 ApplicationServer:atl-cs-001.litwareinc.com 擷取 Help Desk Overflow Queue 的回應群組佇列，並將該佇列資訊儲存在名為 $x 的變數中。

擷取佇列之後，**New-CsRgsPrompt** Cmdlet 可用來建立新的文字轉語音提示 (儲存在名為 $w 的變數中)。從該處，**New-CsRgsCallAction** Cmdlet 可用來建立新的來電動作。這個來電動作會被指派三個參數：Prompt (來電動作使用的提示)；Action (表示觸發新的來電動作時會進行的動作；TransferToQueue 參數值表示來電會轉接到不同的回應群組佇列)；QueueID 表示會將來電轉接到哪一個替代佇列 ($x.Identity 表示 Help Desk Overflow Queue 佇列的 Identity)。這個新的來電動作會建立在記憶體中，然後儲存在名為 $y 的變數中。

下一個指令會擷取待修改的佇列；在此範例中為 ApplicationServer:atl-cs-001.litwareinc.com 上的 Help Desk 佇列。Get-CsRgsQueue 擷取此佇列後，佇列物件會儲存在名為 $z 的變數中。

一切都完成時，您就可以將新的來電動作指派給 Help Desk 佇列；作法是將 OverflowAction 內容的值設為 $y，這是包含剛建立之來電動作的變數。

在指派來電動作後，範例中的最後一個指令會呼叫 **Set-CsRgsQueue** 將變更寫入 ApplicationServer:atl-cs-001.litwareinc.com 上真正的 Help Desk 佇列執行個體。

    $x = Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk Overflow Queue"
    $w = New-CsRgsPrompt -TextToSpeechPrompt "Please hold while we transfer your call."
    $y = New-CsRgsCallAction -Prompt $w -Action TransferToQueue -QueueID $x.Identity
    $z = Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk"
    $z.OverflowAction = $y
    Set-CsRgsQueue -Instance $z

## 詳細描述

如果某人撥打與回應群組應用程式相關聯的電話號碼，通常會發生下列兩件事的其中之一：來電會被轉接至一個問題，而來電者必須回答才能繼續 (例如，「硬體支援請按 1；軟體支援請按 2」)，或來電會被放置在佇列中，直到代理可接聽來電。

回應群組應用程式可讓您建立與不同工作流程和不同回應群組代理群組相關聯的多個佇列，而不是所有來電者都使用單一佇列。依序表示佇列可分別回應事件，例如，X 通來電被同步保留在佇列中，或來電者已保留 X 秒。

**Set-CsRgsQueue** Cmdlet 提供您修改現有回應群組佇列的方法。**Set-CsRgsQueue** 不允許直接修改佇列，例如 Cmdlet 中沒有參數可變更溢位臨界值或溢位動作。如果您必須修改佇列，則要先使用 **Get-CsRgsQueue** 擷取相關佇列，然後將該佇列儲存在變數中，以建立該佇列的物件參考。接著會將新的值指派給佇列屬性，在記憶體中進行佇列修改。在您完成所有的變更後，接著會呼叫 **Set-CsRgsQueue** 將那些變更寫回到實際的回應群組佇列。如果您沒有呼叫 **Set-CsRgsQueue**，則您所做的變更只會在記憶體中進行，且當您關閉 Windows PowerShell 或刪除物件參考變數時，變更就會消失。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsRgsQueue** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsRgsQueue"}

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
<td><p>要修改之回應群組佇列的物件參考。物件參考通常是使用 <strong>Get-CsRgsQueue</strong> Cmdlet 來擷取，並將傳回的值指派至變數；例如，此命令將物件參考傳回至 Help Desk 佇列，並將該物件參考儲存在名為 $x 的變數中：</p>
<p>$x = Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name &quot;Help Desk&quot;</p></td>
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
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
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

Microsoft.Rtc.Rgs.Management.WritableSettings.Queue 物件。**Set-CsRgsQueue** 接受管線傳送的回應群組佇列物件執行個體。

## 傳回類型

**Set-CsRgsQueue** 不會傳回任何物件或值。而是 Cmdlet 修改現有 Microsoft.Rtc.Rgs.Management.WritableSettings.Queue 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsRgsQueue](get-csrgsqueue.md)  
[New-CsRgsQueue](new-csrgsqueue.md)  
[Remove-CsRgsQueue](remove-csrgsqueue.md)

