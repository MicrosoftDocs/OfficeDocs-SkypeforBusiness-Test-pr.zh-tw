---
title: Remove-CsServerApplication
TOCTitle: Remove-CsServerApplication
ms:assetid: 55325d8c-9c67-4e88-868d-ce62bc11322e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398366(v=OCS.15)
ms:contentKeyID: 49290950
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsServerApplication

 

_**上次修改主題的時間：** 2015-03-09_

移除現有的伺服器應用程式。伺服器應用程式是由 Lync Server 代管的應用程式。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsServerApplication -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 中，伺服器應用程式的 Identity 為 service:EdgeServer:atl-edge-001.litwareinc.com/EdgeMonitor 會遭到移除。因為 Identity 必須是唯一的，所以此命令永遠只會刪除一個應用程式。

    Remove-CsServerApplication -Identity "service:EdgeServer:atl-edge-001.litwareinc.com/EdgeMonitor"

## 範例 2

範例 2 會移除所有非關鍵的伺服器應用程式。為了執行此工作，命令會先呼叫 **Get-CsServerApplication** Cmdlet，以傳回組織目前所使用之所有伺服器應用程式的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會挑選所有 Critical 屬性等於 False 的應用程式。接著將篩選後的集合管線傳送到 **Remove-CsServerApplication** Cmdlet，以刪除集合中的每一個項目。

    Get-CsServerApplication | Where-Object {$_.Critical -eq $False} | Remove-CsServerApplication

## 範例 3

範例 3 會刪除所有已設定用於 EdgeServer:atl-cs-001.litwareinc.com 服務的伺服器應用程式。為達成此目的，會使用 **Get-CsServerApplication** Cmdlet 搭配 Filter 參數；篩選值 "service:EdgeServer:atl-cs-001.litwareinc.com/\*" 可傳回 Identity 開頭為 "service:EdgeServer:atl-cs-001.litwareinc.com/" 字元的所有應用程式。然後，此集合會管線傳送到 **Remove-CsServerApplication** Cmdlet，以刪除 EdgeServer:atl-cs-001.litwareinc.com 中的每個應用程式。

    Get-CsServerApplication -Filter "service:EdgeServer:atl-cs-001.litwareinc.com/*" | Remove-CsServerApplication

## 詳細描述

伺服器應用程式是指在 Lync Server 下執行的個別程式。**Remove-CsServerApplication** Cmdlet 讓系統管理員移除做為 Lync Server 一部分而執行的任何應用程式。請注意，刪除伺服器應用程式與解除安裝該應用程式是兩回事。在執行 **Remove-CsServerApplication** Cmdlet 後，該應用程式不再於 Lync Server 之下執行。但軟體本身並未解除安裝，執行 **New-CsServerApplication** Cmdlet 即可重新啟用該應用程式。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsServerApplication** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsServerApplication }

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
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要移除之伺服器應用程式的唯一識別碼。伺服器應用程式 Identity 由託管應用程式的服務和應用程式名稱組成。例如，名為 QoEAgent 的伺服器應用程式可能會有如下的 Identity：service:Registrar:atl-cs-001.litwareinc.com/QoEAgent。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.ServerApplication.Application 物件。**Remove-CsServerApplication** Cmdlet 接受管線傳送的伺服器應用程式物件執行個體。

## 傳回類型

**Remove-CsServerApplication** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.WritableConfig.Settings.ServerApplication.Application 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsServerApplication](get-csserverapplication.md)  
[New-CsServerApplication](new-csserverapplication.md)  
[Set-CsServerApplication](set-csserverapplication.md)

