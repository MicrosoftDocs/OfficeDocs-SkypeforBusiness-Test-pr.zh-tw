---
title: Set-CsRgsWorkflow
TOCTitle: Set-CsRgsWorkflow
ms:assetid: 36cffa89-e5bb-48fd-bd6e-da67066fd273
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425845(v=OCS.15)
ms:contentKeyID: 49290574
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsRgsWorkflow

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的回應群組工作流程。工作流程可決定回應群組應用程式接聽電話時所要採取的動作。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsRgsWorkflow -Instance <Workflow> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會擷取現有的一組營業時間，然後將這些營業時間指派給名為 Help Desk 的工作流程。為了執行這項作業，範例的第一個命令會使用 **Get-CsRgsHoursOfBusiness**，從 ApplicationServer:atl-cs-001.litwareinc.com 服務擷取名為 U.S. Business Hours 的營業時間集合。這些營業時間儲存在名為 $businessHours 的變數中。

擷取營業時間之後，您可以使用 **Get-CsRgsWorkflow** Cmdlet 從 ApplicationServer:atl-cs-001.litwareinc.com 擷取 Help Desk 工作流程。此物件儲存在名為 $y 的變數中。

在範例的第三個命令中，Help Desk 工作流程的 BusinessHoursId 屬性設定為擷取的一組營業時間；作法是將 BusinessHoursId 設定為擷取集合的識別 ($businessHours.Identity)。在最後一個命令中，**Set-CsRgsWorkflow** 用於將新的營業時間寫入 ApplicationServer:atl-cs-001.litwareinc.com 上實際的 Help Desk 工作流程。這最後一個步驟很重要，因為在此之前，所有發生的變更都只在記憶體中。若要實際將這些變更儲存至 Help Desk 工作流程，您必須呼叫 **Set-CsRgsWorkflow**，並將包含工作流程虛擬複本的物件參考 ($y) 傳遞給 Cmdlet。

    $businessHours = Get-CsRgsHoursOfBusiness service:ApplicationServer:atl-cs-001.litwareinc.com -Name "US Business Hours"
    $y = Get-CsRgsWorkflow Service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk"
    $y.BusinessHoursId = $businessHours.Identity
    Set-CsRgsWorkflow -Instance $y

## 範例 2

範例 2 會將新描述指派給 ApplicationServer:atl-cs-001.litwareinc.com 服務上找到的 Help Desk 工作流程。為此，範例中的第一個命令會擷取指定的工作流程 (-Name "Help Desk")，並將擷取的物件儲存在名為 $x 的變數中。在第二個命令中，新描述 ("Workflow for the Redmond Help Desk") 會新增至 Help Desk 工作流程的虛擬複本。變更描述之後，命令 3 會使用 **Set-CsRgsWorkflow** 將這些變更寫回位於 ApplicationServer:atl-cs-001.litwareinc.com 上的實際 Help Desk 工作流程。

    $x = Get-CsRgsWorkflow service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk"
    $x.Description = "Workflow for the Redmond Help Desk" 
    Set-CsRgsWorkflow -Instance $x

## 範例 3

範例 3 所示的命令會匯入新的回應群組音訊檔，然後將此音訊檔指派給現有的工作流程。為達此目的，範例中的第一個命令會匯入新的音訊檔。作法是呼叫 **Get-Content** Cmdlet，在音訊檔 (C:\\MediaFiles\\Hold.wav) 中逐位元組地讀取。為確保能正確地讀取音訊檔，必須加入 ReadCount 參數 (設為 0) 和 Encoding 參數 (設為 Byte)。讀入音訊檔之後，會將資料管線傳送到 **New-CsRgsAudioFile**，以在 ApplicationServer:atl-cs-001.litwareinc.com 上建立新檔案，並將該檔案 (名稱為 HelpDeskHoldMusic.wav) 的物件參考儲存在名為 $musicFile 的變數中。

