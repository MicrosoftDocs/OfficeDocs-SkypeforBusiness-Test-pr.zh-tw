---
title: Remove-CsAVEdgeConfiguration
TOCTitle: Remove-CsAVEdgeConfiguration
ms:assetid: 98bceec5-ed9d-4574-b6bf-f51e0f414ca7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398786(v=OCS.15)
ms:contentKeyID: 49291770
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsAVEdgeConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

可讓您移除目前套用到 Access Edge Service 電腦 (又稱為 A/V Edge Server) 的組態設定集合。A/V Edge Server 可讓內部使用者與外部使用者 (亦即未登入內部網路的使用者) 一起共用音訊和視訊資料。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsAVEdgeConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會移除其 Identity 為 site:Redmond 的 A/V Edge 組態設定。在移除設定之後，Redmond 網站中的 A/V Edge Server 將由全域組態設定控管。

    Remove-CsAVEdgeConfiguration -Identity site:Redmond

## 範例 2

範例 2 會移除所有已在服務範圍套用的 A/V Edge 組態設定。為達成此目的，命令會先呼叫 **Get-CsAVEdgeConfiguration** Cmdlet 並搭配 Filter 參數；篩選值 "service:\*" 可確保只會傳回在服務範圍設定的設定。然後再將篩選後的集合管線傳送到 **Remove-CsAVEdgeConfiguration** Cmdlet，以刪除集合中的每個項目。

    Get-CsAVEdgeConfiguration -Filter "service:*" | Remove-CsAVEdgeConfiguration

## 範例 3

範例 3 所示的命令會刪除 MaxBandwidthPerUserKB 屬性值小於每秒 5,000 KB 的所有 A/V Edge 組態設定。為了執行此工作，命令會先呼叫不含任何額外參數的 **Get-CsAVEdgeConfiguration** Cmdlet，以傳回組織目前所使用之所有 A/V Edge 設定的集合。然後再將此集合管線傳送至 **Where-Object** Cmdlet，這會只選取 MaxBandwidthPerUserKB 屬性小於 5000 的設定。接著將篩選後的集合管線傳送至 **Remove-CsAVEdgeConfiguration** Cmdlet，以刪除該集合中的每個項目。

    Get-CsAVEdgeConfiguration | Where-Object {$_.MaxBandwidthPerUserKB -lt 5000} | Remove-CsAVEdgeConfiguration

## 詳細描述

A/V Edge Server 提供一種方法，可穿過組織防火牆交換音訊和視訊流量。除此之外，這可讓使用者透過網際網路存取 Lync Server，然後與在防火牆內登入系統的使用者交換音訊和視訊資料。您可以在全域範圍、網站範圍和服務範圍指派 Edge Server 組態設定。A/V Edge 組態設定可讓系統管理員執行這類工作：管理使用者驗證在必須更新前的有效時間，以及限制單一使用者或單一連接埠可以使用的頻寬量。

**Remove-CsAVEdgeConfiguration** Cmdlet 可讓您刪除已套用至網站或服務範圍的 A/V Edge 組態設定。此 Cmdlet 也可以對全域設定來執行；然而，這樣並不會刪除那些全域設定，而是會將全域集合內包含的屬性重設為預設值。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsAVEdgeConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsAVEdgeConfiguration"}

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
<td><p>要移除之 A/V Edge 組態設定集合的唯一識別碼。若要移除全域集合，請使用下列語法：-Identity global。(如先前所述，這樣並無法移除全域設定，而只會將屬性重設為預設值)。若要移除網站集合，請使用類似下列的語法：-Identity site:Redmond。您應使用如下的語法，提到在服務範圍設定的設定：</p>
<p>-Identity service:EdgeServer:atl-cs-001.litwareinc.com</p>
<p>在指定原則 Identity 時不能使用萬用字元。</p></td>
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
<td><p>隱藏顯示當執行命令時可能發生的任何非嚴重錯誤訊息。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.Edge.MediaRelaySettings 物件。**Remove-CsAVEdgeConfiguration** Cmdlet 接受管線傳送的媒體轉送設定物件輸入。這些物件是藉由執行 **Get-CsAVEdgeConfiguration** Cmdlet 來擷取的。

## 傳回類型

**Remove-CsAVEdgeConfiguration** Cmdlet 不會傳回值或物件，而會刪除 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.MediaRelaySettings 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsAVEdgeConfiguration](get-csavedgeconfiguration.md)  
[New-CsAVEdgeConfiguration](new-csavedgeconfiguration.md)  
[Set-CsAVEdgeConfiguration](set-csavedgeconfiguration.md)

