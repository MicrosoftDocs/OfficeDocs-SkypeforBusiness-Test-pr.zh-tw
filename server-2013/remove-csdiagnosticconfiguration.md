---
title: Remove-CsDiagnosticConfiguration
TOCTitle: Remove-CsDiagnosticConfiguration
ms:assetid: b15293bf-d0d1-4322-ab1d-10b54636746a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412853(v=OCS.15)
ms:contentKeyID: 49292034
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsDiagnosticConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除組織目前所使用之一或多個診斷組態設定集合。診斷組態設定可用於指定是否要將進出指定網域或統一資源識別元 (URI) 的流量記錄在 Lync Server 記錄檔中。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsDiagnosticConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會刪除 Identity 為 site:Redmond 的診斷組態設定。

    Remove-CsDiagnosticConfiguration -Identity site:Redmond

## 範例 2

範例 2 所示的命令會刪除已在網站範圍設定的所有診斷組態設定。為達成此目的，命令會呼叫 **Get-CsDiagnosticConfiguration** Cmdlet 搭配 Filter 參數；篩選值 "site:\*" 可將傳回的資料限制在 Identity 開頭字元為 "site:" 的設定。然後再將篩選後的集合管線傳送到 **Remove-CsDiagnosticConfiguration** Cmdlet，以移除該集合中的每一個項目。

    Get-CsDiagnosticConfiguration -Filter site:* | Remove-CsDiagnosticConfiguration

## 範例 3

在範例 3 中，命令會刪除組織目前使用的所有診斷組態設定。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsDiagnosticConfiguration** Cmdlet，以傳回組織目前使用的所有診斷組態設定集合。然後再將這些項目管線傳送到 **Remove-CsDiagnosticConfiguration** Cmdlet，以移除集合中的每一個項目。

    Get-CsDiagnosticConfiguration | Remove-CsDiagnosticConfiguration

## 詳細描述

如果您啟用 Lync Server 記錄功能，則這些記錄檔中預設會包含進出任何網域或 URI 的流量。這可確保記錄檔中會盡量記錄最多的資訊。

但是，這有時候會造成資訊過多。例如，當遇到特定網域的連線問題時，需要將記錄範圍限制在您網路與該網路間的流量；這樣您才能更容易識別相關記錄，進而更輕鬆地診斷並修正問題。

診斷組態設定可讓您指定要在記錄檔中記錄的網域或 URI；如果啟用診斷篩選功能，則只會記錄進出特定網域的流量。Lync Server 讓您能夠在網站範圍建立診斷組態設定，並套用診斷篩選器。如此一來，您將能對某個網站 (例如 Redmond) 套用篩選，同時又對其他網站停用篩選。

您可以使用 **Remove-CsDiagnosticConfiguration** Cmdlet 移除您在網站範圍所建立的任何診斷組態設定。您也可以對全域診斷組態集合執行 **Remove-CsDiagnosticConfiguration** Cmdlet。不過，在該情況下，將不會刪除集合；因為 Lync Server 不允許您刪除全域集合。但是，移除全域集合會導致該集合中的屬性重設為其預設值。也就是說，將會移除新增至該集合的所有篩選。

誰可以執行這個 Cmdlet：根據預設，會授權下列群組的成員執行 **Remove-CsDiagnosticConfiguration** Cmdlet：本機執行的 Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsDiagnosticConfiguration"}

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
<td><p>要移除之診斷組態設定的唯一識別碼。若要移除在此網站範圍設定的設定，請使用類似下列的語法：-Identity &quot;site:Redmond&quot;。</p>
<p><strong>Remove-CsDiagnosticConfiguration</strong> Cmdlet 也可以針對全域組態設定來執行；在該情況下，請使用下列語法：–Identity global。不過，不會實際移除全域設定；但是，可在全域設定中找到的屬性將重設為其預設值。</p>
<p></p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.Diagnostics.DiagnosticFilterSettings 物件。**Remove-CsDiagnosticConfiguration** Cmdlet 接受診斷篩選器設定物件管線傳送的執行個體。

## 傳回類型

無。反之，**Remove-CsDiagnosticConfiguration** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.WritableConfig.Settings.Diagnostics.DiagnosticFilterSettings 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsDiagnosticConfiguration](get-csdiagnosticconfiguration.md)  
[New-CsDiagnosticConfiguration](new-csdiagnosticconfiguration.md)  
[Set-CsDiagnosticConfiguration](set-csdiagnosticconfiguration.md)

