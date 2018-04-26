---
title: Set-CsTenantHybridConfiguration
TOCTitle: Set-CsTenantHybridConfiguration
ms:assetid: 805ac9ee-df40-40e1-baaa-adffb6bd8cf6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994046(v=OCS.15)
ms:contentKeyID: 52056134
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTenantHybridConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

用於在混合式方案中針對位於 Microsoft Lync Online 的使用者提供內部部署的企業語音功能存取權限，例如媒體旁路、增強型 9-1-1 以及通話駐留。混合式方案 (亦稱為分割網域方案) 乃是 Lync Server 部署，其中會有部分使用者具有內部部署帳戶，而其他使用者具有 Lync Online 帳戶。

此 Cmdlet 僅可與 商務用 Skype Online 搭配使用。

## 語法

    Set-CsTenantHybridConfiguration [[-Identity] <XdsIdentity>] [-Tenant <guid>] [-PeerDestination <string>] [-HybridConfigServiceInternalUrl <string>] [-HybridConfigServiceExternalUrl <string>] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]Set-CsTenantHybridConfiguration [-Tenant <guid>] [-PeerDestination <string>][-HybridConfigServiceInternalUrl <string>] [-HybridConfigServiceExternalUrl <string>] [-Instance <psobject>] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

## 範例

## 範例 1

範例 1 所示的命令會針對租用戶混合式組態設定的全域集合設定內部服務 URL。若要設定全域設定，請加入 Identity 參數，後接參數值 "global"。

    Set-CsTenantHybridConfiguration -Identity "global" - HybridConfigServiceInternalUrl "https://internal.litwareinc.com"

## 範例 2

在範例 2 中，內部服務 URL 設定用於特定租用戶；在此範例中，租用戶的 TenantID 為 "bf19b7db-6960-41e5-a139-2aa373474354"。當有屬性質明確指派給個別租用戶時，該租用戶將受其個別租用戶混合式組態設定的管理，而非全域設定。

    Set-CsTenantHybridConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" HybridConfigServiceInternalUrl "https://internal.litwareinc.com"

## 範例 3

範例 3 所示的命令會針對貴組織中的所有租用戶設定內部服務 URL。為執行此操作，首先命令會使用 **Get-CsTenant** Cmdlet 傳回所有可用租用戶的集合；該集合接著會傳送至 **ForEach-Object** Cmdlet。接著，**ForEach-Object** Cmdlet 會針對集合中的各個租用戶執行 **Set-CsTenantHybridConfiguration** Cmdlet，將該類租用戶的內部服務 URL 設為 "https://internal.litwareinc.com"。

    Get-CsTenant | ForEach-Object {Set-CsTenantHybridConfiguration -Tenant $_.TenantID -HybridConfigServiceInternalUrl "https://internal.litwareinc.com"}

## 詳細說明

在混合式或「分割網域」部署中，組織會有部分使用者帳戶位於 Lync Online 而其他使用者帳戶位於 Lync Server。根據預設，位於 Lync Online 的使用者無法存取企業語音所提供的完整功能範圍；這是因為 Lync Online 伺服器無法直接存取內部部署的 Lync Server 部署與網路組態資訊。除此之外，Lync Online 使用者沒有下列項目的預設存取權限：

  - 增強型 9-1-1：此 Lync Server 服務用於撥打緊急電話。

  - 通話駐留：此 Lync Server 服務可讓使用者保留電話 A，然後擷取來自電話 B 的通話。

  - 媒體旁路：可讓發送至/自公用交換電話網路 (PSTN) 的通話繞過中繼伺服器，有助將轉碼與網路延遲降至最低。

  - PSTN 會議撥入與撥出：可讓使用者使用任何 PSTN 電話或行動裝置參與線上會議的音訊部分。

  - 回應群組應用程式：可讓您將電話自動路由至例如支援人員或客戶支援專線等實體。根據預設，Lync Online 使用者無法作為回應群組代理而運作。

為了將這些企業語音功能存取權限提供給 Lync Online 使用者，系統管理員需要將適當值指派給混合式組態設定，例如內部與外部 Web 服務 URL 以及組織的 Access Edge Server 的完整網域名稱。這些值僅可使用 **Set-CsTenantHybridConfiguration** Cmdlet 加以設定，可為 Lync Online 伺服器提供使用這些進階企業語音功能的所需資訊。

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
<td><p></p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>HybridConfigServiceExternalUrl</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>外部 Web 服務 URL。</p></td>
</tr>
<tr class="even">
<td><p><em>HybridConfigServiceInternalUrl</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>內部 Web 服務 URL。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>所要修改之租用戶混合式組態設定的唯一識別。因為您有混合式組態設定的單一全域集合限制，所以使用 Identity 參數可修改的唯一集合是全域集合：</p>
<p>-Identity global</p>
<p>若要修改個別租用戶的設定，請使用 Tenant 參數而非 Identity 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>PeerDestination</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>內部部署 Access Edge Server 的完整網域名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>正在修改其混合式組態設定之租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行下列命令傳回每個租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>倘若使用的是 Windows PowerShell 遠端工作階段並僅連線至 商務用 Skype Online，則無需包含 Tenant 參數。相反地，系統將會根據您的連線資訊自動填入租用戶識別碼。Tenant 參數主要用於混合式部署。</p></td>
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

無。 **Set-CsTenantHybridConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。**Set-CsTenantHybridConfiguration** Cmdlet 會改為修改既有的 Microsoft.Rtc.Management.WritableConfig.Settings.HybridConfiguration.TenantHybridConfiguration 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsTenantHybridConfiguration](get-cstenanthybridconfiguration.md)

