---
title: Get-CsRgsWorkflow
TOCTitle: Get-CsRgsWorkflow
ms:assetid: 2ae2e10b-65ac-40f9-96a2-5adb01e8a69d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425766(v=OCS.15)
ms:contentKeyID: 49290406
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsRgsWorkflow

 

_**上次修改主題的時間：** 2015-03-09_

傳回回應群組工作流程的資訊。工作流程可決定回應群組應用程式接聽電話時所要採取的動作。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsRgsWorkflow [-Identity <RgsIdentity>] [-Name <String>] [-Owner <RgsIdentity>] [-ShowAll <SwitchParameter>]

## 範例

## 範例 1

範例 1 會傳回已設定供組織使用之所有工作流程的資訊。作法是不使用任何參數而直接呼叫 **Get-CsRgsWorkflow**。

    Get-CsRgsWorkflow

## 範例 2

範例 2 會傳回在 ApplicationServer:atl-cs-001.litwareinc.com 服務上找到之所有 回應群組應用程式 工作流程的資訊。

    Get-CsRgsWorkflow -Identity service:ApplicationServer:atl-cs-001.litwareinc.com

## 範例 3

範例 3 所示的命令會顯示在 ApplicationServer:atl-cs-001.litwareinc.com 服務上找到的每個回應群組工作流程之 DefaultAction 屬性的詳細資訊。為達此目的，會先使用 **Get-CsRgsWorkflow** 傳回在 ApplicationServer:atl-cs-001.litwareinc.com 上找到的所有工作流程資訊。然後再將該資訊管線傳送至 **Select-Object** Cmdlet，以「展開」儲存在 DefaultAction 屬性中的值。當您展開 DefaultAction 的值後，便可看到儲存在 DefaultAction 屬性中之內嵌物件的個別屬性。

    Get-CsRgsWorkflow -Identity service:ApplicationServer:atl-cs-001.litwareinc.com | Select-Object -ExpandProperty DefaultAction

## 範例 4

範例 4 會傳回單一回應群組工作流程的資訊：在 ApplicationServer:atl-cs-001.litwareinc.com 上發現名為 European Sales Supports 的工作流程。

    Get-CsRgsWorkflow -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "European Sales Support"

## 範例 5

範例 5 所示的命令會傳回所有使用美國英文做為主要語言之回應群組工作流程的資訊。為達此目的，命令會先呼叫 **Get-CsRgsWorkflow** 傳回在 ApplicationServer:atl-cs-001.litwareinc.com 服務上找到的所有工作流程集合。然後會將該集合管線傳送到 **Where-Object** Cmdlet，以選取 Language 屬性等於英文 (美國) (en-US) 的工作流程。

    Get-CsRgsWorkflow -Identity service:ApplicationServer:atl-cs-001.litwareinc.com | Where-Object {$_.Language -eq "en-Us"}

## 範例 6

範例 6 會傳回 ApplicationServer:atl-cs-001.litwareinc.com 上所有 CustomMusicOnHoldFile 屬性已設為 Null 值的工作流程 (換句話說，命令會傳回尚未獲指派自訂音樂的工作流程的資訊)。為達此目的，命令會先使用 **Get-CsRgsWorkflow** 傳回在 ApplicationServer:atl-cs-001.litwareinc.com 服務上找到的所有工作流程集合。然後再將傳回的資料管線傳送到 **Where-Object**，以選取 CustomMusicOnHoldFile 屬性等於 Null 值的項目。

    Get-CsRgsWorkflow service:ApplicationServer:atl-cs-001.litwareinc.com | Where-Object {$_.CustomMusicOnHoldFile -eq $Null}

## 詳細描述

工作流程或許是 回應群組應用程式 中的關鍵元素。每個工作流程只會與一個電話號碼產生關聯，當有人撥打該號碼時，工作流程便會決定如何處理這通電話。例如，系統會將電話路由傳送至一系列的互動語音回應 (IVR) 問題，這些問題會提示來電者輸入額外的資訊 (「硬體支援請按 1)。軟體支援請按 2。」)或者，來電可能會被放在佇列中並保留來電者，直到代理可接聽來電。代理是否可接聽電話的狀態，也是由工作流程指定的：工作流程可用來設定營業時間 (一星期的哪幾天和哪些時段會有代理接聽電話) 與假日 (代理無法接聽電話的日子)。

**Get-CsRgsWorkflow** Cmdlet 能讓您傳回設定供組織使用之工作流程的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsRgsWorkflow** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsRgsWorkflow"}

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
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>表示主控回應群組工作流程的服務識別，或工作流程本身的完整識別。如果您有指定服務識別 (例如 service:ApplicationServer:atl-cs-001.litwareinc.com)，則會傳回該服務主控的所有回應群組工作流程。如果您有指定工作流程的 Identity，則只會傳回那一個回應群組工作流程。請注意，工作流程的識別是由服務識別後面加上全域唯一識別碼 (GUID) 所組成，例如：service:ApplicationServer:atl-cs-001.litwareinc.com /1987d3c2-4544-489d-bbe3-59f79f530a83。</p>
<p>還有另一種方法可傳回單一回應群組工作流程，就是指定服務 Identity，然後再包含後面加上工作流程名稱的 Name 參數。這可讓您不必知道指派給工作流程的 GUID 為何，就能擷取特定的工作流程。</p>
<p>呼叫時若未使用任何參數，<strong>Get-CsRgsWorkflow</strong> 會傳回設定供組織使用的所有工作流程。</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>建立回應群組工作流程時給予該工作流程的唯一名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>Owner</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>「擁有」工作流程之集區的完整網域名稱。擁有者集區識別碼和工作流程的集區識別碼通常一樣。然而，如果需要暫時移動工作流程 (可能在災害復原程序中)，則集區識別碼將會變更。不過，擁有者識別碼會繼續指向原始集區。</p></td>
</tr>
<tr class="even">
<td><p><em>ShowAll</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定此參數，會顯示所有回應群組工作流程，包括擁有者集區識別碼與集區識別碼不同的那些工作流程。根據預設，Get-CsRgsWorkflow 只會傳回擁有者與父系集區相同之工作流程的資訊。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsRgsWorkflow** 不接受管線傳送的輸入。

## 傳回類型

**Get-CsRgsWorkflow** 會傳回 Microsoft.Rtc.Rgs.Management.WritableSettings.Workflow 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsRgsWorkflow](new-csrgsworkflow.md)  
[Remove-CsRgsWorkflow](remove-csrgsworkflow.md)  
[Set-CsRgsWorkflow](set-csrgsworkflow.md)

