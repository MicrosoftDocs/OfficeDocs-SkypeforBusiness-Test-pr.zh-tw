---
title: Set-CsQoEConfiguration
TOCTitle: Set-CsQoEConfiguration
ms:assetid: 199f0127-7444-4f88-993a-8e6a33fdcb61
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398245(v=OCS.15)
ms:contentKeyID: 49290236
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsQoEConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改現有 QoE (經驗品質) 設定的集合。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsQoEConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsQoEConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-EnableExternalConsumer <$true | $false>] [-EnablePurging <$true | $false>] [-EnableQoE <$true | $false>] [-ExternalConsumerIssuedCertId <IssuedCertId>] [-ExternalConsumerName <String>] [-ExternalConsumerURL <String>] [-Force <SwitchParameter>] [-KeepQoEDataForDays <UInt32>] [-PurgeHourOfDay <UInt32>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 的命令使用 **Set-CsQoEConfiguration** Cmdlet 修改 Redmon 網站 (-Identity site:Redmond) 的經驗品質設定。新設定透過將 EnableQoE 參數設為 False，以關閉 QoE。

    Set-CsQoEConfiguration -Identity site:Redmond -EnableQoE $False

## 範例 2

這個命令會修改套用至 Dublin 網站的 QoE 設定。在這個範例中，我們將 KeepQoEDataForDays 參數設為 45，所以 QoE 資料在 45 天後會從資料庫中清除。此外，我們將 PurgeHourOfDay 參數設為 4，表示任何資料只要超過剛指定的 45 天，都會在上午 4:00 清除。

注意：如果您已啟用 QoE 和通話詳細記錄 (CDR)，基於效能的緣故，最好確認 QoE 的 PurgeHourOfDay 設定不同於 CDR 的 PurgeHourOfDay 設定。

    Set-CsQoEConfiguration -Identity site:Dublin -KeepQoEDataForDays 45 -PurgeHourOfDay 4

## 詳細描述

QoE 計量追蹤在組織中建立的音訊和視訊撥號品質，包括遺失的網路封包數量、背景雜訊和「抖動」(封包延遲差異) 量。這些計量都會儲存在資料庫中，除了其他資料 (例如通話詳細記錄) 之外，讓您可啟用和停用與其他資料記錄無關的 QoE。使用這個 Cmdlet 在全域或網站層級上修改配置 QoE 的設定。

QoE 是 監控伺服器 角色的一部分；因此，在 QoE 記錄生效之前或可收集任何 QoE 資料之前，您必須在 Lync Server 安裝中部署 監控伺服器。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsQoEConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsQoEConfiguration"}

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
<td><p><em>EnableExternalConsumer</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指定外部消費者是否可接收 QoE 報告。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePurging</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指定在經過 KeepQoEDataForDays 屬性中定義的期間後是否清除記錄。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableQoE</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指定是否收集 QoE 記錄，並儲存至監控資料庫。</p>
<p>請注意，即使 EnableQoE 設為 True，除非已部署 監控伺服器 而且與登錄器集區相關聯，否則系統不會收集 QoE 資料。</p></td>
</tr>
<tr class="odd">
<td><p><em>ExternalConsumerIssuedCertId</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.BaseTypes.IssuedCertId</p></td>
<td><p>允許存取外部消費者 Web 服務之憑證的憑證 ID。</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalConsumerName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>QoE 報告之外部消費者的易記名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>ExternalConsumerURL</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要張貼 QoE 報告之外部消費者的 URL。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>您要修改之設定的唯一識別碼。可能的值為 global 和 site:&lt;網站名稱&gt;，其中 &lt;網站名稱&gt; 是 Lync Server 在部署中要套用變更的網站名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>QoESettings</p></td>
<td><p>QoE 組態物件的物件參考。此物件的類型必須是 QoESettings，並且可透過呼叫 <strong>Get-CsQoEConfiguration</strong> Cmdlet 來擷取。</p></td>
</tr>
<tr class="odd">
<td><p><em>KeepQoEDataForDays</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>從資料庫清除之前，QoE 資料的儲存天數。如果 EnablePurging 設為 False，會忽略此值。</p>
<p>必須是從 1 到 2562 的值。</p></td>
</tr>
<tr class="even">
<td><p><em>PurgeHourOfDay</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>超出 KeepQoEDataForDays 屬性中指定天數之 QoE 記錄將清除的時刻。</p>
<p>必須是從 0 到 23 的值，該值代表幾點鐘。例如，0 為午夜，13 為下午 1:00。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.QoE.QoESettings 物件。接受 QoE 組態物件的管線傳送資料。

## 傳回類型

**Set-CsQoEConfiguration** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Settings.QoE.QoESettings 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsQoEConfiguration](new-csqoeconfiguration.md)  
[Remove-CsQoEConfiguration](remove-csqoeconfiguration.md)  
[Get-CsQoEConfiguration](get-csqoeconfiguration.md)

