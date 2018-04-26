---
title: Remove-CsRgsAgentGroup
TOCTitle: Remove-CsRgsAgentGroup
ms:assetid: dc185da9-0ae0-4f89-8ef8-7cb680d5dc51
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398969(v=OCS.15)
ms:contentKeyID: 49292521
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsRgsAgentGroup

 

_**上次修改主題的時間：** 2015-03-09_

移除現有的回應群組代理群組。代理群組是指派給回應群組佇列的代理集合。代理是指派以接聽導向到特定佇列來電的使用者。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsRgsAgentGroup -Instance <AgentGroup> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會刪除所有設定用於 ApplicationServer:atl-cs-001.litwareinc.com 服務的回應群組代理群組。為達此目的，命令會先使用 **Get-CsRgsAgentGroup** 傳回 ApplicationServer:atl-cs-001.litwareinc.com 的所有代理群組。然後，那些群組會傳送到 **Remove-CsRgsAgentGroup** Cmdlet，並由此 Cmdlet 移除。

    Get-CsRgsAgentGroup -Identity service:ApplicationServer:atl-cs-001.litwareinc.com | Remove-CsRgsAgentGroup

## 範例 2

在範例 2 中，單一回應群組代理群組會被刪除：名為 Help Desk 的群組。為達此目的，會先使用 **Get-CsRgsAgentGroup** 從 ApplicationServer:atl-cs-001.litwareinc.com 傳回 Help Desk 代理群組 (-Name "Help Desk")。接著會將這個群組傳送到 **Remove-CsRgsAgentGroup**，這會將群組從服務中移除。

    Get-CsRgsAgentGroup -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk" | Remove-CsRgsAgentGroup

## 範例 3

範例 3 會刪除 ApplicationServer:atl-cs-001.litwareinc.com 中所有未使用循環配置資源路由方法的回應群組代理群組。為達此目的，命令會先呼叫 **Get-CsRgsAgentGroup** 傳回所有在 ApplicationServer:atl-cs-001.litwareinc.com 服務上找到的代理群組集合。然後再將該集合管線傳送到 **Where-Object** Cmdlet，以選取 RoutingMethod 屬性不等於 (-ne) RoundRobin 的群組。接著將篩選後的集合管線傳送到 **Remove-CsRgsAgentGroup**，以刪除該集合中的每個項目。

    Get-CsRgsAgentGroup -Identity service:ApplicationServer:atl-cs-001.litwareinc.com | Where-Object {$_.RoutingMethod -ne "RoundRobin"} | Remove-CsRgsAgentGroup

## 詳細描述

當某人撥打與回應群組應用程式相關聯的電話號碼時，服務會先判斷哪一個工作流程對應至所撥的號碼。系統會根據該工作流程組態，將來電路由傳送至一組互動語音回應 (IVR) 問題 (語音會詢問來電者一或多個類似「此問題是有關硬體支援或軟體支援？」等問題)。或者，來電可能會被放置在回應群組佇列中；來電者會被保留，直到有人員接聽來電。被指定要接聽來電的人員就是所謂的代理，而一組集中的代理就是回應群組代理群組。代理群組與工作流程相關聯，並進一步與類似的工作責任產生關聯；例如，服務台人員會分組到 Help Desk 代理群組，客戶支援代理則會分組到 Customer Support 代理群組。

使用 **New-CsRgsAgentGroup** Cmdlet 可建立新的代理群組。如果必須刪除代理群組，只可呼叫 **Remove-CsRgsAgentGroup** Cmdlet。請注意，此 Cmdlet 會刪除整個群組，以及該群組中所有的代理。如果您只要移除群組中的單一代理，請改用 **Set-CsRgsAgentGroup** Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsRgsAgentGroup** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsRgsAgentGroup"}

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
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.AgentGroup</p></td>
<td><p>指向要移除之代理群組的物件參考。將工作流程物件傳送到 <strong>Remove-CsRgsAgentGroup</strong> 時，您可以省略 Instance 參數。</p>
<p>若要使用 Instance 參數，請使用類似下列的命令：</p>
<p>$x = Get-CsRgsAgentGroup –Identity ApplicationServer:atl-cs-001.litwareinc.com /1987d3c2-4544-489d-bbe3-59f79f530a83</p>
<p>Remove-CsRgsAgentGroup –Instance $x</p>
<p>請注意，使用 Instance 參數時，您一次只能移除一個代理群組。這表示物件參考 ($x) 不能包含多個代理群組物件。</p></td>
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
<td><p>強制移除代理群組。如果設定此參數，即使代理群組由作用中工作流程使用，它仍然會被刪除而不會有警告。如果沒有設定此參數，則系統會要求您確認是否刪除目前正由作用中工作流程使用的所有代理群組。</p></td>
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

Microsoft.Rtc.Rgs.Management.WritableSettings.AgentGroup 物件。**Remove-CsRgsAgentGroup** 接受管線傳送的回應群組代理群組物件執行個體。

## 傳回類型

**Remove-CsRgsAgentGroup** 會刪除現有的 Microsoft.Rtc.Rgs.Management.WritableSettings.AgentGroup 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsRgsAgentGroup](get-csrgsagentgroup.md)  
[New-CsRgsAgentGroup](new-csrgsagentgroup.md)  
[Set-CsRgsAgentGroup](set-csrgsagentgroup.md)

