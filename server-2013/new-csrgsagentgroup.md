---
title: New-CsRgsAgentGroup
TOCTitle: New-CsRgsAgentGroup
ms:assetid: faaf46f9-1063-4d64-a36f-872e657cd869
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413065(v=OCS.15)
ms:contentKeyID: 49292884
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsRgsAgentGroup

 

_**上次修改主題的時間：** 2015-03-09_

建立新的回應群組代理群組。代理群組是指派給回應群組佇列的代理集合。代理是指派以接聽導向到特定佇列來電的使用者。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsRgsAgentGroup -Name <String> -Parent <RgsIdentity> [-AgentAlertTime <Int16>] [-AgentsByUri <Collection>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-DistributionGroupAddress <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-ParticipationPolicy <Informal | Formal>] [-RoutingMethod <LongestIdle | Serial | Parallel | RoundRobin | Attendant>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會建立名為 Help Desk Group 的新回應群組代理群組，這個新的群組位於 ApplicationServer:atl-cs-001.litwareinc.com 服務。為了建立群組，命令會呼叫 **New-CsRgsAgentGroup** 搭配 Parent 與 Name 參數。這個範例中未指定任何其他的群組，表示群組將使用所有預設的屬性值。因為沒有代理指派給此群組，會自動切斷任何轉接給新代理群組的來電。

    New-CsRgsAgentGroup -Parent service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk Group"

## 範例 2

範例 2 中會建立新的回應群組代理群組，同時會將一對代理指派給該群組。為達此目的，命令會呼叫 **New-CsRgsAgentGroup** 搭配 Parent 與 Name 參數。此外，這個範例也會加入參數 AgentsByUri 搭配 "sip:kenmyer@litwareinc.com","sip:pilarackerman@litwareinc.com" 參數值。這個值是以逗號分隔的清單，包含了要新增至代理群組的 SIP 位址。

    New-CsRgsAgentGroup -Parent service: ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk Group" -AgentsByUri "sip:kenmyer@litwareinc.com","sip:pilarackerman@litwareinc.com"

## 詳細描述

當某人撥打與回應群組應用程式相關聯的電話號碼時，應用程式會先判斷哪一個工作流程對應至所撥的號碼。系統會根據該工作流程組態，將來電路由傳送至一組互動語音回應 (IVR) 問題 (語音會詢問來電者一或多個類似「此問題是有關硬體支援或軟體支援？」等問題)。或者，來電可能會被放置在回應群組佇列中；來電者會被保留，直到指定的人員可接聽來電。被指定要接聽來電的人員就是所謂的代理，而集合中的代理，就是回應群組代理群組。代理群組與佇列相關聯，甚至和類似的工作職責相關聯：服務台人員會分至 Help Desk 代理群組，客戶支援代理則會分至 Customer Support 代理群組。

如果有多個群組指派給佇列，則回應群組應用程式開始時會撥打已指派至該佇列的第一個群組中的所有線上代理。如果這些代理都未接聽，則應用程式會開始撥打給已指派至佇列的下一個群組中的所有線上代理。

使用 **New-CsRgsAgentGroup** Cmdlet 可建立新的代理群組。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsRgsAgentGroup** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

    Get-CsAdminRole | Where-Object  {$_.Cmdlets -match "New-CsRgsAgentGroup"}

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
<td><p><em>Name</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>指派給代理群組的唯一名稱。Parent 屬性和 Name 屬性的組合可讓您唯一識別代理群組，而不必參考群組的全域唯一識別碼 (GUID)。</p></td>
</tr>
<tr class="even">
<td><p><em>Parent</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>主控新代理群組的服務。例如：-Parent &quot;service:ApplicationServer:atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>AgentAlertTime</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int16</p></td>
<td><p>表示一段時間 (單位為秒)，當來電過了這段時間都無人接聽，便會自動路由傳送給下一個代理。AgentAlertTime 可設為介於 10 到 600 秒 (10 分鐘) (含) 的任何整數值。預設值為 20 秒。<strong>注意：</strong>[代理警示時間] 設定不得超過 180 秒。如果超過 180 秒，由於 SIP 交易計時器達到其最長等候時間，因此用戶端應用程式會拒絕來電。若要避免這種情況，請將 [警示時間] 值設為小於 180 秒。</p></td>
</tr>
<tr class="even">
<td><p><em>AgentsByUri</em></p></td>
<td><p>選用</p></td>
<td><p>System.Collections.ObjectModel.Collection</p></td>
<td><p>可讓您將代理個別新增至代理群組中。新的代理由 SIP 位址來識別。</p>
<p>請注意，您只能選取已為 Enterprise Voice 啟用的使用者。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓系統管理員提供代理群組的其他解釋性資訊。例如，描述可能包含當群組未接到預期的電話時應向誰連絡的資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>DistributionGroupAddress</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您將通訊群組的所有成員新增到代理群組。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="even">
<td><p><em>ParticipationPolicy</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.ParticipationPolicy</p></td>
<td><p>指出是否需要有代理才能正式登入系統，以接聽預定由該群組接聽的電話。如果 ParticipationPolicy 設為 Informal (預設值)，則不需要登入。如果 ParticipationPolicy 設為 Formal，則需要登入。</p></td>
</tr>
<tr class="odd">
<td><p><em>RoutingMethod</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.RoutingMethod</p></td>
<td><p>指定用於將新來電路由傳送至代理的方法。RoutingMethod 必須設為下列其中一個值：</p>
<p>LongestIdle – 來電會路由傳送給閒置最久的 (也就是未涉入 Lync 活動) 代理。</p>
<p>RoundRobin – 來電會路由傳送給清單上的下一個代理。</p>
<p>Serial – 來電一律轉接給清單上的第一個代理，且只有在此人無法接聽或在分配的時間內未接聽時，才會轉接給其他代理。</p>
<p>Parallel – 來電會同時路由傳送給所有代理，但目前狀態指出為電話中或無法接聽的代理除外。</p>
<p>Attendant – 來電會同時路由傳送給所有代理，即使該代理的目前狀態指出為電話中或無法接聽。唯一的例外是當代理將使用者的目前狀態設為「請勿打擾」。</p>
<p>預設的路由方法為 Parallel。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>描述執行命令後的結果，但無須實際執行命令。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsRgsAgentGroup** 不接受管線傳送的輸入。

## 傳回類型

**New-CsRgsAgentGroup** 會建立 Microsoft.Rtc.Rgs.Management.WritableSettings.AgentGroup 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsRgsAgentGroup](get-csrgsagentgroup.md)  
[Remove-CsRgsAgentGroup](remove-csrgsagentgroup.md)  
[Set-CsRgsAgentGroup](set-csrgsagentgroup.md)

