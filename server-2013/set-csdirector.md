---
title: Set-CsDirector
TOCTitle: Set-CsDirector
ms:assetid: 74eb6f17-812f-47df-84ee-fa6e42990f2e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398565(v=OCS.15)
ms:contentKeyID: 49291344
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsDirector

 

_**上次修改主題的時間：** 2015-03-09_

修改一或多個 Director 的屬性。Director 只可用於驗證使用者要求，而無法代管裝載使用者帳戶。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsDirector [-Identity <XdsGlobalRelativeIdentity>] [-ArchivingServer <String>] [-Confirm [<SwitchParameter>]] [-EdgeServer <String>] [-Force <SwitchParameter>] [-MirrorMonitoringDatabase <String>] [-MonitoringDatabase <String>] [-MonitoringServer <String>] [-SipHealthPort <UInt16>] [-SipPort <UInt16>] [-SipServerTcpPort <UInt16>] [-WebPort <UInt16>] [-WebServer <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會變更與 Director Director:atl-cs-001.litwareinc.com 相關聯的 封存伺服器。在此範例中，封存伺服器 會切換到 ArchivingServer:dublin-cs-001.litwareinc.com。

    Set-CsDirector -Identity "Director:atl-cs-001.litwareinc.com" -ArchivingServer "ArchivingServer:dublin-cs-001.litwareinc.com"

## 範例 2

範例 2 會變更組織目前正在使用之所有 Director 的 SIP 連接埠。為達成此目的，命令會先使用 **Get-CsService** Cmdlet 並搭配 Director 參數，以傳回組織中所有 Director 的集合。然後，此集合會管線傳送到 **ForEach-Object**。接著 **ForEach-Object** Cmdlet 會對集合中的每個網站執行 **Set-CsDirector** Cmdlet，以將 SipPort 屬性值變更為 5072。

    Get-CsService -Director | ForEach-Object {Set-CsDirector -Identity $_.Identity -SipPort 5072}

## 詳細描述

Director 會驗證使用者並回應使用者要求，不需實際主控使用者帳戶。Director 通常用於允許透過 Edge Server 對網路進行外部存取的組織。在該情況下，Director 不僅有助於減少前端伺服器的壓力 (藉由處理驗證要求)，也可協助保護內部網路不受拒絕服務的攻擊和其他惡意流量。當中央網站部署了多個前端伺服器時，Director 也很有用。在該情況下，Director 會接收所有使用者要求，然後將這些要求傳送到適當的伺服器集區。這也有助於減少前端伺服器的壓力。

**Set-CsDirector** Cmdlet 可讓您修改組織中目前使用中之任何 Director 的屬性值。這包含變更與 Director 相關聯的 封存伺服器 或 Edge Server，或者變更用來傳送與接收 SIP 流量的連接埠。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsDirector** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsDirector"}

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
<td><p><em>ArchivingServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要與 Director 相關聯之 封存伺服器 的服務位置。例如：-ArchivingServer &quot;ArchivingServer:atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>EdgeServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要與 Director 相關聯之 Edge Server 的服務位置。例如：-EdgeServer &quot;EdgeServer:atl-edge-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏顯示當執行命令時可能發生的任何非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要修改的 Director 服務位置。例如：-Identity &quot;Director:atl-cs-001.litwareinc.com&quot;。</p>
<p>請注意，您可以省略首碼 &quot;Director&quot;：指定 Director 時。例如：-Identity &quot;atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>MirrorMonitoringDatabase</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要與 Director 建立關聯之鏡像監控資料庫的服務位置。</p></td>
</tr>
<tr class="odd">
<td><p><em>MonitoringDatabase</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要與 Director 建立關聯之監控資料庫的服務位置。</p></td>
</tr>
<tr class="even">
<td><p><em>MonitoringServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要與 Director 相關聯之 監控伺服器 的服務位置。例如：-MonitoringServer &quot;MonitoringServer:atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>SipHealthPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>用於監視伺服器狀況的連接埠。</p></td>
</tr>
<tr class="even">
<td><p><em>SipPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>用於工作階段初始通訊協定 (SIP) 流量的連接埠。</p></td>
</tr>
<tr class="odd">
<td><p><em>SipServerTcpPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>SIP 聆聽連接埠。預設值為 5060。</p></td>
</tr>
<tr class="even">
<td><p><em>WebPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>用於與 Web 服務 進行通訊的連接埠。</p></td>
</tr>
<tr class="odd">
<td><p><em>WebServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>與 Director 相關聯之伺服器的 Web 服務 位置。例如：-WebServer &quot;WebServer:atl-cs-001.litwareinc.com&quot;</p></td>
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

無。**Set-CsDirector** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Set-CsDirector** Cmdlet 不會傳回任何物件或值，而會修改現有的 Microsoft.Rtc.Management.Xds.DisplayDirector 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsService](get-csservice.md)

