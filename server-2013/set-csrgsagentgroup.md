---
title: Set-CsRgsAgentGroup
TOCTitle: Set-CsRgsAgentGroup
ms:assetid: 48944530-29ec-4f5d-893f-37d3fd4aeb66
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425955(v=OCS.15)
ms:contentKeyID: 49290804
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsRgsAgentGroup

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的回應群組代理群組。代理群組是指派到回應群組佇列的代理集合。代理是指派以接聽導向到特定佇列來電的使用者。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsRgsAgentGroup -Instance <AgentGroup> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會修改回應群組代理群組 Help Desk (可在 ApplicationServer:atl-cs-001.litwareinc.com 服務上找到) 的 RoutingMethod 屬性。為達此目的，命令會先使用 **Get-CsRgsAgentGroup** Cmdlet 從 ApplicationServer:atl-cs-001.litwareinc.com 擷取 Help Desk 代理群組 (-Name "Help Desk")。然後再將該代理群組物件儲存在名為 $x 的變數中。

範例中的命令 2 會修改 RoutingMethod 內容的值。在範例的最後一個命令中，**Set-CsRgsAgentGroup** Cmdlet 可用來將這些變更寫入實際的 Help Desk 代理群組。

    $x = Get-CsRgsAgentGroup -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk"
    $x.RoutingMethod = "RoundRobin"
    Set-CsRgsAgentGroup -Instance $x

## 範例 2

範例 2 說明您可以如何變更指派給回應群組代理群組的通訊群組。作法是先使用 **Get-CsRgsAgentGroup** 傳回要修改的代理群組；在這個範例中為可在 ApplicationServer:atl-cs-001.litwareinc.com 服務上找到的 Help Desk 群組 (-Name "Help Desk ")。在 **Get-CsRgsAgentGroup** 傳回此群組之後，產生的物件會儲存在名為 $x 的變數中。

範例的第二個命令會將新值 (helpdesk@litwareinc.com) 指派給 DistributionGroupAddress 屬性。指派新值之後，**Set-CsRgsAgentGroup** 即可用來將變更寫入 ApplicationServer:atl-cs-001.litwareinc.com 上的 Help Desk 代理群組。

    $x = Get-CsRgsAgentGroup -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk"
    $x.DistributionGroupAddress = "helpdesk@litwareinc.com"
    Set-CsRgsAgentGroup -Instance $x

## 範例 3

範例 3 所示的命令會將新代理新增至回應群組代理群組 Help Desk。為達此目的，範例會先使用 **Get-CsRgsAgentGroup** 從 ApplicationServer:atl-cs-001.litwareinc.com 服務傳回 Help Desk 群組 (-Name "Help Desk")。然後再將擷取的物件儲存在名為 $x 的變數中。

第二個命令會使用新增方法將新代理加入 AgentsByUri 屬性；作法是指定新代理的 SIP 位址 ("sip:kenmyer@litwareinc.com")。命令 3 會使用 **Set-CsRgsAgentGroup** 將變更 (亦即加入新代理) 寫入 Help Desk 群組。請注意，如果您沒有呼叫 **Set-CsRgsAgentGroup**，則變更只會在記憶體中進行，而不會套用到實際的代理群組。

    $x = Get-CsRgsAgentGroup -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk"
    $x.AgentsByUri.Add("sip:kenmyer@litwareinc.com")
    Set-CsRgsAgentGroup -Instance $x

## 範例 4

範例 4 會從 ApplicationServer:atl-cs-001.litwareinc.com 服務上的回應群組代理群組 Help Desk 中移除代理。為達此目的，範例會先使用 **Get-CsRgsAgentGroup** 從 ApplicationServer:atl-cs-001.litwareinc.com 傳回 Help Desk 群組 (-Name "Help Desk")。然後再將擷取的代理群組物件儲存在名為 $x 的變數中。

擷取代理群組之後，您可以使用移除方法移除群組的代理 (含有 SIP 位址 "sip:kenmyer@litwareinc.com" 的代理)。接著命令 3 會呼叫 **Set-CsRgsAgentGroup**，以從群組寫入變更 (亦即移除代理)。如果您沒有呼叫 **Set-CsRgsAgentGroup**，則變更只會在記憶體中進行，而不會套用到實際的代理群組；只有呼叫 **Set-CsRgsAgentGroup**，才會移除代理。

    $x = Get-CsRgsAgentGroup -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk"
    $x.AgentsByUri.Remove("sip:kenmyer@litwareinc.com")
    Set-CsRgsAgentGroup -Instance $x

## 詳細描述

當某人撥打與回應群組應用程式相關聯的電話號碼時，服務會先判斷哪一個工作流程對應至所撥的號碼。系統會根據該工作流程組態，將來電路由傳送至一組互動語音回應 (IVR) 問題 (語音會詢問來電者一或多個類似「此問題是有關硬體支援或軟體支援？」等問題)。或者，來電可能會被放置在回應群組佇列中；來電者會被保留，直到指定的人員可接聽來電。被指定要接聽來電的人員就是所謂的代理，而集合中的代理，就是回應群組代理群組。代理群組與工作流程相關聯，而且會進一步和工作職責相關聯：服務台人員會分至 Help Desk 代理群組，客戶支援代理則會分至 Customer Support 代理群組。

使用 **New-CsRgsAgentGroup** Cmdlet 可建立新的代理群組。如果您必須在代理群組建立之後變更，請使用 **Set-RgsAgentGroup** Cmdlet；此外，這個 Cmdlet 可用來新增和移除群組的個別代理。請注意，**Set-CsRgsAgentGroup** 不會直接修改代理群組的屬性。如果您必須修改群組，您必須先建立該群組的物件參考；作法是呼叫 **Get-CsRgsAgentGroup** 擷取群組，然後將傳回的物件儲存在變數中。建立物件參考之後，請在記憶體中對群組屬性進行變更。完成修改之後，您必須呼叫 **Set-CsRgsAgentGroup**，將變更寫入實際的回應群組代理群組。如果您沒有呼叫 **Set-CsRgsAgentGroup**，則您的變更只會存在於記憶體中，且當您關閉 Windows PowerShell 或刪除物件參考變數時，變更就會消失。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsRgsAgentGroup** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsRgsAgentGroup"}

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
<td><p>要修改之回應群組代理群組的物件參考。物件參考通常是使用 <strong>Get-CsRgsAgentGroup</strong> Cmdlet 來擷取，並將傳回的值指派至變數；例如，此命令會將物件參考傳回至佇列 Help Desk 代理群組，並將該物件參考儲存在名為 $x 的變數中：</p>
<p>$x = Get-CsRgsAgentGroup -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name &quot;Help Desk &quot;</p>
<p></p></td>
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

Microsoft.Rtc.Rgs.Management.WritableSettings.AgentGroup 物件。**Set-CsRgsAgentGroup** 接受管線傳送的回應群組代理群組物件執行個體。

## 傳回類型

**Set-CsRgsAgentGroup** 不會傳回任何物件或值，而會修改現有的 Microsoft.Rtc.Rgs.Management.WritableSettings.AgentGroup 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsRgsAgentGroup](get-csrgsagentgroup.md)  
[New-CsRgsAgentGroup](new-csrgsagentgroup.md)  
[Remove-CsRgsAgentGroup](remove-csrgsagentgroup.md)

