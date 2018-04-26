---
title: Set-CsAVEdgeConfiguration
TOCTitle: Set-CsAVEdgeConfiguration
ms:assetid: b410164b-b47d-450c-8048-983cac4be624
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412869(v=OCS.15)
ms:contentKeyID: 49292059
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsAVEdgeConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

可讓您修改 A/V Edge 服務 電腦 (又稱為 A/V Edge Server) 的組態設定。A/V Edge Server 可讓內部使用者與外部使用者 (亦即未登入內部網路的使用者) 一起共用音訊和視訊資料，以及交換檔案與參與桌面期用工作階段。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsAVEdgeConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsAVEdgeConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-MaxBandwidthPerPortKb <UInt32>] [-MaxBandwidthPerUserKb <UInt32>] [-MaxTokenLifetime <TimeSpan>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

在範例 1 中，命令會修改全域 A/V Edge 組態設定的 MaxTokenLifetime 屬性。在此範例中，將權杖存留期上限設為 4 小時 (04 小時：00 分鐘：00 秒) 的 A/V Edge 組態設定。

    Set-CsAVEdgeConfiguration -Identity global -MaxTokenLifetime "04:00:00"

## 詳細描述

A/V Edge Server 提供一種方法，可穿過組織防火牆交換音訊和視訊流量。除此之外，這可讓使用者透過網際網路存取 Lync Server，然後與在防火牆內登入系統的使用者交換音訊和視訊資料。您可以在全域範圍、網站範圍和服務範圍指派 Edge Server 組態設定。這些組態設定讓系統管理員能夠進行諸如下列的事項：管理使用者驗證在必須更新之前的有效性期限，以及限制單一使用者或單一連接埠可以使用的頻寬量。

**Set-CsAVEdgeConfiguration** Cmdlet 提供方法，讓您修改目前組織中使用的 A/V Edge 組態設定。不過，除非 Microsoft 支援人員另有指示，建議系統管理員不要修改預設的 A/V Edge 設定。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsAVEdgeConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsAVEdgeConfiguration"}

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
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要修改的 A/V Edge 組態設定集合的唯一識別碼。若要修改全域集合，請使用下列語法：-Identity global。若要修改網站集合，則使用類似下列的語法：-Identity site:Redmond。您應使用如下的語法，提到在服務範圍設定的設定：-Identity service:EdgeServer:atl-cs-001.litwareinc.com。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>MediaRelaySettings 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxBandwidthPerPortKb</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>指出可配置給單一連接埠的頻寬上限，單位為 每秒 KB。頻寬上限可以設定為每秒介於 1 和 4294967296 (4096 GB) 之間的任何整數，預設值是 3000。</p></td>
</tr>
<tr class="even">
<td><p><em>MaxBandwidthPerUserKb</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>指出可配置給任何一名使用者的頻寬上限，單位為每秒 KB。頻寬上限可以設定為每秒介於 1 和 4294967296 (4096 GB) 之間的任何整數，預設值是 10000。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxTokenLifetime</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>驗證權杖到期必須更新之前，可以使用的時間長度上限。權杖存留期必須以下列格式表示：天數.小時數:分鐘數:秒數。例如，13 天必須以下列方式來表示：天數後方帶有一個句號 (.)，並使用分號 (:) 來分隔小時、分和秒：</p>
<p>13.00:00:00</p>
<p>預設值 8 小時必須表示為：</p>
<p>08:00:00</p>
<p>權杖存留期的下限是 1 分鐘 (00:01:00)，存留期上限是 180 天 (180.00:00:00)。</p>
<p></p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.Edge.MediaRelaySettings 物件。**Set-CsAVEdgeConfiguration** Cmdlet 接受媒體轉送設定物件管線傳送的輸入。

## 傳回類型

**Set-CsAVEdgeConfiguration** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.MediaRelaySettings 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsAVEdgeConfiguration](get-csavedgeconfiguration.md)  
[New-CsAVEdgeConfiguration](new-csavedgeconfiguration.md)  
[Remove-CsAVEdgeConfiguration](remove-csavedgeconfiguration.md)

