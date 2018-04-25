---
title: Set-CsConferenceServer
TOCTitle: Set-CsConferenceServer
ms:assetid: 90f9f1f1-0029-4f97-a8f4-719523cfad56
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398738(v=OCS.15)
ms:contentKeyID: 49291661
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsConferenceServer

 

_**上次修改主題的時間：** 2015-03-09_

修改 A/V 會議伺服器 (又稱為會議伺服器) 的屬性。會議伺服器可提供會議所需的音訊和視訊 (A/V) 功能。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsConferenceServer [-Identity <XdsGlobalRelativeIdentity>] [-AppSharingPortCount <UInt16>] [-AppSharingPortStart <UInt16>] [-AppSharingSipPort <UInt16>] [-AudioPortCount <UInt16>] [-AudioPortStart <UInt16>] [-AudioVideoSipPort <UInt16>] [-Confirm [<SwitchParameter>]] [-DataPsomPort <UInt16>] [-EdgeServer <String>] [-Force <SwitchParameter>] [-ImSipPort <UInt16>] [-MeetingPsomPort <UInt16>] [-PhoneSipPort <UInt16>] [-VideoPortCount <UInt16>] [-VideoPortStart <UInt16>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會修改會議伺服器 ConferencingServer:atl-cs-001.litwareinc.com 的立即訊息 SIP 連接埠。在此範例中，連接埠會變更為 5075。

    Set-CsConferenceServer -Identity "ConferencingServer:atl-cs-001.litwareinc.com" -ImSipPort 5075

## 範例 2

範例 2 是範例 1 所示命令的變化；但此範例會針對組織中所有會議伺服器，變更立即訊息 SIP 連接埠。為達成此目的，命令會先使用 **Get-CsService** Cmdlet 並搭配 ConferencingServer 參數，以傳回目前所使用之所有會議伺服器的集合。然後，此集合會管線傳送到 **ForEach-Object** Cmdlet，以對集合中的每部伺服器執行 **Set-CsConferenceServer** Cmdlet，並將 ImSipPort 設為 5075。

    Get-CsService -ConferencingServer | ForEach-Object {Set-CsConferenceServer -Identity $_.Identity -ImSipPort 5075}

## 詳細描述

會議伺服器 (又稱為 A/V 會議伺服器) 是用來提供會議的音訊和視訊功能。**Set-CsConferenceServer** Cmdlet 可用於修改這些伺服器的屬性；明確地說，您可以指定像是音訊流量、視訊流量和應用程式共用等使用的連接埠。您也可以使用 **Set-CsConferenceServer** Cmdlet，將指定的伺服器與 Edge Server 或封存伺服器產生關聯。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsConferenceServer** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsConferenceServer"}

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
<td><p><em>AppSharingPortCount</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>配置用於應用程式共用的連接埠總數。要開啟的實際連接埠會從設定給 AppSharingPortStart 的值開始算起，延續到指定給 AppSharingPortCount 的連接埠數目。例如，如果 AppSharingPortStart 設為 60000，而 AppSharingPortCount 設為 100，則連接埠 60000 至 60099 將會用於應用程式共用。</p></td>
</tr>
<tr class="even">
<td><p><em>AppSharingPortStart</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>配置用於應用程式共用之媒體連接埠範圍中的第一個連接埠。例如：–AppSharingPortStart 60000。</p></td>
</tr>
<tr class="odd">
<td><p><em>AppSharingSipPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>用來聆聽應用程式共用要求的 SIP 連接埠。可以使用 AppSharingPortStart 和 AppSharingPortCount 設定應用程式共用實際使用的連接埠。</p></td>
</tr>
<tr class="even">
<td><p><em>AudioPortCount</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>配置來傳送與接收音訊流量的連接埠總數。要開啟的實際連接埠會從設定給 AudioPortStart 的值開始算起，延續到指定給 AudioPortCount 的連接埠數目。例如，如果 AudioPortStart 設為 60000，而 AudioPortCount 設為 100，則連接埠 60000 至 60099 將會用於音訊流量。</p></td>
</tr>
<tr class="odd">
<td><p><em>AudioPortStart</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>配置來傳送與接收音訊流量之媒體連接埠範圍中的第一個連接埠。例如：–AudioPortStart 60000。</p></td>
</tr>
<tr class="even">
<td><p><em>AudioVideoSipPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>用來傾聽音訊和視訊服務之傳入要求的 SIP 連接埠。可以使用 AudioPortCount、AudioPortStart、VideoPortCount 和 VideoPortStart 設定音訊和視訊流量實際使用的連接埠。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>DataPsomPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>持續性共用物件模型 (PSOM) 通訊協定使用的資料連接埠。</p></td>
</tr>
<tr class="odd">
<td><p><em>EdgeServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要和會議伺服器建立關聯的 Edge Server 服務位置。例如：-EdgeServer &quot;EdgeServer:atl-edge-001.litwareinc.com&quot;。</p></td>
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
<td><p>要修改之會議伺服器的服務位置。例如：-Identity &quot;ConferencingServer:atl-cs-001.litwareinc.com&quot;。</p>
<p>請注意，您可以省略首碼 &quot;ConferencingServer&quot;：指定會議伺服器時。例如：-Identity &quot;atl-cs-001.litwareinc.com&quot;。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>ImSipPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>用於立即訊息流量的連接埠。</p></td>
</tr>
<tr class="odd">
<td><p><em>MeetingPsomPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>用於持續性共用物件模型 (PSOM) 通訊協定 (一個用於會議的 Microsoft 通訊協定) 的連接埠。</p></td>
</tr>
<tr class="even">
<td><p><em>PhoneSipPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>用於電話語音流量的連接埠。</p></td>
</tr>
<tr class="odd">
<td><p><em>VideoPortCount</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>配置來傳送與接收視訊流量的連接埠總數。要開啟的實際連接埠會從設定給 VideoPortStart 的值開始算起，延續到指定給 VideoPortCount 的連接埠數目。例如，如果 VideoPortStart 設為 60000，而 VideoPortCount 設為 100，則連接埠 60000 至 60099 將會用於視訊流量。</p></td>
</tr>
<tr class="even">
<td><p><em>VideoPortStart</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>配置來傳送與接收視訊流量之連接埠範圍中的第一個連接埠。例如：–VideoPortStart 60000。</p></td>
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

無。**Set-CsConferenceServer** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Set-CsConferenceServer** Cmdlet 不會傳回任何物件或值，而會修改現有的 Microsoft.Rtc.Management.Xds.DisplayConferenceServer 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsConferencingConfiguration](get-csconferencingconfiguration.md)  
[Get-CsService](get-csservice.md)

