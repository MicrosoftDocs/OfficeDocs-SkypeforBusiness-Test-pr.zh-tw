---
title: Get-CsTenantHybridConfiguration
TOCTitle: Get-CsTenantHybridConfiguration
ms:assetid: 4b2e6781-8f46-4ba3-be76-3a95460e3132
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994034(v=OCS.15)
ms:contentKeyID: 52056103
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTenantHybridConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回可讓 Microsoft Lync Online 的使用者存取 Enterprise Voice 功能 (如媒體旁路、增強型 9-1-1 和通話駐留) 的混合式組態設定值。混合式方案 (也稱為分割網域方案) 是一種 Lync Server 部署，其中部分使用者的帳戶在內部部署中，而其他使用者的帳戶則在 Lync Online 上。

Get-CsTenantHybridConfiguration Cmdlet 僅可與 商務用 Skype Online 搭配使用。

## 語法

    Get-CsTenantHybridConfiguration [[-Identity] <XdsIdentity>] [-Tenant <guid>] [-LocalStore] [<CommonParameters>]Get-CsTenantHybridConfiguration [-Tenant <guid>] [-Filter <string>] [-LocalStore] [<CommonParameters>]

## 範例

## 範例 1

範例 1 所示的命令會傳回租用戶混合式組態設定之全域集合的屬性值。

    Get-CsTenantHybridConfiguration -Identity "Global"

## 範例 2

範例 2 會傳回套用至 TenantId 為 "bf19b7db-6960-41e5-a139-2aa373474354" 之租用戶的自訂租用戶混合式組態設定的屬性值。

    Get-CsTenantHybridConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354"

## 範例 3

範例 3 會傳回所有可用租用戶的租用戶混合式組態資訊。為達成此目的，命令會先呼叫 **Get-CsTenant** Cmdlet，以傳回所有租用戶的集合。接著，此集合會以管道方式傳送到 **ForEach-Object** Cmdlet，以取得集合中的每個租用戶並逐一執行兩個工作。首先，Cmdlet 會列印出租用戶的 Active Directory 顯示名稱，這能確保輕易識別每個設定集合。之後，**ForEach-Object** Cmdlet 會執行 **Get-CsTenantHybridConfiguration** Cmdlet，傳回有問題之租用戶的租用戶混合式組態設定。

    Get-CsTenant | ForEach-Object {$_.DisplayName; Get-CsTenantHybridConfiguration -Tenant $_.TenantId}

## 詳細描述

在混合式或「分割網域」部署中，組織有部分使用者的帳戶 Lync Online 上，而同時其他使用者的帳戶在內部部署版本的 Lync Server 上。依據預設，Lync Online 上的使用者無法存取 Enterprise Voice 提供的完整功能，因為 Lync Online 伺服器無法直接存取 Lync Server 部署和網路組態資訊。此外，Lync Online 使用者沒有部分功能的預設存取權限，例如：

  - 增強型 9-1-1，用於撥打緊急電話的 Lync Server 服務。

  - 通話駐留，可讓使用者保留通話 A，然後從電話 B 擷取該項通話的 Lync Server 服務。

  - 媒體旁路，允許與公用交換電話網路 (PSTN) 之間的通話略過中繼伺服器，協助將轉碼和網路延遲降到最低。

  - PSTN 會議撥入和撥出，可讓使用者使用任何 PSTN 電話或行動裝置來參與線上會議的音訊部分。

  - 回應群組應用程式，能讓您將通話自動路由到如服務台或客戶支援專線等實體。依據預設，Lync Server 使用者無法作為回應群組代理程式運作。

若要將這些 Enterprise Voice 功能的存取權提供給 Lync Online 使用者，系統管理員需要為混合式組態設定指派適當的值，例如內部和外部 Web 服務 URL，以及組織 Access Edge Server 的完整網域名稱。這些值只能使用 **Set-CsTenantHybridConfiguration** Cmdlet 設定，能提供必要的資訊給 Lync Online 伺服器，以便使用者能使用這些進階 Enterprise Voice 功能。

您可以使用 **Get-CsTenantHybridConfiguration** Cmdlet，來傳回您組織目前使用之租用戶混合式組態設定的相關資訊。

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
<td><p>可讓您使用萬用字元來傳回租用戶混合式組態設定的集合。因為限定您只能有單一全域的混合式組態設定集合，所以不需要使用 Filter 參數。不過，這是 <strong>Get-CsTenantHybridConfiguration</strong> Cmdlet 的有效語法：</p>
<p>Get-CsTenantHybridConfiguration –Filter &quot;g*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>所傳回租用戶混合式組態設定的唯一 Identity。因為限定您只能有單一全域的混合式組態設定集合，因此使用 Identity 參數唯一能傳回的集合是全域集合：</p>
<p>-Identity global</p>
<p>若要修改個別租用戶的設定，請使用 Tenant 參數，而非 Identity 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取租用戶混合式組態資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要傳回混合式組態設定之租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行下列命令傳回每個租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>如果您正在使用 Windows PowerShell 的遠端工作階段，並且僅連線至 商務用 Skype Online，您不需要包含 Tenant 參數，而是將會根據您的連線資訊自動填入租用戶 ID。Tenant 參數主要用於混合部署。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Get-CsTenantHybridConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsTenantHybridConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.HybridConfiguration.TenantHybridConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[Set-CsTenantHybridConfiguration](set-cstenanthybridconfiguration.md)

