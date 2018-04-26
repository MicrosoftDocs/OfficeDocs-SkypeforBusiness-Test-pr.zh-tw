---
title: Set-CsEdgeServer
TOCTitle: Set-CsEdgeServer
ms:assetid: cbe140a4-8ce6-4e20-913b-b1ffb58e6698
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398859(v=OCS.15)
ms:contentKeyID: 49292332
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsEdgeServer

 

_**上次修改主題的時間：** 2015-03-09_

修改一或多部 Edge Server 的屬性值。Edge Server 可用於連接內部網路與網際網路。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsEdgeServer [-Identity <XdsGlobalRelativeIdentity>] [-AccessEdgeClientSipPort <UInt16>] [-AccessEdgeExternalSipPort <UInt16>] [-AccessEdgeInternalSipPort <UInt16>] [-Confirm [<SwitchParameter>]] [-DataPsomClientPort <UInt16>] [-DataPsomServerPort <UInt16>] [-Force <SwitchParameter>] [-MediaCommunicationPortCount <UInt16>] [-MediaCommunicationPortStart <UInt16>] [-MediaRelayAuthEdgePort <UInt16>] [-MediaRelayExternalTurnTcpPort <UInt16>] [-MediaRelayExternalTurnUdpPort <UInt16>] [-MediaRelayInternalTurnTcpPort <UInt16>] [-MediaRelayInternalTurnUdpPort <UInt16>] [-Registrar <String>] [-WhatIf [<SwitchParameter>]] [-XmppInternalPort <UInt16>] [-XmppListeningPort <UInt16>]

## 範例

## 範例 1

範例 1 所示的命令會修改 Edge Server "EdgeServer:atl-edge-001.litwareinc.com" 的內部和外部 SIP 連接埠。

    Set-CsEdgeServer -Identity "EdgeServer:atl-edge-001.litwareinc.com" -AccessEdgeInternalSipPort 5062 -AccessEdgeExternalSipPort 5062

## 範例 2

範例 2 會修改 Redmond 網站中所有 Edge Server 的內部和外部 SIP 連接埠。為達成此目的，命令會先使用 **Get-CsService** Cmdlet 搭配 EdgeServer 參數，以傳回組織目前使用的所有 Edge Server 集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 Redmond 網站中的 Edge Server (即 SiteId 屬性等於 site:Redmond 的伺服器)。接著將此篩選後的集合管線傳送到 **For-Each-Object** Cmdlet。該 Cmdlet 會對集合中的每一部伺服器執行 **Set-CsEdgeServer** Cmdlet，以變更指派給 AccessInternalSipPort 和 AccessExternalSipPort 屬性的值。

    Get-CsService -EdgeServer | Where-Object {$_.SiteId -eq "site:Redmond"} | ForEach-Object {Set-CsEdgeServer -Identity $_.Identity -AccessEdgeInternalSipPort 5062 -AccessEdgeExternalSipPort 5062}

## 詳細描述

和外部世界的連線能力 (也就是使用網際網路) 是 Lync Server 的重要環節。若缺乏這類型的連線能力，使用者就必須要登入內部網路才能存取 Lync Server。這會使得在異地工作的使用者難以使用軟體，也會使不具有網域帳戶的使用者無法參與會議。同樣地，若無法和組織的外部連線，使用者便無法和同盟協力廠商或具有公用立即訊息系統 (如 Yahoo\!、AOL 或 MSN) 之帳戶的人員交換立即訊息。

Edge Server 可用來提供內部網路和網際網路間的連線。**Set-CsEdgeServer** Cmdlet 可讓您修改 Edge Server 的組態設定。這項工作的內容主要是和變更用來傳輸網路流量的連接埠號碼相關。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsEdgeServer** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsEdgeServer"}

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
<td><p><em>AccessEdgeClientSipPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>用來傳輸 Edge Server 和用戶端裝置間 SIP 通訊的連接埠。初始值會在拓撲產生器中設定，但可透過為此參數指定新值加以變更。</p></td>
</tr>
<tr class="even">
<td><p><em>AccessEdgeExternalSipPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>用來傳輸外部 SIP 流量的連接埠。預設值為 5061。</p></td>
</tr>
<tr class="odd">
<td><p><em>AccessEdgeInternalSipPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>用來傳輸內部 SIP 流量的連接埠。預設值為 5061。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>DataPsomClientPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>用來傳輸 Edge Server 和用戶端裝置間持續性共用物件模型 (PSOM) 通訊的連接埠。初始值會在拓撲產生器中設定，但可透過為此參數指定新值加以變更。</p></td>
</tr>
<tr class="even">
<td><p><em>DataPsomServerPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>用來傳輸 Edge Server 和其他伺服器間 PSOM 通訊的連接埠。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要修改的 Edge Server 服務位置。例如：-Identity &quot;EdgeServer:atl-edge-001.litwareinc.com&quot;。</p>
<p>請注意，當您在指定 Edge Server 時，可以省略首碼 &quot;EdgeServer:&quot;。例如：-Identity &quot;atl-cs-001.litwareinc.com&quot;。</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>MediaCommunicationPortCount</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>針對媒體通訊在外部 Edge 上配置的連接埠總數。預設值為 10000。</p></td>
</tr>
<tr class="even">
<td><p><em>MediaCommunicationPortStart</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>外部 Edge 上之媒體通訊的起始連接埠號碼。預設值為 50000。</p></td>
</tr>
<tr class="odd">
<td><p><em>MediaRelayAuthEdgePort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>用於媒體轉送驗證的連接埠。預設值為 5062。</p></td>
</tr>
<tr class="even">
<td><p><em>MediaRelayExternalTurnTcpPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>用來透過傳輸控制通訊協定 (TCP) 傳輸外部媒體轉送流量的連接埠。如果您的 Edge Server 具有單一 IP 位址，預設值為 444。如果您的 Edge Server 具有多個 IP 位址，則預設值為 443。這些值會在拓撲產生器中初始設定，但可透過為此參數指定新值加以變更。</p></td>
</tr>
<tr class="odd">
<td><p><em>MediaRelayExternalTurnUdpPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>用來透過使用者資料包通訊協定 (UDP) 傳輸外部媒體轉送流量的連接埠。預設值為 3478。</p></td>
</tr>
<tr class="even">
<td><p><em>MediaRelayInternalTurnTcpPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>用來透過 TCP 傳輸內部媒體轉送流量的連接埠。預設值為 443。</p></td>
</tr>
<tr class="odd">
<td><p><em>MediaRelayInternalTurnUdpPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>用來透過 UDP 傳輸內部媒體轉送流量的連接埠。預設值為 3478。</p></td>
</tr>
<tr class="even">
<td><p><em>Registrar</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要和 Edge Server 建立關聯的登錄器服務位置。例如：-Registrar &quot;Registrar:atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
<tr class="even">
<td><p><em>XmppInternalPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>用於內部 XMPP 流量的連接埠。Extensible Messaging and Presence Protocol (XMPP) 是使用 XML 交換訊息的開放標準通訊協定。允許的合作夥伴是指 IM 和目前狀態提供者，其使用者可與您的 Lync Server 使用者交換立即訊息和目前狀態資訊。預設值為 5098。</p></td>
</tr>
<tr class="odd">
<td><p><em>XmppListeningPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>用於 XMPP 流量的聆聽連接埠。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Set-CsEdgeServer** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Set-CsEdgeServer** Cmdlet 不會傳回任何物件或值，而會修改現有的 Microsoft.Rtc.Management.Xds.DisplayEdgeServer 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsService](get-csservice.md)

