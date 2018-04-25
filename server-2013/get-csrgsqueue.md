---
title: Get-CsRgsQueue
TOCTitle: Get-CsRgsQueue
ms:assetid: a2e786b7-5096-4011-8108-2b56ae768c1d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412759(v=OCS.15)
ms:contentKeyID: 49291859
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsRgsQueue

 

_**上次修改主題的時間：** 2015-03-09_

擷取組織所使用之回應群組佇列的資訊。回應群組應用程式會將來電放入佇列加以保留，直到回應群組代理可接聽來電為止。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsRgsQueue [-Identity <RgsIdentity>] [-Name <String>] [-Owner <RgsIdentity>] [-ShowAll <SwitchParameter>]

## 範例

## 範例 1

範例 1 顯示的命令會傳回設定供組織使用之所有回應群組佇列的資訊。作法是不使用任何參數而直接呼叫 **Get-CsRgsQueue**。

    Get-CsRgsQueue

## 範例 2

範例 2 所示的命令會傳回位於 ApplicationServer:atl-cs-001.litwareinc.com 服務的所有回應群組佇列。

    Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com

## 範例 3

範例 3 會傳回單一回應群組佇列的資訊：位於 ApplicationServer:atl-cs-001.litwareinc.com 服務上，名為 "Help Desk" 的佇列。

    Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk"

## 範例 4

範例 4 所示的命令會顯示在 ApplicationServer:atl-cs-001.litwareinc.com 服務上找到的每一個回應群組佇列的 TimeoutAction 屬性詳細資訊。為達此目的，會先使用 **Get-CsRgsQueue** 傳回在 ApplicationServer:atl-cs-001.litwareinc.com 上找到的所有佇列資訊。,然後再將該資訊管線傳送至 **Select-Object** Cmdlet，以「展開」TimeoutAction 內容中儲存的值。當您展開 TimeoutAction 內容時，即可看到內嵌物件中構成內容值的個別內容：Prompt、TargetQuestion、Target、TargetQueueID 與 TargetUri。

    Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com | Select-Object -ExpandProperty TimeoutAction

## 範例 5

範例 5 會傳回在 ApplicationServer:atl-cs-001.litwareinc.com 上，OverflowCandidate 屬性設定為 NewestCall 的所有回應群組佇列相關資訊。為達此目的，命令會先使用 **Get-CsRgsQueue** 傳回在指定服務上找到之所有回應群組佇列的集合。然後再將該集合管線傳送到 **Where-Object** Cmdlet，以選取 OverflowCandidate 屬性等於 "NewestCall" 的佇列。

    Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com | Where-Object {$_.OverflowCandidate -eq "NewestCall"}

## 詳細描述

如果某人撥打與 回應群組應用程式 相關聯的電話號碼，通常會發生下列兩件事的其中之一：來電會被轉接至一個問題，而來電者必須回答才能繼續 (例如，「硬體支援請按 1；軟體支援請按 2」)，或來電會被放置在佇列中，直到回應群組代理可接聽來電。

回應群組應用程式 可讓您建立與不同工作流程和不同回應群組代理群組相關聯的多個佇列，而不是所有來電者都使用單一佇列。依序表示佇列可分別回應事件，例如指定的來電號碼被同步保留在佇列中，或以指定的秒數保留來電者。

**Get-CsRgsQueue** Cmdlet 提供您傳回用於組織的回應群組佇列資訊的方法。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsRgsQueue** Cmdlet：RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsRgsQueue"}

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
<td><p>代表主控回應群組佇列的服務識別，或佇列本身的完整識別。如果您有指定服務識別 (例如 service:ApplicationServer:atl-cs-001.litwareinc.com)，則該服務主控的所有回應群組佇列都會被傳回。如果您指定佇列的識別，則只有指定的回應群組佇列會被傳回。請注意，佇列的識別由服務識別後面加上全域唯一識別碼 (GUID) 所組成，例如：service:ApplicationServer:atl-cs-001.litwareinc.com /1987d3c2-4544-489d-bbe3-59f79f530a83。</p>
<p>還有另一種方法可傳回單一回應群組佇列，就是指定服務識別，然後再加上 Name 參數和佇列名稱。這可讓您不必知道指派給佇列的 GUID 為何，就能擷取特定的回應群組佇列。</p>
<p>呼叫若未使用任何參數，<strong>Get-CsRgsQueue</strong> 會傳回設定供組織使用的所有回應群組佇列。</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>建立佇列時給予回應群組佇列的唯一名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>Owner</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>「擁有」佇列之集區的完整網域名稱。擁有者集區識別碼和佇列的集區識別碼通常一樣。然而，如果需要暫時移動佇列 (可能在災害復原程序中)，則集區識別碼將會變更。不過，擁有者識別碼會繼續指向原始集區。</p></td>
</tr>
<tr class="even">
<td><p><em>ShowAll</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定此參數，會顯示所有回應群組佇列，包括擁有者集區識別碼與集區識別碼不同的那些佇列。根據預設，Get-CsRgsQueue 只會傳回擁有者集區識別碼與集區識別碼相同之佇列的資訊。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

字串。**Get-CsRgsQueue** 接受字串值，代表回應群組佇列的 Identity。

## 傳回類型

**Get-CsRgsQueue** 會傳回 Microsoft.Rtc.Rgs.Management.WritableSettings.Queue 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsRgsQueue](new-csrgsqueue.md)  
[Remove-CsRgsQueue](remove-csrgsqueue.md)  
[Set-CsRgsQueue](set-csrgsqueue.md)

