---
title: Get-CsAccessEdgeConfiguration
TOCTitle: Get-CsAccessEdgeConfiguration
ms:assetid: 75a8a7e9-728f-4abd-87e9-593713ae39ee
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398574(v=OCS.15)
ms:contentKeyID: 49291341
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAccessEdgeConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回您組織中 Access Edge Service 電腦 (又稱為 Access Edge Server) 的組態設定資訊 。Access Edge Server 不在內部網路的使用者與內部網路內的人員通訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsAccessEdgeConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsAccessEdgeConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 會示範 **Get-CsAccessEdgeConfiguration** Cmdlet 的基本用法：呼叫不含任何額外參數的 Cmdlet 會傳回 Access Edge Server 實作的所有屬性值。請注意，不需要加入 Identity 或 Filter 參數；因為只有一組 Access Edge Server 組態資料。

    Get-CsAccessEdgeConfiguration

## 範例 2

範例 2 只會傳回 Access Edge Server 組態的三個屬性值：AllowAnonymousUsers、AllowFederatedUsers 及 AllowOutsideUsers。為達成此目的，命令會先使用 **Get-CsAccessEdgeConfiguration** Cmdlet 傳回所有 Access Edge Server 屬性值。然後再將該資訊管線傳送到 **Select-Object** Cmdlet，這會只挑出開頭為字串值 "Allow" 的屬性，而畫面上也只會顯示這些屬性值。

    Get-CsAccessEdgeConfiguration | Select-Object Allow*

## 範例 3

範例 3 所示的命令會傳回單一 Access Edge Server 組態屬性 (EnablePartnerDiscovery) 的值。為達成此目的，會先呼叫 **Get-CsAccessEdgeConfiguration** Cmdlet 傳回所有 Access Edge Server 組態屬性值。呼叫 **Get-CsAccessEdgeConfiguration** Cmdlet 會括上括號，促使 Windows PowerShell 會先完成此命令，然後再執行其他作業。當所有屬性值傳回之後，會使用標準的「點標記法」( 物件名稱後依序加上句號和屬性名稱) 顯示單一屬性：EnablePartnerDiscovery 的值。

    (Get-CsAccessEdgeConfiguration).EnablePartnerDiscovery

## 詳細描述

Access Edge Server (也稱為 Access Proxy 伺服器) 提供一種方式，讓您將 Lync Server 的功能擴大給未登入內部網路的人員使用。例如，如果您有遠端使用者 (不是透過內部網路，而是透過網際網路登入 Lync Server 的已驗證使用者)，將需要設定 Access Edge Server。此外，如果您要與其他組織建立同盟，或者如果要賦予使用者與擁有公用立即訊息服務 (例如 Yahoo\!、AOL 或 MSN) 帳戶之人員進行通訊的權限，也需要 Edge Server。Access Edge Server 位於周邊網路上，用來建立與驗證內部網路內部與外部使用者之間的 SIP 連線。

在 Lync Server 中，Access Edge Server 由單一的全域組態設定集合所管理。**Get-CsAccessEdgeConfiguration** Cmdlet 可讓您傳回這些全域設定的資訊。請注意，**Get-CsAccessEdgeConfiguration** Cmdlet 傳回的屬性值會隨 Edge Server 所設定的路由類型而有所不同。如需詳細資訊，請參閱 **Set-CsAccessEdgeConfiguration** 說明主題。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsAccessEdgeConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsAccessEdgeConfiguration"}

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
<td><p>可讓您在指定要傳回的 Access Edge 組態設定時使用萬用字元。因為您只能有一個這些設定的全域執行個體，因此幾乎沒有理由使用 Filter 參數。但如有需要，可以使用類似下列的語法擷取全域設定：-Identity &quot;g*&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要傳回之 Access Edge 組態設定的唯一識別碼。因為您只能有這些設定的單一、全域執行個體，因此在呼叫 <strong>Get-CsAccessEdgeConfiguration</strong> Cmdlet 時，不需要加入 Identity。然而，您可以使用下列語法擷取全域設定：-Identity global。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區 的本機複本擷取 Access Edge 組態資料，而非從 中央管理存放區 本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsAccessEdgeConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsAccessEdgeConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayAccessEdgeSettingsDnsSrvRouting 物件或 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayAccessEdgeSettingsDefaultRoute 物件的執行個體。

## 請參閱

#### 其他資源

[Set-CsAccessEdgeConfiguration](set-csaccessedgeconfiguration.md)

