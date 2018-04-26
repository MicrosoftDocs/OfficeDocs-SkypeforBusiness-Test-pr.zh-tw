---
title: Get-CsPoolFabricState
TOCTitle: Get-CsPoolFabricState
ms:assetid: 9fe6cce5-4142-47b3-94ac-4cb8b94ec215
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ619188(v=OCS.15)
ms:contentKeyID: 49291830
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPoolFabricState

 

_**上次修改主題的時間：** 2015-03-09_

傳回 Lync Server 2013 集區的 Windows 虛擬環境狀態。Windows 虛擬環境是一項 Microsoft 技術，可用來建立高度可靠、可散發及可擴充的應用程式。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsPoolFabricState -PoolFqdn <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Type <All | MCUFactory | ConferenceDirectory | Routing | LYSS>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會傳回集區 atl-cs-001.litwareinc.com 的虛擬環境狀態。因為並未加上 Type 參數，所以將會傳回集區上所有服務的狀態資訊。

    Get-CsPoolFabricState -PoolFqdn "atl-cs-001.litwareinc.com"

## 範例 2

範例 2 會傳回集區 atl-cs-001.litwareinc.com 上的單一服務：MCU Factory 服務。若要這樣做，請加上 VerificationLevel 參數與參數值 "MCU"。

    Get-CsPoolFabricState -PoolFqdn "atl-cs-001.litwareinc.com" -Type MCU

## 詳細描述

**Get-CsPoolFabricState** Cmdlet 會傳回 Lync Server 2013 集區的 Windows 虛擬環境狀態。這包括下列任何 (或所有) 服務之 Windows 虛擬環境複本執行個體的資訊：MCU Factory、會議目錄、路由、 Lync Server Storage Service。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPoolFabricState"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Get-CsPoolFabricState** Cmdlet 所執行的功能。

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
<td><p><em>PoolFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>正在檢查的集區完整網域名稱。呼叫此 Cmdlet 時，您必須提供集區的 FQDN；例如：</p>
<p>-PoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p></td>
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
<td><p><em>Type</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.HADR.GetOcsPoolFabricStateCmdlet+FabricEnumerationType</p></td>
<td><p>指定要傳回的服務類型。允許的值為：</p>
<p>* All (傳回所有服務的資訊)</p>
<p>* MCUFactory (傳回 MCU Factory 服務的資訊)</p>
<p>* ConferenceDirectory (傳回會議目錄服務的資訊)</p>
<p>LYSS (傳回 Lync Server 存放服務的資訊)</p>
<p>每個命令只能指定一種類型。</p></td>
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

無。 **Get-CsPoolFabricState** Cmdlet 不支援管線傳送的輸入。

## 傳回類型

代表虛擬環境狀態的字串值。 **Get-CsPoolFabricState** Cmdlet 不會傳回物件。