建立音訊檔之後，命令 2 會從 ApplicationServer:atl-cs-001.litwareinc.com 擷取 Help Desk 工作流程，並將傳回的物件儲存在名為 $y 的變數中。命令 3 會將值 $musicFile 指派給此工作流程的 CustomMusicOnHoldFile 屬性；這是包含新建立的音訊檔的變數。

$musicFile 指派給 CustomMusicOnHoldFile之後，最後一個命令會使用 **Set-CsRgsWorkflow** Cmdlet，將這些變更寫回 Help Desk 工作流程。

    $musicFile = Get-Content -ReadCount 0 -Encoding Byte C:\MediaFiles\Hold.wav | Import-CsRgsAudioFile -Identity Service:ApplicationServer:atl-cs-001.litwareinc.com -FileName "HelpDeskHoldMusic.wav"
    $y = Get-CsRgsWorkflow -Identity Service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk"
    $y.CustomMusicOnHoldFile = $musicFile
    Set-CsRgsWorkflow -Instance $y

## 詳細描述

工作流程或許是 回應群組應用程式 中的關鍵元素。每個工作流程只會與一個電話號碼產生關聯，當有人撥打該號碼時，工作流程便會決定如何處理這通電話。例如，系統會將電話路由傳送至一系列的互動語音回應 (IVR) 問題，這些問題會提示來電者輸入額外的資訊 (例如「硬體支援請按 1)。如需要軟體支援，請按 2。」)或者，來電可能會被放置在佇列中並保留來電者，直到代理可接聽來電。代理是否可接聽電話的狀態，也是由工作流程指定的：工作流程可用來設定營業時間 (一星期的哪幾天和哪些時段會有代理接聽電話) 與假日 (代理無法接聽電話的日子)。

**Set-CsRgsWorkflow** Cmdlet 提供您修改現有工作流程屬性的方法；例如，您可以變更工作流程的電話號碼、變更與工作流程相關聯的代理群組，或變更每當觸發工作流程時要採取的預設動作 (亦即，每當有人撥打與工作流程相關聯的電話號碼)。

**Set-CsRgsWorkflow** 不會直接修改工作流程本身。反之，如果您必須變更工作流程，您必須先使用 **Get-CsRgsWorkflow** 來建立該工作流程的物件參考；也就是說，請擷取有興趣的工作流程，然後將傳回的物件儲存在變數中。建立物件參考之後，您修改記憶體中的物件內容，然後使用 **Set-CsRgsWorkflow** 將這些變更寫回實際的回應群組應用程式工作流程。如果您沒有呼叫 **Set-CsRgsWorkflow**，則您的變更只會存在於記憶體中，且當您關閉 Windows PowerShell 或刪除物件參考變數時，變更就會消失。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsRgsWorkflow** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsRgsWorkflow"}

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
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.Workflow</p></td>
<td><p>待修改 回應群組應用程式 工作流程的物件參考。物件參考通常是使用 <strong>Get-CsRgsWorkflow</strong> Cmdlet 來擷取，並將傳回的值指派至變數；例如，此命令將物件參考傳回至名為 Help Desk 的工作流程，並將該物件參考儲存在名為 $x 的變數中：</p>
<p>$x = Get-CsRgsWorkflow service:ApplicationServer:atl-cs-001.litwareinc.com -Name &quot;Help Desk&quot;</p>
<p>Instance 參數是位置參數：只要工作流程的物件參考是命令中使用的第一個參數值，就可以省略。這表示下列兩個命令的功能相同：</p>
<p>Set-CsRgsWorkflow –Instance $x</p>
<p>Set-CsRgsWorkflow $x</p></td>
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

Microsoft.Rtc.Rgs.Management.WritableSettings.Workflow 物件。**Set-CsRgsWorkflow** 接受管線傳送的回應群組工作流程物件執行個體。

## 傳回類型

**Set-CsRgsWorkflow** 不會傳回任何物件或值，而會修改現有的 Microsoft.Rtc.Rgs.Management.WritableSettings.Workflow 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsRgsWorkflow](get-csrgsworkflow.md)  
[New-CsRgsWorkflow](new-csrgsworkflow.md)  
[Remove-CsRgsWorkflow](remove-csrgsworkflow.md)

