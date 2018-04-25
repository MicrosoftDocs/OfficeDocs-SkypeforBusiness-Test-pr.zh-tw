---
title: Set-CsApplicationServer
TOCTitle: Set-CsApplicationServer
ms:assetid: 74b3f941-df06-4fde-9487-eba081233723
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398562(v=OCS.15)
ms:contentKeyID: 49291320
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsApplicationServer

 

_**上次修改主題的時間：** 2015-03-09_

可讓您修改一或多部執行應用程式服務的組態屬性。這些伺服器 (又稱為應用程式伺服器) 代管許多軟體程式，例如使用 Microsoft Unified Communications Managed API (UCMA) 集所開發的通話駐留應用程式。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsApplicationServer [-Identity <XdsGlobalRelativeIdentity>] [-ApplicationDatabase <String>] [-AppSharingPortCount <UInt16>] [-AppSharingPortStart <UInt16>] [-AtsSipPort <UInt16>] [-AudioPortCount <UInt16>] [-AudioPortStart <UInt16>] [-CaaSipPort <UInt16>] [-CasSipPort <UInt16>] [-Confirm [<SwitchParameter>]] [-CpsSipPort <UInt16>] [-Force <SwitchParameter>] [-PdpSipPort <UInt16>] [-PdpTurnPort <UInt16>] [-Registrar <String>] [-RgsSipPort <UInt16>] [-RgsWcfMtlsPort <UInt16>] [-VideoPortCount <UInt16>] [-VideoPortStart <UInt16>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將應用程式伺服器 ApplicationServer:atl-cs-001.litwareinc.com 上 會議宣告應用程式 的 SIP 連接埠設為 5074。

    Set-CsApplicationServer -Identity "ApplicationServer:atl-cs-001.litwareinc.com" -CasSipPort 5074 

## 範例 2

範例 2 會設定 ApplicationServer:atl-cs-001.litwareinc.com 應用程式伺服器的音訊連接埠。在此範例中，開始音訊連接埠設為 49500，而總共預留了 5500 個連接埠供音訊流量使用。

    Set-CsApplicationServer -Identity "ApplicationServer:atl-cs-001.litwareinc.com" -AudioPortStart 49500 -AudioPortCount 5500 

## 範例 3

範例 3 中，會將組織內所有應用程式伺服器之會議宣告應用程式的 SIP 連接埠設為 5074。為達成此目的，命令會先使用 **Get-CsService** Cmdlet，以傳回目前所使用之所有應用程式伺服器的集合。然後，此集合會管線傳送到 **ForEach-Object** Cmdlet，這會針對集合中的每個伺服器來使用 **Set-CsApplicationServer** Cmdlet，以將會議宣告應用程式 SIP 連接埠設為 5074。

    Get-CsService -ApplicationServer | ForEach-Object {Set-CsApplicationServer -Identity $_.Identity -CasSipPort 5074} 

## 詳細描述

應用程式服務主控幾個不屬於核心伺服器元件的 Lync Server 程式；這些程式包括回應群組應用程式、會議服務員應用程式以及會議宣告應用程式。應用程式服務會採用這些程式，並將這些程式完全整合到 Lync Server 環境中。

**Set-CsApplicationServer** Cmdlet 可讓系統管理員修改其組織中部署之任何 (或所有) 應用程式伺服器的組態設定。例如，您可以修改音訊、視訊或應用程式共用流量所使用的連接埠，或是為個別應用程式 (如 會議服務員應用程式 或 會議宣告應用程式) 使用的連接埠指派新值。請注意，只要您變更連接埠，就必須重新啟動對應的服務。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsApplicationServer** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsApplicationServer"}

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
<td><p><em>ApplicationDatabase</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>應用程式資料庫 的服務位置。例如：-ApplicationDatabase &quot;ApplicationDatabase:atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>AppSharingPortCount</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>配置給應用程式共用的連接埠總數。要開放的實際連接埠將以針對 AppSharingPortStart 設定的值開始，然後繼續加上針對 AppSharingPortCount 指定的連接埠數目。例如，如果 AppSharingPortStart 設為 60000，而 AppSharingPortCount 設為 100，則連接埠 60000 至 60099 將會用於應用程式共用。</p></td>
</tr>
<tr class="odd">
<td><p><em>AppSharingPortStart</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>配置給應用程式共用的連接埠範圍中的第一個連接埠。例如：–AppSharingPortStart 60000。</p></td>
</tr>
<tr class="even">
<td><p><em>AtsSipPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>用於音訊測試服務的通訊埠。</p></td>
</tr>
<tr class="odd">
<td><p><em>AudioPortCount</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>配置給傳送和接收音訊流量的連接埠總數。要開放的實際連接埠將以針對 AudioPortStart 設定的值開始，然後繼續加上針對 AudioPortCount 指定的連接埠數目。例如，如果 AudioPortStart 設為 60000，而 AudioPortCount 設為 100，則連接埠 60000 至 60099 將會用於音訊流量。</p></td>
</tr>
<tr class="even">
<td><p><em>AudioPortStart</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>配置給傳送和接收音訊流量之連接埠範圍中的第一個連接埠。例如：–AudioPortStart 60000。</p></td>
</tr>
<tr class="odd">
<td><p><em>CaaSipPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>會議服務員應用程式 使用的 SIP 連接埠，當使用者連線到撥入式會議時會使用該連接埠。</p></td>
</tr>
<tr class="even">
<td><p><em>CasSipPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>會議宣告應用程式 使用的 SIP 連接埠，用於在會議期間播放宣告 (例如，「Ken Myer 現在要離開」)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>CpsSipPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>通話駐留服務使用的 SIP 連接埠。通話駐留服務可讓您保留某個電話的通話，然後從不同電話擷取該通來電。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏顯示當執行命令時可能發生的任何非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要修改之應用程式伺服器的服務位置。例如：-Identity &quot;ApplicationServer:atl-cs-001.litwareinc.com&quot;。</p>
<p>請注意，您可以省略首碼 &quot;ApplicationServer&quot;：指定應用程式伺服器時。例如：-Identity &quot;atl-cs-001.litwareinc.com&quot;。</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>PdpSipPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>原則決定點 伺服器所使用的 SIP 連接埠。原則決定點 伺服器是用於頻寬管理。</p></td>
</tr>
<tr class="even">
<td><p><em>PdpTurnPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>轉換 原則決定點 伺服器使用的流量連接埠。</p></td>
</tr>
<tr class="odd">
<td><p><em>Registrar</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>與 原則決定點 伺服器相關聯之登錄器的完整網域名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>RgsSipPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>回應群組應用程式 所使用的 SIP 連接埠。回應群組應用程式 會提供一種方式，將來電導向至特定一組人員，例如組織的支援小組。</p></td>
</tr>
<tr class="odd">
<td><p><em>RgsWcfMtlsPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>回應群組應用程式 所使用之 Windows Communication Foundation (WCF) 相互傳輸層安全性 (MTLS) 流量使用的連接埠。</p></td>
</tr>
<tr class="even">
<td><p><em>VideoPortCount</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>配置給傳送和接收視訊流量的連接埠總數。要開放的實際連接埠將以針對 VideoPortStart 設定的值開始，然後繼續加上針對 VideoPortCount 指定的連接埠數目。例如，如果 VideoPortStart 設為 60000，而 VideoPortCount 設為 100，則連接埠 60000 至 60099 將會用於視訊流量。</p></td>
</tr>
<tr class="odd">
<td><p><em>VideoPortStart</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>配置給傳送和接收視訊流量之連接埠範圍中的第一個連接埠。例如 –VideoPortStart 60000。</p></td>
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

無。**Set-CsApplicationServer** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Set-CsApplicationServer** Cmdlet 不會傳回任何值或物件，而會修改現有的 Microsoft.Rtc.Management.Xds.DisplayApplicationServer 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsServerApplication](get-csserverapplication.md)

