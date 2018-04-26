---
title: Set-CsCallParkServiceMusicOnHoldFile
TOCTitle: Set-CsCallParkServiceMusicOnHoldFile
ms:assetid: af5e7573-4bfd-47b1-a92b-83b06a537158
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412836(v=OCS.15)
ms:contentKeyID: 49292018
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCallParkServiceMusicOnHoldFile

 

_**上次修改主題的時間：** 2015-03-09_

變更要對保留或駐留通話之來電者播放的音訊檔案。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsCallParkServiceMusicOnHoldFile -Content <Byte[]> -Service <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會設定 SoothingMusic.wma 檔案做為向保留通話之來電者播放的音訊檔案。此範例的第一行會呼叫 **Get-Content** Cmdlet。此 Cmdlet 只會讀取檔案的內容，並將它們指派給變數 $a (在此範例中)。我們將 0 值傳遞到 ReadCount 參數，因此 **Get-Content** Cmdlet 便能立即讀取整個檔案 (而不是嘗試逐行讀取，逐行讀取就不會套用至音訊檔案)。我們將 Encoding 參數設為 byte。這會告訴 **Get-Content** Cmdlet，我們要讀入變數 $a 的內容是位元組陣列，而非 .wma 格式的音訊檔案。

此範例的第 2 行是真正指定音訊檔案的地方。我們呼叫 **Set-CsCallParkServiceMusicOnHoldFile** Cmdlet，並指定「通話駐留」服務執行的服務識別碼。然後將讀取到變數 $a 中的音訊檔案內容傳遞到 Content 參數 (請記得，這些內容必須是位元組格式)。

    $a = Get-Content -ReadCount 0 -Encoding byte "C:\MoHFiles\soothingmusic.wma"
    Set-CsCallParkServiceMusicOnHoldFile -Service ApplicationServer:pool0.litwareinc.com -Content $a

## 詳細描述

通話保留代接是允許使用者「駐留」來電的服務。保留通話會將來電轉接到指定範圍中的號碼，並立即保留來電。根據「通話駐留 」服務的組態設定，可以在駐留通話時向來電者播放等候音樂。使用這個 Cmdlet 可變更向等候保留通話之來電者播放的音訊檔案 (等候音樂)。

唯有「通話駐留」服務的 EnableMusicOnHold 屬性設為 True 時，才會播放等候音樂。您可以呼叫 **Get-CsCpsConfiguration** Cmdlet 來檢查此屬性。您可以在建立保留通話設定時使用 **New-CsCpsConfiguration** Cmdlet，或在保留通話設定已存在時呼叫 **Set-CsCpsConfiguration** Cmdlet，來設定此屬性。此屬性預設為 True。

Lync Server 附有預設的「通話駐留」服務等候音樂檔案。若未指定音訊檔案，會使用預設檔案。

音訊檔案必須是下列其中一種格式：Windows Media Audio 9、44 kHz、16 位元、單聲道、CBR 或 32 kbps。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsCallParkServiceMusicOnHoldFile** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCallParkServiceMusicOnHoldFile"}

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
<td><p>音訊檔案的內容，使用位元組格式。</p>
<p>使用 <strong>Get-Content</strong> Cmdlet 擷取位元組格式的音訊檔案內容 (如需詳細資訊，請參閱本主題中的＜範例＞區段)。</p></td>
</tr>
<tr class="even">
<td><p><em>Service</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>通話駐留服務所在的服務 ID；例如，ApplicationServer:pool0.litwareinc.com。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
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

Byte\[\]。接受包含等候音樂檔案之位元組陣列管線傳送的輸入。

## 傳回類型

此 Cmdlet 不會傳回值。

## 請參閱

#### 其他資源

[New-CsCpsConfiguration](new-cscpsconfiguration.md)  
[Remove-CsCpsConfiguration](remove-cscpsconfiguration.md)  
[Set-CsCpsConfiguration](set-cscpsconfiguration.md)  
[Get-CsCpsConfiguration](get-cscpsconfiguration.md)

