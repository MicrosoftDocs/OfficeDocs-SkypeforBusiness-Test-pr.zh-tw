---
title: New-CsRgsQueue
TOCTitle: New-CsRgsQueue
ms:assetid: e013533b-6845-44c6-ae5e-e75187b43181
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398989(v=OCS.15)
ms:contentKeyID: 49292560
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsRgsQueue

 

_**上次修改主題的時間：** 2015-03-09_

建立新的回應群組佇列。回應群組應用程式會將來電會放入佇列加以保留，直到回應群組代理可接聽來電為止。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsRgsQueue -Name <String> -Parent <RgsIdentity> [-AgentGroupIDList <Collection>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-OverflowAction <CallAction>] [-OverflowCandidate <NewestCall | OldestCall>] [-OverflowThreshold <Int16>] [-TimeoutAction <CallAction>] [-TimeoutThreshold <Int32>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會為 ApplicationServer:atl-cs-001.litwareinc.com 服務建立新的回應群組佇列。範例中的第一個命令使用 **New-CsRgsCallAction** Cmdlet 建立佇列的來電動作；在此範例中，只要超過溢位臨界值，來電就會自動轉接到語音信箱。這是透過將 Action 參數設為 TransferToVoicemailUri，並將 URI 內容設為語音信箱 SIP URI "sip:+14255551298@litwareinc.com" 來設定。

設定來電動作之後 (並儲存在變數 $x)，**New-CsRgsQueue** 便用來建立名為 Help Desk 的新佇列。除了指定 OverflowAction，此命令也設定 OverflowCandidate 和 OverflowThreshold 內容的值。

    $x = New-CsRgsCallAction -Action TransferToVoicemailUri -Uri "sip:+14255551298@litwareinc.com"
    
    New-CsRgsQueue -Parent service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk" -OverflowCandidate "OldestCall" -OverflowAction $x -OverflowThreshold 25

## 詳細描述

如果某人撥打與 回應群組應用程式 相關聯的電話號碼，通常會發生下列兩件事的其中之一：來電會被轉接至一個問題，而來電者必須回答才能繼續 (例如，「硬體支援請按 1；軟體支援請按 2」)，或來電會被放置在佇列中，直到代理可接聽來電。

回應群組應用程式 可讓您建立與不同工作流程和不同回應群組代理群組相關聯的多個佇列，而不是所有來電者都使用單一佇列。這表示佇列可以分別回應事件，例如佇列會同時保留指定數目的來電，或回應已保留了指定時間的來電者。

**New-CsRgsQueue** Cmdlet 可讓系統管理員輕鬆建立新的回應群組佇列。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsRgsQueue** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsRgsQueue"}

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
<td><p><em>Name</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>指派給佇列的唯一名稱。Parent 屬性和 Name 屬性的組合可讓您唯一識別營業回應群組佇列，而不必參考佇列的全域唯一識別碼 (GUID)。</p></td>
</tr>
<tr class="even">
<td><p><em>Parent</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>主控新佇列的服務。例如：-Parent &quot;service:ApplicationServer:atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>AgentGroupIDList</em></p></td>
<td><p>選用</p></td>
<td><p>System.Collections.ObjectModel.Collection</p></td>
<td><p>要新增到佇列的回應群組代理群組的 Identity。使用 <strong>Get-CsRgsAgentGroup</strong> Cmdlet 可以擷取代理群組的 Identity。如需詳細資訊，請參閱本主題中的＜範例＞區段。</p>
<p>如果來電轉送到未指派代理群組的佇列 (或僅指派沒有任何代理的代理群組)，則會自動切斷來電。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>讓系統管理員能夠提供有關回應群組佇列的其他資訊。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="even">
<td><p><em>OverflowAction</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.CallAction</p></td>
<td><p>如果到達溢位臨界值時採取的動作。OverflowAction 必須使用 <strong>New-CsRgsCallAction</strong> Cmdlet 建立。</p></td>
</tr>
<tr class="odd">
<td><p><em>OverflowCandidate</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.OverflowCandidate</p></td>
<td><p>指出如果已達溢位臨界值時應對來電採取的動作。OverflowCandidate 屬性必須設為以下兩個值之一：</p>
<p>NewestCall</p>
<p>OldestCall</p>
<p>預設值為 NewestCall。</p></td>
</tr>
<tr class="even">
<td><p><em>OverflowThreshold</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int16</p></td>
<td><p>任何一個時間可同時在佇列中的來電數目，超過此數目即觸發溢位動作。OverflowThreshold 可以是介於 0 和 1000 (含) 之間的任何整數值。預設值是 Null，表示在任何指定的時間中可在佇列中的來電數目沒有限制。</p></td>
</tr>
<tr class="odd">
<td><p><em>TimeoutAction</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.CallAction</p></td>
<td><p>如果到達逾時臨界值時採取的動作。TimeoutAction 必須使用 <strong>New-CsRgsCallAction</strong> Cmdlet 建立。</p></td>
</tr>
<tr class="even">
<td><p><em>TimeoutThreshold</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>來電可保留在佇列中的時間 (單位為秒)，來電過了這段時間後便算逾時。到時候系統便會採取由 TimeoutAction 參數指定的動作。</p>
<p>逾時臨界值可由任何介於 10 到 65535 秒 (含) (約 18 個小時) 的整數；預設值為 Null，這表示佇列永不逾時。</p></td>
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

無。**New-CsRgsQueue** 不接受管線傳送的輸入。

## 傳回類型

**New-CsRgsQueue** 會建立 Microsoft.Rtc.Rgs.Management.WritableSettings.Queue 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsRgsQueue](get-csrgsqueue.md)  
[Remove-CsRgsQueue](remove-csrgsqueue.md)  
[Set-CsRgsQueue](set-csrgsqueue.md)

