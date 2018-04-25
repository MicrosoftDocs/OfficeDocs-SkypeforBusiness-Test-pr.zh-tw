---
title: Import-CsRgsAudioFile
TOCTitle: Import-CsRgsAudioFile
ms:assetid: ae9dfd76-9b3e-4c51-9692-39d1fe8e430b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412830(v=OCS.15)
ms:contentKeyID: 49292011
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Import-CsRgsAudioFile

 

_**上次修改主題的時間：** 2015-03-09_

匯入新的音訊檔與回應群組應用程式搭配使用。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Import-CsRgsAudioFile -Content <Byte[]> -FileName <String> -Identity <RgsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會匯入音訊檔 (C:\\Media\\WhileYouWait.wav)，然後將該檔指派給工作流程的 CustomMusicOnHold 屬性。為了執行這項作業，第一個命令會使用 **Import-CsRgsAudioFile** 將音訊匯入到 ApplicationServer:atl-cs-001.litwareinc.com 上找到的 回應群組應用程式。除了 Identity 參數 (指出服務位置) 外，也會使用 FileName 參數指定要匯入檔案的檔案名稱。

同時會使用 Content 參數來匯入音訊檔。執行檔案匯入的做法為呼叫 **Get-Content**，程式後面要加上匯入檔案的路徑。**Get-Content** 也必須將編碼類型設為位元組，將 ReadCount 設定 0 (將 ReadCount 設為 0 可確保以單一作業能讀取整個檔案)。匯入的檔案會儲存在名為 $x 的變數中。

在第二個命令中，使用 **Get-CsRgsWorkflow** 來建立 Help Desk Workflow 工作流程的物件參考 ($y)。建立此物件參考後，命令 3 會將 CustomMusicOnHoldFile 屬性的值設為 $x (包含所匯入音訊檔的變數)。最後，範例中的最後一個屬性會使用 **Set-CsRgsWorkflow** 將這些變更寫入真正的 Help Desk Workflow 工作流程中。如果您沒有呼叫 **Set-CsRgsWorkflow**，您所做的修改只會存在於記憶體中，只要關閉 Windows PowerShell 或刪除變數 $x 或 $y 消失，修改就會消失。

    $x = Import-CsRgsAudioFile -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" -FileName "WhileYouWait.wav" -Content (Get-Content C:\Media\WhileYouWait.wav -Encoding byte -ReadCount 0)
    
    $y = Get-CsRgsWorkflow -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" -Name "Help Desk Workflow"
    $y.CustomMusicOnHoldFile = $x
    
    Set-CsRgsWorkflow $y

## 詳細描述

回應群組應用程式 至少有兩種不同的方式可使用音訊檔 (僅限 .WAV 或 .WMA 格式)。例如，任何時候當將來電者保留時，服務可播放音樂 (或某種類型的宣告)。另外，回應群組應用程式偶爾會與來電者「對話」；例如，透過互動語音回應 (IVR)，服務可能向來電者詢問問題，例如「您是否為了現有訂單來電？」您可以讓服務使用文字轉語音技術來讀取這些問題，或播放真人詢問問題的音訊錄音。

無論您選擇使用音訊檔的方法為何，皆須使用 **Import-CsRgsAudioFile** Cmdlet 將檔案本身匯入回應群組應用程式。請注意，每次您要使用音訊檔時，都必須執行 **Import-CsRgsAudioFile**，即使該檔案已在回應群組應用程式的他處使用。例如，假設工作流程 A 使用指定的音訊檔做為自訂等候音樂檔，而您現在想要使用相同的音訊檔做為工作流程 B 的自訂等候音樂。即使回應群組應用程式已使用音訊檔，您仍然需要匯入檔案，才能用於工作流程 B。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Import-CsRgsAudioFile** Cmdlet：RTCUniversalServerAdmins。您也必須具有目標電腦檔案存放區的寫入權。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Import-CsRgsAudioFile"}

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
<td><p><em>Content</em></p></td>
<td><p>必要</p></td>
<td><p>System.Byte[]</p></td>
<td><p>要匯入之音訊檔實際內容。Content 屬性是透過呼叫 <strong>Get-Content</strong> Cmdlet 填入的。呼叫 <strong>Get-Content</strong> 時，將 Encoding 參數設為位元組，並將 ReadCount 參數設為 0 (如需詳細資訊，請參閱本主題的＜範例＞一節)。</p></td>
</tr>
<tr class="even">
<td><p><em>FileName</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要匯入之音訊檔檔案名稱。例如，C:\Media\Welcome.wav 的檔案名稱是：Welcome.wav。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>要將音訊檔匯入的服務識別(這必須與主控回應群組應用程式的服務相同)。例如：-Identity &quot;service:ApplicationServer:atl-cs-001.litwareinc.com&quot;。</p></td>
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

無。**Import-CsRgsAudioFile** 不接受管線傳送的輸入。

## 傳回類型

建立 Microsoft.Rtc.Rgs.Management.WritableSettings.AudioFile 物件的新執行個體。

## 請參閱

#### 其他資源

[New-CsRgsWorkflow](new-csrgsworkflow.md)  
[Set-CsRgsWorkflow](set-csrgsworkflow.md)

