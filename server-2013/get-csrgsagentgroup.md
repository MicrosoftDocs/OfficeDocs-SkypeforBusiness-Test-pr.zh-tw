---
title: Get-CsRgsAgentGroup
TOCTitle: Get-CsRgsAgentGroup
ms:assetid: 2e3c7004-9017-48a4-91d8-5c271fb8a1ab
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425793(v=OCS.15)
ms:contentKeyID: 49290462
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsRgsAgentGroup

 

_**上次修改主題的時間：** 2015-03-09_

傳回設定供組織使用之回應群組代理群組的資訊。代理群組是指派給回應群組佇列的代理集合。代理是指派以接聽導向到佇列來電的使用者。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsRgsAgentGroup [-Identity <RgsIdentity>] [-Name <String>] [-Owner <RgsIdentity>] [-ShowAll <SwitchParameter>]

## 範例

## 範例 1

範例 1 會傳回設定供組織使用的所有回應群組代理群組。作法是不使用任何參數而直接呼叫 **Get-CsRgsAgentGroup**。

    Get-CsRgsAgentGroup

## 範例 2

範例 2 所示的命令會傳回所有設定用於 ApplicationServer:atl-cs-001.litwareinc.com 服務的回應群組代理群組。

    Get-CsRgsAgentGroup -Identity service:ApplicationServer:atl-cs-001.litwareinc.com

## 範例 3

範例 3 所示的命令會傳回單一回應群組代理群組：在 ApplicationServer:atl-cs-001.litwareinc.com 服務上找到之名為 Help Desk 的群組。

    Get-CsRgsAgentGroup -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk"

## 範例 4

範例 4 中，如果 ApplicationServer:atl-cs-001.litwareinc.com 服務所有的回應群組代理群組，使用的是循環配置資源路由方法，則會傳回該服務上這些代理群組的資訊。為達此目的，命令會先使用 **Get-CsRgsAgentGroup** 傳回 ApplicationServer:atl-cs-001.litwareinc.com 上所有代理群組的集合。然後再將該集合管線傳送到 **Where-Object** Cmdlet，以選取 RoutingMethod 屬性等於 "RoundRobin" 的群組。

    Get-CsRgsAgentGroup -Identity service:ApplicationServer:atl-cs-001.litwareinc.com | Where-Object {$_.RoutingMethod -eq "RoundRobin"}

## 範例 5

範例 5 中使用的命令是範例 3 中所用之命令的變化，但在此狀況下會傳回 ApplicationServer:atl-cs-001.litwareinc.com 服務不使用循環配置資源路由方法的所有回應群組代理群組的資訊。為達此目的，命令會先呼叫 **Get-CsRgsAgentGroup** 傳回 ApplicationServer:atl-cs-001.litwareinc.com 所有代理群組的集合。然後再將該集合管線傳送到 **Where-Object** Cmdlet，以選取 RoutingMethod 屬性等於 "RoundRobin" 的代理群組。

    Get-CsRgsAgentGroup -Identity Service:ApplicationServer:atl-cs-001.litwareinc.com | Where-Object {$_.RoutingMethod -ne "RoundRobin"}

## 詳細描述

當某人撥打與 回應群組應用程式 相關聯的電話號碼時，應用程式會先判斷所撥號碼對應的工作流程。系統會根據該工作流程組態，將來電路由傳送至一組互動語音回應 (IVR) 問題 (語音會詢問來電者一或多個類似「此問題是有關硬體支援或軟體支援？」等問題)。或者，來電可能會被放置在回應群組佇列中；來電者會被保留，直到指定的人員可接聽來電。被指定要接聽來電的人員就是所謂的代理，而集合中的代理，就是回應群組代理群組。代理群組與工作流程相關聯，甚至和類似的工作職責相關聯：服務台人員會分至 Help Desk 代理群組，客戶支援代理則會分至 Customer Support 代理群組。

**Get-CsRgsAgentGroup** Cmdlet 能讓您傳回組織目前所使用之回應群組代理群組的資訊，這包括已指派給每個代理群組的使用者的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsRgsAgentGroup** Cmdlet：RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsRgsAgentGroup"}

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
<td><p>表示主控回應群組代理群組的服務 Identity，或是代理群組本身的完整 Identity。如果您有指定服務識別 (例如 service:ApplicationServer:atl-cs-001.litwareinc.com)，則該服務主控的所有代理群組都會被擷取。如果您有指定群組的識別，則只會傳回所指定的代理群組。請注意，代理群組的 Identity 是由服務 Identity 後面加上全域唯一識別碼 (GUID) 所組成，例如：service:ApplicationServer:atl-cs-001.litwareinc.com/1987d3c2-4544-489d-bbe3-59f79f530a83.</p>
<p>還有另一種方法可傳回單一群組，就是指定服務 Identity，然後再包含後面加上代理群組名稱的 Name 參數。這可讓您不必知道指派給群組的 GUID 為何，就能擷取特定的代理群組。</p>
<p>呼叫時若未使用任何參數，<strong>Get-CsRgsAgentGroup</strong> 會傳回設定供組織使用的所有代理群組。</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>建立群組時給予代理群組的唯一名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>Owner</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>「擁有」代理群組之集區的完整網域名稱。擁有者集區識別碼和代理群組的集區識別碼通常一樣。然而，如果需要暫時移動群組 (可能在災害復原程序中)，則集區識別碼將會變更。不過，擁有者識別碼會繼續指向原始集區。</p></td>
</tr>
<tr class="even">
<td><p><em>ShowAll</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定此參數，會顯示所有回應群組代理群組，包括擁有者集區識別碼與集區識別碼不同的那些群組。根據預設，Get-CsRgsAgentGroup 只會傳回擁有者集區識別碼與集區識別碼相同之代理群組的資訊。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

字串。**Get-CsRgsAgentGroup** 會接受代表回應群組代理群組之 Identity 的字串值。

## 傳回類型

**Get-CsRgsAgentGroup** 會傳回 Microsoft.Rtc.Rgs.Management.WritableSettings.AgentGroup 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsRgsAgentGroup](new-csrgsagentgroup.md)  
[Remove-CsRgsAgentGroup](remove-csrgsagentgroup.md)  
[Set-CsRgsAgentGroup](set-csrgsagentgroup.md)

