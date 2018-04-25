---
title: New-CsQoEConfiguration
TOCTitle: New-CsQoEConfiguration
ms:assetid: 4fc607d5-1a85-4de5-9d18-39d0425c82dc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398325(v=OCS.15)
ms:contentKeyID: 49290898
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsQoEConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

建立新的 QoE (經驗品質) 設定集合。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsQoEConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-EnableExternalConsumer <$true | $false>] [-EnablePurging <$true | $false>] [-EnableQoE <$true | $false>] [-ExternalConsumerIssuedCertId <IssuedCertId>] [-ExternalConsumerName <String>] [-ExternalConsumerURL <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-KeepQoEDataForDays <UInt32>] [-PurgeHourOfDay <UInt32>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 中的命令會使用 **New-CsQoEConfiguration** Cmdlet 建立 Identity 為 site:Redmond 的一組新經驗品質設定。除了 Identity site:Redmond 以外，新設定也會將 EnableQoE 屬性設為 False。網站設定的優先順序高於全域設定，因此，這表示將會停用 Redmond 網站的 QoE，不論在全域範圍是否已啟用 QoE 都一樣。

    New-CsQoEConfiguration -Identity site:Redmond -EnableQoE $False

## 範例 2

此命令會建立套用至 Dublin 網站的新 QoE 設定。在此範例中，我們已將 KeepQoEDataForDays 參數設為 30，因此 QoE 資料將在 30 天 (而不是預設的 60 天) 後從資料庫清除。此外，我們已將 PurgeHourOfDay 參數設為 4，表示超過我們剛才指定的 30 天的任何資料都將在上午 4:00 清除。

注意：如果您已啟用 QoE 和通話詳細記錄 (CDR)，基於效能的緣故，最好確認 QoE 的 PurgeHourOfDay 設定不同於 CDR 的 PurgeHourOfDay 設定。

    New-CsQoEConfiguration -Identity site:Dublin -KeepQoEDataForDays 30 -PurgeHourOfDay 4

## 詳細描述

QoE 計量會追蹤組織內執行的音訊與視訊通話品質，包括網路封包遺失數目、背景雜訊，以及「抖動」(封包延遲中的差異) 的數目等等。這些計量都會儲存在資料庫中，除了其他資料 (例如通話詳細記錄) 之外，讓您可啟用和停用與其他資料記錄無關的 QoE。使用此 Cmdlet 可建立在網站層級設定 QoE 的設定 (根據預設，全域層級的設定已存在，且無法移除)。

QoE 是監控伺服器角色的一部分；因此，在 QoE 記錄生效之前或可收集任何 QoE 資料之前，您必須在 Lync Server 安裝中部署監控伺服器。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsQoEConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsQoEConfiguration"}

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
<td><p>套用新設定的網站。此參數的格式必須為 site:&lt;網站名稱&gt;，其中 &lt;網站名稱&gt; 是在您 Lync Server 部署中之網站的名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableExternalConsumer</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指定外部取用者是否可以接收 QoE 報告。</p>
<p>預設值：False</p></td>
</tr>
<tr class="even">
<td><p><em>EnablePurging</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指定在經過 KeepQoEDataForDays 屬性所定義的期間之後是否將清除記錄。</p>
<p>預設值：True</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableQoE</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指定是否將收集 QoE 記錄並儲存至監控資料庫。</p>
<p>請注意，即使 EnableQoE 設為 True，除非已部署 監控伺服器 而且與登錄器集區相關聯，否則系統不會收集 QoE 資料。</p>
<p>預設值：True</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalConsumerIssuedCertId</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.BaseTypes.IssuedCertId</p></td>
<td><p>允許存取外部取用者 Web 服務之憑證的憑證 ID。</p></td>
</tr>
<tr class="odd">
<td><p><em>ExternalConsumerName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>QoE 報告的外部取用者易記名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalConsumerURL</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>將發佈 QoE 報告之外部取用者的目的地 URL。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="odd">
<td><p><em>KeepQoEDataForDays</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>QoE 資料從資料庫清除之前將會儲存的天數。如果 EnablePurging 設為 False，將會忽略此值。</p>
<p>必須為 1 至 2562 之間的值。</p>
<p>預設值：60</p></td>
</tr>
<tr class="even">
<td><p><em>PurgeHourOfDay</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>將清除已超過 KeepQoEDataForDays 屬性中指定天數之 QoE 記錄的當天小時數。</p>
<p>必須為 0 至 23 的值，表示當天的小時。例如，0 表示午夜，13 表示下午 1:00。預設值：1</p></td>
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

無。

## 傳回類型

建立 Microsoft.Rtc.Management.WritableConfig.Settings.QoE.QoESettings 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsQoEConfiguration](remove-csqoeconfiguration.md)  
[Set-CsQoEConfiguration](set-csqoeconfiguration.md)  
[Get-CsQoEConfiguration](get-csqoeconfiguration.md)

