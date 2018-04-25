---
title: New-CsRgsPrompt
TOCTitle: New-CsRgsPrompt
ms:assetid: 6812acbf-ae56-43a6-a2d7-e28a930f81c7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398486(v=OCS.15)
ms:contentKeyID: 49291187
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsRgsPrompt

 

_**上次修改主題的時間：** 2015-03-09_

為回應群組應用程式建立新的工作流程提示。工作流程提示可以是播放的音訊檔，或是讀出聲音的文字，以提供來電者額外的資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsRgsPrompt [-AudioFilePrompt <AudioFile>] [-TextToSpeechPrompt <String>]

## 範例

## 範例 1

範例 1 所示的命令會示範如何在新的來電動作中加入工作流程提示 (與回應群組佇列)。第一個命令會使用 **Get-CsRgsQueue** Cmdlet 將物件參考 ($queue) 傳回 Help Desk 回應群組佇列。第二個命令會接著使用 **New-CsRgsPrompt** Cmdlet 建立新的文字轉換語音提示 "Welcome to the help desk. Please hold."。此新提示會儲存在名為 $prompt 的變數中。

範例中的最後一個命令使用 **New-CsRgsCallAction** 來建立新的回應群組來電動作 ($z)。建立來電動作時，會使用物件參考 $prompt (包含新建立的工作流程提示) 做為 Prompt 參數的值；同樣的也會將物件參考 $queue 結合 QueueID 參數使用。執行此命令後，新的來電動作及其新的工作流程提示便準備好可新增到回應群組工作流程。

    $queue = Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk"
    
    $prompt = New-CsRgsPrompt -TextToSpeechPrompt "Welcome to the help desk. Please hold."
    
    $z = New-CsRgsCallAction -Prompt $prompt -Action TransferToQueue -QueueID $queue.Identity

## 範例 2

範例 2 所示的命令是範例 1 所示命令的變化，但在此狀況下，新的工作流程提示除了文字轉換語音提示之外，還包括音訊檔提示。為了在工作流程提示中包含音訊檔，範例中的第二個命令使用 **Import-CsRgsAudioFile** Cmdlet 匯入 C:\\Media\\Welcome.wav 音訊檔。匯入的檔案之後會儲存在名為 $audioFile 的變數中。

匯入音訊檔後，該音訊檔與文字轉換語音提示都會新增到新的工作流程提示 ($prompt)。為達此目的，AudioFilePrompt 參數會設為 $audioFile，TextToSpeechPrompt 參數會設為文字值 "Welcome to the help desk.Please hold."。

    $queue = Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk Queue"
    
    $audioFile = Import-CsRgsAudioFile -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" -FileName "welcome.wav" -Content (Get-Content C:\Media\Welcome.wav -Encoding byte -ReadCount 0)
    
    $prompt = New-CsRgsPrompt -AudioFilePrompt $audioFile -TextToSpeechPrompt "Welcome to the help desk. Please hold."
    
    $z = New-CsRgsCallAction -Prompt $prompt -Action TransferToQueue -QueueID $queue.Identity

## 詳細描述

藉此充分告知來電者接下來的動作與原因，這對於回應群組工作流程而言很重要。例如，您設定了要接聽電話的工作流程，然後立即保留這通電話直到代理接聽為止。這樣的設定沒有問題，但還需要告知來電者：1) 電話已接聽；2) 電話將保留到有代理接聽為止。提供這類資訊是工作流程提示的工作。

回應群組應用程式支援兩種不同的工作流程提示。第一種是預錄音訊檔，然後再播放。若要執行此作業，必須錄製 .WAV 或 .WMA 格式的提示 ("Please hold. Your call is important to us." (請不要掛斷。我們十分重視您的來電))，使用 **Import-CsRgsAudioFile** Cmdlet 匯入檔案，然後將檔案指派給工作流程提示。或者，您可以只提供要讀出的文字，當需要提示時，回應群組應用程式會使用其文字轉換語音功能大聲「讀」出文字。文字轉換語音提示的設定較為簡單：不需要錄製與匯入音訊檔。不過，音訊檔提示通常音質比較好，也比較逼真。

請注意，文字轉語音提示中使用的語言與母項工作流程中使用的語言相同。

**New-CsRgsPrompt** Cmdlet 可讓您建立工作流程提示。每次需要使用提示時，都必須從頭開始建立，無法儲存提示以重複使用。(這表示您也必須重新匯入音訊檔)。建立新的工作流程提示時，您必須提供文字轉換語音提示，如果您想要，也可以提供音訊檔提示。當您同時提供文字轉換語音與音訊檔提示時，回應群組應用程式會根據預設使用音訊檔，只有在音訊檔無法使用時，才會使用文字轉換語音提示。在記憶體內建立新的提示後，通常會接著將對應的物件參考新增到回應群組來電動作中。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsRgsPrompt** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。由於此 Cmdlet 會在記憶體內建立物件，而其本身亦不會變更系統，因此任何人皆可執行。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsRgsPrompt"}

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
<td><p><em>AudioFilePrompt</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.AudioFile</p></td>
<td><p>工作流程啟用時播放的音訊檔。音訊檔必須使用 <strong>Import-CsRgsAudioFile</strong> Cmdlet 匯入。</p></td>
</tr>
<tr class="even">
<td><p><em>TextToSpeechPrompt</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>工作流程啟用時讀出的文字轉換語音 ( TTS) 提示。TTS 提示只有在未指定音訊檔時才會使用，最多可容納 4096 個字元。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsRgsPrompt** 不接受管線傳送的輸入。

## 傳回類型

**New-CsRgsPrompt** 建立 Microsoft.Rtc.Management.WritableSettings.Prompt 物件的執行個體。

## 請參閱

#### 其他資源

[Import-CsRgsAudioFile](import-csrgsaudiofile.md)  
[New-CsRgsCallAction](new-csrgscallaction.md)

