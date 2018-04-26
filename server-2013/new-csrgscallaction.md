---
title: New-CsRgsCallAction
TOCTitle: New-CsRgsCallAction
ms:assetid: 07b70bbd-8e2e-426f-8c30-29f74b07b55b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398136(v=OCS.15)
ms:contentKeyID: 49289996
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsRgsCallAction

 

_**上次修改主題的時間：** 2015-03-09_

建立新的回應群組撥號動作。回應群組應用程式使用撥號動作決定系統接聽電話時的動作。例如，撥號動作可以指定將來電移轉到另一個佇列、詢問特定的回應群組問題，或是結束電話等。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsRgsCallAction -Action <Terminate | TransferToQueue | TransferToQuestion | TransferToUri | TransferToVoicemailUri | TransferToPstn> [-Prompt <Prompt>] [-Question <Question>] [-QueueID <RgsIdentity>] [-Uri <String>]

## 範例

## 範例 1

範例 1 所示的命令示範如何建立新的回應群組來電動作，然後將該動作指派給現有的回應群組佇列；在此範例中，來電動作會決定佇列溢位時所應採取的動作。為達此目的，會先使用 **Get-CsRgsQueue** 從 ApplicationServer:atl-cs-001.litwareinc.com 擷取回應群組應用程式佇列 Help Desk Overflow 佇列，並將來自該佇列的資訊儲存在名為 $x 的變數中。然後再使用類似的命令擷取 Help Desk 佇列，並將該資訊儲存在名為 $z 的變數中。

擷取佇列之後，使用 **New-CsRgsPrompt** Cmdlet 建立新來電動作隨附的文字轉語音提示。新的來電動作是透過執行 **New-CsRgsCallAction** Cmdlet 而建立。這個來電動作會被指派三個參數：Prompt (來電動作使用的提示)；Action (表示觸發新的來電動作時會進行的動作；TransferToQueue 參數值表示來電會轉接到不同的回應群組佇列)；QueueID 表示會將來電轉接到哪一個替代佇列 ($x.Identity 表示 Help Desk Overflow 佇列的 Identity)。這個新的來電動作會建立在記憶體中，然後儲存在名為 $y 的變數中。

建立來電動作之後，您便可以指派新的來電動作給 Help Desk 佇列；作法是將 OverflowAction 內容的值設為 $y，此變數包含剛建立的來電動作。如果 Help Desk 佇列「溢位」(亦即，達到允許的來電者數目上限)，則後續任何來電都會自動轉接到 Help Desk Overflow 佇列。

最後，範例中的最後一個命令會呼叫 **Set-CsRgsQueue**，將變更寫入 ApplicationServer:atl-cs-001.litwareinc.com 上的 Help Desk Overflow 佇列的實際執行個體。

    $x = Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk Overflow"
    $z = Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk"
    
    $w = New-CsRgsPrompt -TextToSpeechPrompt "Please hold while we transfer your call."
    $y = New-CsRgsCallAction -Prompt $w -Action TransferToQueue -QueueID $x.Identity
    $z.OverflowAction = $y
    Set-CsRgsQueue $z

## 範例 2

範例 2 所示的命令類似於範例 1 顯示的命令。不過在範例 2 中，新的來電動作會將來電轉接到 PSTN 電話號碼。為達此目的，新來電動作的 Action 內容設為 TransferToPSTN，而 Uri 內容設為 "sip:+14255551298@litwareinc.com"。

    $w = New-CsRgsPrompt -TextToSpeechPrompt "Please hold while we transfer your call."
    $y = New-CsRgsCallAction -Prompt $w -Action TransferToPSTN -Uri "sip:+14255551298@litwareinc.com"
    $z = Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk Queue"
    $z.OverflowAction = $y
    Set-CsRgsQueue $z

## 詳細描述

