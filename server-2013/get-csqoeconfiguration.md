---
title: Get-CsQoEConfiguration
TOCTitle: Get-CsQoEConfiguration
ms:assetid: e2ed87e0-a5ae-41a2-8572-bda0070c59dc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399004(v=OCS.15)
ms:contentKeyID: 49292596
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsQoEConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

擷取一或多個經驗品質 (QoE) 設定的集合。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsQoEConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsQoEConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

此範例會使用 **Get-CsQoEConfiguration** Cmdlet，以傳回設定供組織使用之所有 QoE 設定的集合。

    Get-CsQoEConfiguration

## 範例 2

範例 2 會使用 Identity 參數，以確保 **Get-CsQoEConfiguration** Cmdlet 只會傳回 Identity 為 site:Redmond 的 QoE 設定。

    Get-CsQoEConfiguration -Identity site:Redmond

## 範例 3

在範例 3 中，Filter 參數可用來傳回已在網站範圍設定的所有 QoE 設定。萬用字元 "site:\*" 傳回 Identity 是以字串值 site: 開頭的所有 QoE 設定。符合該準則的設定是已在網站範圍設定的設定。

    Get-CsQoEConfiguration -Filter site:*

## 範例 4

範例 4 會傳回 KeepQoEDataForDays 屬性少於 30 天之所有 QoE 設定的集合。為達成此目的，命令會先使用 **Get-CsQoEConfiguration** Cmdlet，以傳回設定供組織使用之所有 QoE 設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet 套用篩選，以將傳回的資料限制在 KeepQoEDataForDays 值少於 30 天的設定。

    Get-CsQoEConfiguration | Where-Object {$_.KeepQoEDataForDays -lt 30}

## 詳細描述

QoE 計量追蹤在組織中建立的音訊和視訊撥號品質，包括遺失的網路封包數量、背景雜訊和「抖動」(封包延遲差異) 量。這些計量都會儲存在資料庫中，除了其他資料 (例如通話詳細記錄) 之外，讓您可啟用和停用與其他資料記錄無關的 QoE。使用這個 Cmdlet 來擷取在全域或網站層級設定 QoE 的設定。

QoE 是監控伺服器角色的一部分；因此，在 QoE 記錄生效之前或可收集任何 QoE 資料之前，您必須在 Lync Server 安裝中部署監控伺服器。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsQoEConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsQoEConfiguration"}

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
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您使用萬用字元傳回一或多個 QoE 組態設定的集合。若要傳回在網站範圍所設定之所有設定集合，請使用下列語法：-Filter site:*。若要傳回在其 Identity (您可篩選的唯一屬性) 某處具有字串值 &quot;Western&quot; 的所有設定集合，請使用下列語法：-Filter *Western*。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>您要擷取之設定的唯一識別碼。可能的值為 global 和 site:&lt;網站名稱&gt;，其中 &lt;網站名稱&gt; 是 Lync Server 在部署中要套用變更的網站名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區 的本機複本擷取設定。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

**Get-CsQoEConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.QoE.QoESettings 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsQoEConfiguration](new-csqoeconfiguration.md)  
[Remove-CsQoEConfiguration](remove-csqoeconfiguration.md)  
[Set-CsQoEConfiguration](set-csqoeconfiguration.md)

