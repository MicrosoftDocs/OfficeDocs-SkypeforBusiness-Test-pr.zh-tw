---
title: New-CsRgsAnswer
TOCTitle: New-CsRgsAnswer
ms:assetid: aba521db-1741-4da3-aaf0-2d78fda4c4d2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412812(v=OCS.15)
ms:contentKeyID: 49291985
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsRgsAnswer

 

_**上次修改主題的時間：** 2015-03-09_

建立新的回應群組回覆。回應群組回覆可用來關聯來電回應及其對應動作。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsRgsAnswer -Action <CallAction> [-DtmfResponse <String>] [-Name <String>] [-VoiceResponseList <PSListModifier>]

## 詳細描述

為了處理來電，回應群組應用程式 通常會做出陳述或提出問題，然後依據客戶的回應採取動作。舉例來說，服務可能會要求來電者按 1 選擇英文，或按 2 選擇西班牙文。在提出這樣的問題後，系統必須等待來電者回應，然後再採取適當的動作。在此狀況下則代表，如果來電者按下電話鍵盤上的 1，來電會轉接到英文佇列，按下 2 則會轉接到西班牙文佇列。

回應群組回覆可用來分析來電回應並採取合適的動作。例如，如果給予來電者按 1 或 2 的選項，則需要兩個回應群組回覆，以便處理狀況：如果來電者按 1，會有一個回覆指定要採取的動作，如果按 2，則會有第二個回覆指定要採取的動作。這兩個回覆都是使用 **New-CsRgsAnswer** Cmdlet 建立，並且必須新增至合適的回應群組問題 (要求來電者按 1 或 2 的問題)。回應群組回覆必須包含一組允許的語音回應 (例如，字組「英文」)，或合適的電話鍵盤回應 (例如按 1)。或者，您可以給予客戶使用語音回應或鍵盤回應的選項：說出字組「英文」或按下電話鍵盤上的 1。(這些情況下使用的語音辨識是母項工作流程中使用的語言。)

回應群組接聽無法儲存和重複用於其他問題。例如，假設您有一個回覆是來電者按 9 可隨時將電話轉到語音信箱，您就建立了該回覆與回應群組問題的關聯性。稍後，您建立新問題，同樣給予來電者按 9 將電話轉接到語音信箱的選項。在這種情況下，您必須建立新的回應群組回覆執行個體；無法儲存回覆並反覆使用儲存的回覆。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsRgsAnswer** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。由於此 Cmdlet 會在記憶體內建立物件，而其本身亦不會變更系統，因此任何人皆可執行。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsRgsAnswer"}

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
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.CallAction</p></td>
<td><p>指出來電者隨時提供此回覆所要採取的動作。必須使用透過 <strong>New-CsRgsCallAction</strong> Cmdlet 所建立的物件參考來指定 Action 參數。如需詳細資訊，請參閱本主題中的＜範例＞區段。</p></td>
</tr>
<tr class="even">
<td><p><em>DtmfResponse</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>指出電話鍵盤上符合回覆的按鍵。例如，如果系統告知來電者按 1 為硬體，則 DtmfResponse 可設定為：-DtmfResponse 1。</p>
<p>單一接聽可以同時包含語音回應和雙音多頻 (DTMF) 回應。每一個回覆必須至少是兩種回應類型中的一種。</p></td>
</tr>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>給予回應群組回覆的名稱。名稱不一定是唯一的。</p></td>
</tr>
<tr class="even">
<td><p><em>VoiceResponseList</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>來電者可說出符合回覆的關鍵字陣列。例如，如果提供給來電者的一個選項是「硬體」，則 VoiceResponseList 屬性可設為：-VoiceResponseList &quot;Hardware&quot;。可使用 comma-separated 值指定多個關鍵字。例如，此參數值會使硬體或裝置符合回覆：-VoiceResponseList Hardware, Devices。語音回應不能包含雙引號，因為語音引擎無法辨識該字元。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsRgsAnswer** 不接受管線傳送的輸入。

## 傳回類型

建立 Microsoft.Rtc.Rgs.Management.WritableSettings.Answer 物件的新執行個體。

## 範例

## 範例 1

範例 1 所示的命令顯示如何建立與回應群組佇列和回應群組來電動作相關聯的新回應群組接聽。範例中的第一個命令使用 **New-CsRgsPrompt** Cmdlet 來建立新接聽的 TextToSpeechPrompt。之後，呼叫 **Get-CsRgsQueue** Cmdlet，傳回回應群組佇列 Help Desk 的物件參考 ($x)。接著在下一個命令中使用該物件參考，利用 **New-CsRgsCallAction** 建立將來電者轉移至 Help Desk 佇列的來電動作。此來電動作儲存在名為 $y 的變數中。

範例的最後一個命令是建立回應群組回覆 (儲存在變數 $a 中)。此回覆接受 DTMF 回應 1 (在電話鍵盤上按 1) 或語音回應「Yes」。

建立此回覆之後，該回覆即可和回應群組問題產生關聯。如需詳細資訊，請參閱 [New-CsRgsQuestion](new-csrgsquestion.md) 的＜說明＞主題。

    $w = New-CsRgsPrompt -TextToSpeechPrompt "Please hold while we transfer your call."
    $x = Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk"
    
    $y = New-CsRgsCallAction -Prompt $w -Action TransferToQueue -QueueID $x.Identity
    
    $a = New-CsRgsAnswer -Action $y -DtmfResponse 1 -VoiceResponseList Yes -Name "New Service Request"

## 請參閱

#### 其他資源

[New-CsRgsQuestion](new-csrgsquestion.md)

