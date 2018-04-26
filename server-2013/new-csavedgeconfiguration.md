---
title: New-CsAVEdgeConfiguration
TOCTitle: New-CsAVEdgeConfiguration
ms:assetid: b6bcf426-9037-4679-99dc-e94bfb8f72a6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412884(v=OCS.15)
ms:contentKeyID: 49292083
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsAVEdgeConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

建立新的組態設定集合，供 A/V Edge 服務 電腦 (又稱為 A/V Edge Server) 使用。A/V Edge Server 可讓內部使用者與外部使用者 (亦即未登入內部網路的使用者) 一起共用音訊和視訊資料。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsAVEdgeConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-MaxBandwidthPerPortKb <UInt32>] [-MaxBandwidthPerUserKb <UInt32>] [-MaxTokenLifetime <TimeSpan>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會為 Redmond 網站建立新的 A/V Edge 組態設定集合。在此範例中，MaxTokenLifetime 內容設為 4 小時 (04 小時：00 分鐘：00 秒) 的 A/V Edge 組態設定。

    New-CsAVEdgeConfiguration -Identity site:Redmond -MaxTokenLifetime "04:00:00"

## 範例 2

範例 2 示範如何在記憶體中建立新的 A/V Edge 組態設定集合，然後將這些虛擬設定轉換為實際的 A/V Edge 設定集合。為達此目的，範例中的第一個命令為 Redmond 網站建立新的設定集合；加上 InMemory 參數以確保這些設定只建立在記憶體中，且不會立即套用到 Redmond 網站。(由於這些設定僅存在於記憶體中，因此必須儲存在變數中；在此範例中，變數的名稱為 $x)。

第二個命令會將 MaxTokenLifetime 屬性值設為 4 小時 (04 小時：00 分鐘：00 秒)。第三個命令接著會使用 **Set-CsAVEdgeConfiguration** Cmdlet，將 $x 中所儲存的設定套用到 Redmond 網站。

    $x = New-CsAVEdgeConfiguration -Identity site:Redmond -InMemory
    $x.MaxTokenLifetime = "04:00:00"
    Set-CsAVEdgeConfiguration -Instance $x

## 詳細描述

A/V Edge Server 提供一種方法，可穿過組織防火牆交換音訊和視訊流量。除此之外，這可讓使用者透過網際網路存取 Lync Server，然後與在防火牆內登入系統的使用者交換音訊和視訊資料。您可以在全域範圍、網站範圍和服務範圍指派 Edge Server 組態設定。A/V Edge 組態設定可讓系統管理員管理使用者驗證在必須更新之前可以維持多久有效時間，以及限制單一使用者或單一連接埠可以使用的頻寬量。

**New-CsAVEdgeConfiguration** Cmdlet 讓您可以在網站或服務範圍建立新的 A/V Edge 組態設定集合。但如上述，也可以在全域範圍設定 A/V Edge 設定。不過，您無法在全域範圍建立新集合。

請注意，任何特定網站或服務最多只能裝載一個 A/V Edge 組態設定集合。如果 Redmond 網站已經裝載 A/V Edge 設定，您便無法建立 Identity 為 site:Redmond 的新集合。

除非 Microsoft 支援人員另有指示，建議您不要變更預設的 A/V Edge 組態設定。因為如此，您可能不需要建立網站或服務的設定新集合。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsAVEdgeConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsAVEdgeConfiguration"}

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
<td><p>要建立的 A/V Edge 組態設定集合的唯一識別碼。若要建立設定集合以套用在網站範圍，則使用類似下列的語法：-Identity site:Redmond。(請注意，如果已經有 A/V Edge 組態設定集合套用到 Redmond 網站，這個命令就會失敗)。設定於服務範圍的設定應使用類似如下的語法：-Identity service:EdgeServer:atl-cs-001.litwareinc.com。</p></td>
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
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
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

無。**New-CsAVEdgeConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

建立 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.MediaRelaySettings 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsAVEdgeConfiguration](get-csavedgeconfiguration.md)  
[Remove-CsAVEdgeConfiguration](remove-csavedgeconfiguration.md)  
[Set-CsAVEdgeConfiguration](set-csavedgeconfiguration.md)