當某人撥打與回應群組應用程式相關聯的電話號碼時，應用程式會查閱對應於所撥電話號碼的工作流程。找到工作流程後，服務便會檢查該通電話是否是在非營業時間或是在假日時接到的。如果是，服務就會採取針對非營業時間內或假日時接到來電之指定動作 (例如將電話直接轉接到語音信箱)。如果是在營業時間接到電話，回應群組應用程式會採取針對營業時間來電所預先設定的動作。所有的動作都是事先決定的，而這些動作全都是使用 **New-CsRgsCallAction** Cmdlet 建立。**New-CsRgsCallAction** 可讓您將來電放置在回應群組佇列中；轉接到語音信箱、SIP 位址或公用交換電話網路 (PSTN) 電話號碼；轉接到互動語音回應 (IVR) 問題；或是終止電話，

使用 **New-CsRgsCallAction** 時，您不會直接修改工作流程、佇列或其他回應群組應用程式元素的內容。而是您所建立的新來電動作一開始只會存在於記憶體中，且必須儲存在物件參考變數 (例如 $x) 內。等到需要修改時 (例如工作流程的 DefaultAction 內容)，您就可以指派適當內容的物件參考。例如：

\-DefaultAction $x

請注意，只有下列兩個來電動作可以指派給 DefaultAction 內容：TransferToQueue 和 TransferToQuestion。針對在假日或在營業時間外發生的動作，除了 TransferToQueue 和 TransferToQuestion 以外，其他所有來電動作都有效。此外，TransferToQuestion 以外的所有來電動作都可用於佇列逾時和溢位。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsRgsCallAction** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。由於此 Cmdlet 會在記憶體內建立物件，而其本身亦不會變更系統，因此任何人皆可執行。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsRgsCallAction"}

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
<td><p><em>Action</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.Action</p></td>
<td><p>表示要採取的來電動作。動作必須設為下列其中一個值：</p>
<p>Terminate – 終止來電。</p>
<p>TransferToQueue – 將來電轉接到回應群組佇列。</p>
<p>TransferToQuestion – 將來電轉接到回應群組問題。</p>
<p>TransferToUri – 將來電轉接到指定的 SIP 統一資源識別元 (URI)。</p>
<p>TransferToVoiceMailUri – 將來電轉接到語音信箱。</p>
<p>TransferToPSTN – 將來電轉接到公用交換電話網路 (PSTN) 電話。</p>
<p>每次您建立新的來電動作時，必須指定 Action；沒有預設值。</p></td>
</tr>
<tr class="even">
<td><p><em>Prompt</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.Prompt</p></td>
<td><p>執行來電動作前播放的提示 (例如：「請稍候，我們將為您轉接」)。提示必須使用 <strong>New-CsRgsPrompt</strong> Cmdlet 建立。</p></td>
</tr>
<tr class="odd">
<td><p><em>Question</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.Question</p></td>
<td><p>當 Action 設為 TransferToQuestion 時要詢問的問題。問題必須使用 <strong>New-CsRgsQuestion</strong> Cmdlet 建立。</p>
<p>如果 Action 設為 TransferToQuestion，此參數就是必要的。</p></td>
</tr>
<tr class="even">
<td><p><em>QueueID</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>要將來電轉接到哪一個回應群組佇列的識別 (假定 Action 已設為 TransferToQueue)。使用 <strong>Get-CsRgsQueue</strong> 最能夠指定 QueueID 來擷取相關佇列的識別。</p>
<p>如果 Action 設為 TransferToQueue，此參數就是必要的。</p></td>
</tr>
<tr class="odd">
<td><p><em>Uri</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要將來電轉接到哪一個 SIP 位址、語音信箱 URI 或 PSTN 電話號碼。</p>
<p>如果 Action 設為 TransferToUri、TransferToVoiceMailUri 或 TransferToPSTN，此參數就是必要的。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsRgsCallAction** 不接受管線傳送的輸入。

## 傳回類型

**New-CsRgsCallAction** 會建立 Microsoft.Rtc.Rgs.Management.WritableSettings.CallAction 物件的新執行個體。

## 請參閱

#### 其他資源

[New-CsRgsQueue](new-csrgsqueue.md)  
[Set-CsRgsQueue](set-csrgsqueue.md)

