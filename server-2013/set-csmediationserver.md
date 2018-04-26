---
title: Set-CsMediationServer
TOCTitle: Set-CsMediationServer
ms:assetid: 13efdd9d-ba26-4c93-b0b9-b6e4739bb630
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398213(v=OCS.15)
ms:contentKeyID: 49290168
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsMediationServer

 

_**上次修改主題的時間：** 2015-03-09_

可讓您修改一或多個中繼伺服器的屬性。中繼伺服器可用於路由內部 Enterprise Voice 基礎結構與公用交換電話網路 (PSTN) 閘道或 SIP 主幹之間的流量。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsMediationServer [-Identity <XdsGlobalRelativeIdentity>] [-AudioPortCount <UInt16>] [-AudioPortStart <UInt16>] [-Confirm [<SwitchParameter>]] [-EdgeServer <String>] [-Force <SwitchParameter>] [-Registrar <String>] [-SipClientTcpPort <UInt16>] [-SipClientTlsPort <UInt16>] [-SipServerPort <UInt16>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將 中繼伺服器 MediationServer:atl-cs-001.litwareinc.com 的 SIP 閘道 TCP 聆聽連接埠設為 5072。變更連接埠之後，您需要重新啟動 Lync Server 中繼服務。

    Set-CsMediationServer -Identity "MediationServer:atl-cs-001.litwareinc.com" -SipClientTcpPort 5072

## 範例 2

範例 2 會設定 中繼伺服器 MediationServer:atl-cs-001.litwareinc.com 的音訊連接埠設定。在此範例中，開始音訊連接埠設為 60000，而配置給音訊的連接埠總數為 1000。

    Set-CsMediationServer -Identity "MediationServer:atl-cs-001.litwareinc.com" -AudioPortStart 60000 -AudioPortCount 1000

## 詳細描述

中繼伺服器扮演內部 Enterprise Voice 組態與 PSTN 閘道、IP-PBX 或 SIP 主幹之間的橋接器，因此可以讓您的 Enterprise Voice 使用者 (使用 Voice over Internet Protocol 裝置者) 與使用標準地面通訊電話或行動電話的人員進行通訊。**Set-CsMediationServer** Cmdlet 提供一種方法，讓您變更現有的中繼伺服器。特別是您可以修改用與用戶端裝置、前端伺服器與對等閘道進行通訊的連接埠。如有必要，亦可使用 **Set-CsMediationServer** Cmdlet，讓中繼伺服器與新的登錄器或新的 Edge Server 產生關聯。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsMediationServer** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsMediationServer"}

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
<td><p><em>AudioPortCount</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>配置給傳送和接收音訊流量的連接埠總數。要開放的實際連接埠將以針對 AudioPortStart 設定的值開始，然後繼續加上針對 AudioPortCount 指定的連接埠數目。例如，如果 AudioPortStart 設為 60000，而 AudioPortCount 設為 100，則連接埠 60000 至 60099 (含) 將會用於音訊流量。</p>
<p>轉接單一音訊通話至少需要七個媒體連接埠：</p>
<p>兩個閘道連接埠。即時傳輸通訊協定 (RTP) 流量需要一個連接埠，即時傳輸控制通訊協定 (RTCP) 流量也需要一個連接埠。</p>
<p>兩個使用者資料包通訊協定 (UDP) 轉送連接埠：一個用於 RTP 流量，另一個用於 RTCP 流量。</p>
<p>一個傳輸控制通訊協定 (TCP) 轉送連接埠。單一 TCP 轉送連接埠可以同時處理 RTP 與 RTCP 流量。</p>
<p>每一個網路介面有兩個本機連接埠：一個用於 RTP 流量，另一個用於 RTCP 流量</p></td>
</tr>
<tr class="even">
<td><p><em>AudioPortStart</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>配置給傳送和接收音訊流量之連接埠範圍中的第一個連接埠。例如：–AudioPortStart 60000。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>EdgeServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要與中繼伺服器相關聯之 Edge Server 的服務識別碼。例如：-EdgeServer &quot;EdgeServer:atl-edge-001.litwareinc.com&quot;。</p></td>
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
<td><p>要修改的 中繼伺服器 服務位置。例如：-Identity &quot;MediationServer:atl-cs-001.litwareinc.com&quot;。</p>
<p>請注意，指定中繼伺服器時，您可以省略首碼 &quot;MediationServer:&quot;。例如：-Identity &quot;atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>Registrar</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要與中繼伺服器相關聯之登錄器的服務識別碼。例如：-Registrar &quot;Registrar:atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>SipClientTcpPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>以 TCP 與閘道對等實體通訊時使用的聆聽連接埠。預設不會定義 TCP 連接埠；不過，建立 PSTN 閘道時會自動建立連接埠號碼 5068 的 TCP 連接埠。如果您變更 SipClientTcpPort，則需要重新啟動中繼伺服器服務，才會實際使用新的連接埠。</p></td>
</tr>
<tr class="odd">
<td><p><em>SipClientTlsPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>以傳輸層安全性 (TLS) 通訊協定與閘道對等實體通訊時使用的聆聽連接埠。根據預設，SipClientTlsPort 設定為使用連接埠 5067。如果您變更 SipClientTlsPort，則需要重新啟動中繼伺服器服務，才會實際使用新的連接埠。</p></td>
</tr>
<tr class="even">
<td><p><em>SipServerPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>用於與前端伺服器通訊的聆聽連接埠。根據預設，SipServerPort 設定為使用連接埠 5070。如果您變更 SipServerPort，則需要重新啟動中繼伺服器服務，才會實際使用新的連接埠。</p></td>
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

無。**Set-CsMediationServer** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Set-CsMediationServer** Cmdlet 不會傳回任何物件或值，而會修改現有的 Microsoft.Rtc.Management.Xds.DisplayMediationServer 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsService](get-csservice.md)

