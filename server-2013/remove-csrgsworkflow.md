---
title: Remove-CsRgsWorkflow
TOCTitle: Remove-CsRgsWorkflow
ms:assetid: 9626df55-e3ed-478a-a485-f2a9abcf493b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398765(v=OCS.15)
ms:contentKeyID: 49291745
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsRgsWorkflow

 

_**上次修改主題的時間：** 2015-03-09_

刪除現有的回應群組工作流程。工作流程可決定回應群組應用程式接聽電話時所要採取的動作。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsRgsWorkflow -Instance <Workflow> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會從 ApplicationServer:atl-cs-001.litwareinc.com 服務移除所有回應群組工作流程。為達此目的，命令會先呼叫 **Get-CsRgsWorkflow** 傳回在 ApplicationServer:atl-cs-001.litwareinc.com 上找到之所有工作流程的集合。然後再將該集合管線傳送到 **Remove-CsRgsWorkflow**，以刪除集合中的每一個工作流程。

    Get-CsRgsWorkflow -Identity Service:ApplicationServer:atl-cs-001.litwareinc.com | Remove-CsRgsWorkflow

## 範例 2

範例 2 所示的命令會刪除單一回應群組工作流程：位於 ApplicationServer:atl-cs-001.litwareinc.com 服務上，名為 "Help Desk Workflow" 的工作流程。為達此目的，先使用 **Get-CsRgsWorkflow** 從服務 ApplicationServer:atl-cs-001.litwareinc.com 傳回名為 Help Desk Workflow 的工作流程。該工作流程接著會被傳送到 **Remove-CsRgsWorkflow**，並予以刪除。

    Get-CsRgsWorkflow service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk Workflow" | Remove-CsRgsWorkflow

## 範例 3

範例 3 會從 ApplicationServer:atl-cs-001.litwareinc.com 服務刪除所有語言為美國英文的工作流程。為達此目的，命令會先使用 **Get-CsRgsWorkflow** 擷取在 ApplicationServer:atl-cs-001.litwareinc.com 上找到的所有工作流程。然後再將該集合管線傳送到 **Where-Object** Cmdlet，以選取語言等於美國英文 (en-us) 的工作流程。接著將篩選後的集合管線傳送到 **Remove-CsRgsWorkflow** Cmdlet，以刪除集合中的每一個項目。

    Get-CsRgsWorkflow service:ApplicationServer:atl-cs-001.litwareinc.com | Where-Object {$_.Language -eq "en-us"} | Remove-CsRgsWorkflow

## 範例 4

範例 4 所顯示的命令會刪除 ApplicationServer:atl-cs-001.litwareinc.com 服務上已設定 CustomMusicOnHoldFile 屬性值的所有回應群組工作流程。為達此目的，命令會先使用 **Get-CsRgsWorkflow** 傳回在 ApplicationServer:atl-cs-001.litwareinc.com 上找到的所有工作流程集合。然後再將該集合管線傳送到 **Where-Object** Cmdlet，以選取 CustomMusicOnHoldFile 屬性不等於 Null 值的工作流程 (若此屬性不等於 Null 值，表示已為此工作流程定義自訂音樂)。接著將篩選後的集合管線傳送到 **Remove-CsRgsWorkflow**，以移除集合中的每一個項目。

    Get-CsRgsWorkflow service:ApplicationServer:atl-cs-001.litwareinc.com | Where-Object {$_.CustomMusicOnHoldFile -ne $Null} | Remove-CsRgsWorkflow

## 詳細描述

工作流程是回應群組應用程式中的關鍵元素。每個工作流程只會與一個電話號碼產生關聯，當有人撥打該號碼時，工作流程便會決定如何處理這通電話。例如，系統會將電話路由傳送至一系列的互動語音回應 (IVR) 問題，這些問題會提示來電者輸入額外的資訊 (「硬體支援請按 1)。如需要軟體支援，請按 2。」)或者，來電可能會被放在佇列中並保留來電者，直到代理可接聽來電。代理是否可接聽電話的狀態，也是由工作流程指定的：工作流程可用來維護營業時間 (一星期的哪幾天和哪些時段會有代理接聽電話) 與假日 (代理無法接聽電話的日子)。

使用 **New-CsRgsWorkflow** Cmdlet 可建立新的工作流程。這些工作流程建立之後，日後可使用 **Remove-CsRgsWorkflow** 刪除。請注意，當您刪除工作流程時，工作流程會從 回應群組應用程式 完全移除。如果要暫時停用工作流程，請勿使用 **Remove-CsRgsWorkflow**；請改用 **Set-CsRgsWorkflow** Cmdlet 來停用 (日後再重新啟用) 工作流程。

如果您嘗試刪除作用中的工作流程，**Remove-CsRgsWorkflow** 會提示您確認您是否真的要刪除工作流程；在回應提示之前，**Remove-CsRgsWorkflow** 不會採取進一步動作。若要略過此提示，以無訊息的方式刪除作用中的工作流程，請使用 Force 參數。例如：

Get-CsRgsWorkflow –Identity "service:ApplicationServer:atl-cs-001.litwareinc.com " | Remove-CsRgsWorkflow –Force

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsRgsWorkflow** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsRgsWorkflow"}

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
<td><p>指向要移除之工作流程的物件參考。將工作流程物件傳送到 <strong>Remove-CsRgsWorkflow</strong> 時，您可以省略 Instance 參數。</p>
<p>若要使用 Instance 參數，請使用類似下列的命令：</p>
<p>$x = Get-CsRgsWorkflow –Identity ApplicationServer:atl-cs-001.litwareinc.com /1987d3c2-4544-489d-bbe3-59f79f530a83</p>
<p>Remove-CsRgsWorkflow –Instance $x</p>
<p>請注意，使用 Instance 參數時，您一次只能移除一個工作流程。這表示物件參考 ($x) 不能包含多個工作流程物件。</p></td>
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
<td><p>強制移除工作流程。如果此參數存在，即使工作流程目前處於作用狀態，它仍然會被刪除而不會有警告。若未指定此參數，則系統會要求您確認是否要刪除所有作用中的工作流程。</p></td>
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

Microsoft.Rtc.Rgs.Management.WritableSettings.Workflow 物件。**Remove-CsRgsWorkflow** 接受管線傳送的回應群組工作流程物件執行個體。

## 傳回類型

**Remove-CsRgsWorkflow** 會刪除現有的 Microsoft.Rtc.Rgs.Management.WritableSettings.Workflow 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsRgsWorkflow](get-csrgsworkflow.md)  
[New-CsRgsWorkflow](new-csrgsworkflow.md)  
[Set-CsRgsWorkflow](set-csrgsworkflow.md)

