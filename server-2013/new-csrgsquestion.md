---
title: New-CsRgsQuestion
TOCTitle: New-CsRgsQuestion
ms:assetid: 0ed9f3b4-cbc5-41ca-8547-2300b579b119
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398186(v=OCS.15)
ms:contentKeyID: 49290101
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsRgsQuestion

 

_**上次修改主題的時間：** 2015-03-09_

建立新的回應群組問題。回應群組應用程式會使用問題供來電者選擇，然後再根據這些選擇採取動作。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsRgsQuestion -Prompt <Prompt> [-AnswerList <PSListModifier>] [-InvalidAnswerPrompt <Prompt>] [-Name <String>] [-NoAnswerPrompt <Prompt>]

## 範例

## 範例 1

範例 1 所示的命令會建立兩個回應群組回覆，再將這兩個回覆與新的回應群組問題產生關聯。為了建立這兩個回覆，您必須先指定根據來電者提供的回覆所採取的來電動作。因此，範例中的前兩個命令會建立以下兩個回應群組佇列的物件參考：New Service Request 和 Existing Service Request。建立這些物件參考後，下個命令會使用 **New-CsRgsPrompt** 建立文字轉換語音提示，並以名稱為 $w 的變數儲存該提示。

該作業完成時，下兩個命令會建立兩個對應的來電動作：一個是將來電者轉接到 \[新增服務要求\] 佇列，另一個是將來電者轉接到 \[現有服務要求\] 佇列。建立來電動作後，會使用 **New-CsRgsAnswer** Cmdlet 建立兩個回應群組答覆，一個會儲存在 $newRequest 變數中，另一個則儲存在 $existingRequest 變數中。

儲存兩個回覆後，便能使用 **New-CsRgsPrompt** 建立新問題的提示。在本範例中，提示就是指文字轉換語音提示，此提示會要求來電者按下 1 (或說出「新增」) 選擇新的服務要求，或按下 2 (或說出「現有」) 選擇現有的服務要求。該提示本身會儲存在名稱為 $u 的變數中。

建立提示後，可以呼叫 **New-CsRgsQuestion** 以建立新問題。除了 Prompt 參數外，還會使用 AnswerList 參數指出與問題關聯的兩個回覆：變數 $newRequest 與 $existingRequest。

    $new = Get-CsRgsQueue -Identity service:ApplicationServer:pool0.litwareinc.com -Name "New Service Request"
    $existing = Get-CsRgsQueue -Identity service:ApplicationServer:pool0.litwareinc.com -Name "Existing Service Request"
    
    $w = New-CsRgsPrompt -TextToSpeechPrompt "Please hold while we transfer your call."
    
    $y = New-CsRgsCallAction -Prompt $w -Action TransferToQueue -QueueID $new.Identity
    $z = New-CsRgsCallAction -Prompt $w -Action TransferToQueue -QueueID $existing.Identity
    
    $newRequest = New-CsRgsAnswer -Action $y -DtmfResponse 1 -VoiceResponseList "New" -Name "New Request"
    $existingRequest = New-CsRgsAnswer -Action $z -DtmfResponse 2 -VoiceResponseList "Existing" -Name "Existing Request"
    
    $u = New-CsRgsPrompt -TextToSpeechPrompt "Press 1 or say New for a new service request. Press 2 or say Existing for an existing service request."
    
    $question = New-CsRgsQuestion -Prompt $u -AnswerList $newRequest $newRequest, $existingRequest 

## 詳細描述

為了處理來電，回應群組應用程式通常會做出陳述或提出問題，然後根據來電者的回應採取動作。舉例來說，服務可能會要求來電者按 1 選擇英文，或按 2 選擇西班牙文。在提出這樣的問題後，系統必須等待來電者回應，然後再採取適當的動作。在此狀況下則代表，如果來電者按下電話鍵盤上的 1，來電會轉接到英文佇列，按下 2 則會轉接到西班牙文佇列。

為了建立問題，您必須使用 **New-CsRgsQuestion** Cmdlet。建立回應群組問題時，您必須至少提供提示 (也就是實際的問題本身) 與一組支援的回覆。例如，如果您提供給來電者按下 1 或 2 的選項，那麼您必須有兩個回覆：一個回覆是指定如果來電者按下 1 時採取的動作，另一個回覆則是指定如果來電者按下 2 時採取的動作。如果您提供來電者按下 1、2、3 或 4 的選項，則必須有四個回覆，依此類推。

此外 **New-CsRgsQuestion** 讓您能夠指定當來電者提供的回覆無效，或者完全不回覆時使用的提示。例如，如果原始案例中的來電者按下 3，則提示會提醒來電者「抱歉，並非有效回應」。此時會重新播放原始提示。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsRgsQuestion** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。由於此 Cmdlet 會在記憶體內建立物件，而其本身亦不會變更系統，因此任何人皆可執行。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsRgsQuestion"}

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
<td><p><em>Prompt</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.Prompt</p></td>
<td><p>要詢問來電者的問題。提示必須使用 <strong>New-CsRgsPrompt</strong> Cmdlet 建立。</p></td>
</tr>
<tr class="even">
<td><p><em>AnswerList</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>問題的有效回覆陣列。例如，服務台問題的回覆可能有「硬體支援」、「軟體安裝」，以及「網路連線」。回覆必須使用 <strong>New-CsRgsAnswer</strong> Cmdlet 建立。</p></td>
</tr>
<tr class="odd">
<td><p><em>InvalidAnswerPrompt</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.Prompt</p></td>
<td><p>當來電者選擇的回覆無效時會發出的回應。InvalidAnswerPrompt 必須使用 <strong>New-CsRgsPrompt</strong> Cmdlet 建立。請注意，播放 InvalidAnswerPrompt 後，應用程式會接著重複原始提示。</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>問題的識別碼。問題名稱不必是唯一，長度上限為 128 個字元。</p></td>
</tr>
<tr class="odd">
<td><p><em>NoAnswerPrompt</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.Prompt</p></td>
<td><p>當來電者沒有回應一開始的提示時會發出的回應。NoAnswerPrompt 必須使用 <strong>New-CsRgsPrompt</strong> 指令提示建立。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsRgsQuestion** 不接受管線傳送的輸入。

## 傳回類型

**New-CsRgsQuestion** 會建立 Microsoft.Rtc.Management.WriteableSettings.Question 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsRgsAnswer](new-csrgsanswer.md)

