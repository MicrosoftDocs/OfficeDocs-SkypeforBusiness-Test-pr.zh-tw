---
title: Import-CsAnnouncementFile
TOCTitle: Import-CsAnnouncementFile
ms:assetid: 66da2361-e325-4085-8b6f-47a8423edaab
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398472(v=OCS.15)
ms:contentKeyID: 49291159
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Import-CsAnnouncementFile

 

_**上次修改主題的時間：** 2015-03-09_

將宣告檔案匯入至宣告服務音訊媒體庫。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Import-CSAnnouncementFile -Content <Byte[]> -FileName <String> -Parent <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

這些命令會將音訊檔案匯入宣告服務 檔案存放區。由於音訊檔案必須以位元組陣列的方式匯入，因此我們首先需要呼叫 **Get-Content** Cmdlet，將音訊檔案擷取為個別位元組的陣列。**Get-Content** 是 Windows PowerShell 內建的 Cmdlet，我們會將用於宣告的檔案名稱 (含路徑) 傳遞給此 Cmdlet。接著，我們會將 0 這個值傳遞 ReadCount 參數，表示我們要一次讀取整個檔案。然後，我們會將 Byte 這個值傳遞到 Encoding 參數，指示 **Get-Content** 我們需要檔案的內容做為位元組陣列。我們將該陣列指派給變數 $a。

在第二行中，我們呼叫 **Import-CsAnnouncementFile** Cmdlet 以實際匯入檔案。我們將 Identity 為 ApplicationServer:redmond.litwareinc.com 的服務傳遞到 Parent 參數，然後將名稱傳遞到 FileName 參數 (WelcomeMessage.wav)。這可以是任何有效的 Windows 作業系統檔案名稱，但應該以 .wav 或 .wma 副檔名為結尾。最後，我們會傳遞變數 $a 做為 Content 參數的值，以便在我們的位元組陣列中讀取。

    $a = Get-Content ".\GreetingFile.wav" -ReadCount 0 -Encoding Byte
    Import-CsAnnouncementFile -Parent ApplicationServer:redmond.litwareinc.com -FileName "WelcomeMessage.wav" -Content $a

## 範例 2

範例 2 與範例 1 相同，但是我們在括號中加入了 **Get-Content** 命令做為 Content 參數的值，而不是另外呼叫該命令並將它指派給變數。

    Import-CsAnnouncementFile -Parent ApplicationServer:redmond.litwareinc.com -FileName "WelcomeMessage.wav" -Content (Get-Content ".\GreetingFile.wav" -ReadCount 0 -Encoding Byte)

## 範例 3

範例 3 是範例 1 的另一種變化。此範例中的差異在於不使用 Content 參數，而是先呼叫 **Get-Content** Cmdlet，然後將結果傳送到 **Import-CsAnnouncementFile**。這是從遠端工作階段匯入宣告檔案最可靠的方式。

    Get-Content ".\GreetingFile.wav" -ReadCount 0 -Encoding Byte | Import-CsAnnouncementFile -Parent ApplicationServer:redmond.litwareinc.com -FileName "WelcomeMessage.wav"

## 詳細描述

此 Cmdlet 會以位元組陣列的方式，將音訊檔案匯入到宣告服務音訊媒體庫。這可讓檔案針對未指派的號碼，當做宣告播放。

執行此 Cmdlet 會將音訊檔案匯入媒體庫。當檔案匯入之後，可藉由呼叫 **New-CsAnnouncement** Cmdlet 或 **Set-CsAnnouncement** Cmdlet，並傳遞檔案名稱及相關聯的服務做為參數，在宣告中使用該檔案。屆時，可以呼叫 **New-CsUnassignedNumber** 或 **Set-CsUnassignedNumber** Cmdlet，將宣告指派到特定的號碼範圍。

匯入的檔案必須為 WAV 或 WMA 檔案。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Import-CsAnnouncementFile** Cmdlet：RTCUniversalServerAdmins。不過，具有目的地電腦檔案存放區寫入權的任何人，也可以執行此 Cmdlet。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Import-CsAnnouncementFile"}

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
<td><p>音訊檔案當做位元組陣列的內容。</p></td>
</tr>
<tr class="even">
<td><p><em>FileName</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>您希望檔案在 檔案存放區 中所具備的名稱。您將會在呼叫 <strong>New-CsAnnouncement</strong>或 <strong>Set-CsAnnouncement</strong> Cmdlet 時的 AudioFilePrompt 參數中，使用此名稱將檔案指派給宣告。</p></td>
</tr>
<tr class="odd">
<td><p><em>Parent</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>執行相關聯宣告服務之應用程式伺服器的服務識別碼。</p></td>
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
<td><p>隱藏變更前所顯示的確認提示。</p></td>
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

Byte\[\]。接受音訊檔中的位元組陣列。位元組陣列必須以單一記錄來傳送。請參閱範例 3。

## 傳回類型

這個 Cmdlet 不會傳回值。

