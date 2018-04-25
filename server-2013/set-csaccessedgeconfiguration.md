---
title: Set-CsAccessEdgeConfiguration
TOCTitle: Set-CsAccessEdgeConfiguration
ms:assetid: f3108b59-1ab2-4288-a470-57d741e7e569
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413017(v=OCS.15)
ms:contentKeyID: 49292787
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsAccessEdgeConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改 Access Edge Service 電腦現有之 Access Edge 組態設定集合的屬性值。這些電腦上所執行的 Access Edge Service (又稱為 Edge Server) 可讓在內部網路的使用者與內部網路內的人員通訊。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsAccessEdgeConfiguration [-AllowAnonymousUsers <$true | $false>] [-AllowFederatedUsers <$true | $false>] [-AllowOutsideUsers <$true | $false>] [-CertificatesDeletedPercentage <UInt32>] [-DiscoveredPartnerReportPeriodMinutes <UInt32>] [-DiscoveredPartnerStandardRate <UInt32>] [-EnableArchivingDisclaimer <$true | $false>] [-EnableDiscoveredPartnerContactsLimit <$true | $false>] [-EnableUserReplicator <$true | $false>] [-Identity <XdsIdentity>] [-KeepCrlsUpToDateForPeers <$true | $false>] [-MarkSourceVerifiableOnOutgoingMessages <$true | $false>] [-MaxAcceptedCertificatesStored <UInt32>] [-MaxContactsPerDiscoveredPartner <UInt32>] [-MaxRejectedCertificatesStored <UInt32>] [-OutgoingTlsCountForFederatedPartners <UInt32>] <COMMON PARAMETERS>

    Set-CsAccessEdgeConfiguration [-AllowAnonymousUsers <$true | $false>] [-AllowFederatedUsers <$true | $false>] [-AllowOutsideUsers <$true | $false>] [-CertificatesDeletedPercentage <UInt32>] [-DefaultRouteFqdn <String>] [-DiscoveredPartnerReportPeriodMinutes <UInt32>] [-DiscoveredPartnerStandardRate <UInt32>] [-EnableArchivingDisclaimer <$true | $false>] [-EnableDiscoveredPartnerContactsLimit <$true | $false>] [-EnableUserReplicator <$true | $false>] [-IsPublicProvider <$true | $false>] [-KeepCrlsUpToDateForPeers <$true | $false>] [-MarkSourceVerifiableOnOutgoingMessages <$true | $false>] [-MaxAcceptedCertificatesStored <UInt32>] [-MaxContactsPerDiscoveredPartner <UInt32>] [-MaxRejectedCertificatesStored <UInt32>] [-OutgoingTlsCountForFederatedPartners <UInt32>] [-UseDefaultRouting <SwitchParameter>] [-VerificationLevel <AlwaysVerifiable | AlwaysUnverifiable | UseSourceVerification>] <COMMON PARAMETERS>

    Set-CsAccessEdgeConfiguration [-AllowAnonymousUsers <$true | $false>] [-AllowFederatedUsers <$true | $false>] [-AllowOutsideUsers <$true | $false>] [-BeClearingHouse <$true | $false>] [-CertificatesDeletedPercentage <UInt32>] [-DiscoveredPartnerReportPeriodMinutes <UInt32>] [-DiscoveredPartnerStandardRate <UInt32>] [-DiscoveredPartnerVerificationLevel <AlwaysVerifiable | AlwaysUnverifiable | UseSourceVerification>] [-EnableArchivingDisclaimer <$true | $false>] [-EnableDiscoveredPartnerContactsLimit <$true | $false>] [-EnablePartnerDiscovery <$true | $false>] [-EnableUserReplicator <$true | $false>] [-KeepCrlsUpToDateForPeers <$true | $false>] [-MarkSourceVerifiableOnOutgoingMessages <$true | $false>] [-MaxAcceptedCertificatesStored <UInt32>] [-MaxContactsPerDiscoveredPartner <UInt32>] [-MaxRejectedCertificatesStored <UInt32>] [-OutgoingTlsCountForFederatedPartners <UInt32>] [-UseDnsSrvRouting <SwitchParameter>] <COMMON PARAMETERS>

    Set-CsAccessEdgeConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會修改 Access Edge 組態設定的兩個屬性：AllowAnonymousUsers 屬性會設定為 True，而 VerificationLevel 屬性會設定為 UseSourceVerification。

    Set-CsAccessEdgeConfiguration -AllowAnonymousUsers $True -VerificationLevel "UseSourceVerification"

## 範例 2

範例 2 所示的命令會將 Edge Server 的路由方法變更為預設路由。為達此目的，命令必須包含 UseDefaultRouting 參數和 DefaultRouteFqdn 參數，並指定 Edge Server 完整網域名稱的參數值。

    Set-CsAccessEdgeConfiguration -UseDefaultRouting -DefaultRouteFqdn "atl-edge-001.litwareinc.com"

## 範例 3

範例 3 會將 Edge Server 的路由方法變更為 DNS 伺服器路由。這需要使用下列兩個參數：UseDnsSrvRouting (不使用任何參數值) 和 EnablePartnerDiscovery (使用參數值 $True)。

    Set-CsAccessEdgeConfiguration -UseDnsSrvRouting -EnablePartnerDiscovery $True

## 詳細描述

Edge Server (又稱為 Access Proxy 伺服器) 可讓您將 Lync Server 的功能擴及未登入您內部網路的人員。例如，您如有已經通過驗證的遠端使用者必須透過網際網路，而非內部網路登入 Lync Server，便須設定 Edge Server，為這些使用者提供存取權限。同樣地，如果您想要和其他組織建立同盟關係，或讓使用者能夠和使用公用立即訊息服務 (例如 Yahoo\!、AOL 或 MSN) 帳戶的人員通訊，便須有 Edge Server。Access Edge Server 位於周邊網路，可用來建立和驗證位於內部網路內、外使用者之間的 SIP 連線。

在 Lync Server 中，Access Edge Server 是使用組態設定的單一、全域集合來管理； **Set-CsAccessEdgeConfiguration** Cmdlet 讓您可以修改這些全域設定。請注意，可修改的屬性會根據您為 Edge Server 選擇的路由類型而定。例如，如果選擇使用網域名稱系統 (DNS) 服務路由，將會看見 BeClearinghouse 和 EnablePartnerDiscovery 屬性值，且能夠加以變更。如果使用預設路由，將無法使用這兩個屬性值；而是會看見屬性值 VerificationLevel 和 IsPublicProvider，且能夠加以變更。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsAccessEdgeConfiguration** Cmdlet：RTCUniversalServerAdmins。執行 Windows PowerShell 提示字元提供的下列命令，即可傳回指派給此 Cmdlet (包括您自行建立的任何自訂 RBAC 角色) 的所有角色型存取控制 (RBAC) 角色清單：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsAccessEdgeConfiguration"}

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
<td><p><em>AllowAnonymousUsers</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出是否允許匿名使用者 (也就是未獲授權的使用者) 跨越防火牆並加入會議與多方通話。預設值為 False。</p></td>
</tr>
<tr class="even">
<td><p><em>AllowFederatedUsers</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出是否允許內部使用者與來自同盟網域的使用者進行通訊。此屬性也會判斷內部使用者是否可與分割網域案例中的使用者進行通訊 (在分隔網域中，您的部分使用者會擁有內部部署主控的帳戶，而其他使用者則擁有外部部署主控的帳戶)。預設值為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowOutsideUsers</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>表示使用者是否可以透過網際網路存取 Lync Server。這包含匿名使用者以及試圖登入系統的遠端使用者。預設值為 True。</p></td>
</tr>
<tr class="even">
<td><p><em>BeClearingHouse</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出 Edge Server 是否可直接連線至其他組織。預設值為 False。除非受到 Microsoft 支援人員的指示，否則不應變更此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>CertificatesDeletedPercentage</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>預設值為 20。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>DefaultRouteFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>用於同盟要求之伺服器的完整網域名稱 (FQDN)。如果使用預設路由，則需要此參數。</p>
<p>請注意，您必須刪除所有主機供應商及所有公用提供者，才可以指派新的預設路由。</p></td>
</tr>
<tr class="even">
<td><p><em>DiscoveredPartnerReportPeriodMinutes</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>預設值為 60。</p></td>
</tr>
<tr class="odd">
<td><p><em>DiscoveredPartnerStandardRate</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>預設值為 20。</p></td>
</tr>
<tr class="even">
<td><p><em>DiscoveredPartnerVerificationLevel</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Edge.VerificationLevelType</p></td>
<td><p>針對已探索的夥伴所收發的訊息設定驗證層級。允許的值包括：</p>
<p>* AlwaysVerifiable</p>
<p>* AlwaysUnverifiable</p>
<p>* UseSourceVerification</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableArchivingDisclaimer</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果設定為 True，Edge Server 會傳送封存通知標頭給同盟和結算所的協力廠商。此通知 (這會通知可能封存其立即訊息 (IM) 交談的人員) 會顯示於同盟或結算所使用者的交談視窗中。預設值為 False。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableDiscoveredPartnerContactsLimit</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>預設值為 true ($True)。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePartnerDiscovery</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若為 True， Lync Server 將使用 DNS 記錄，嘗試和探索 AllowedDomains 清單中未列出的協力廠商網域。若為 False， Lync Server 將只會與可在 AllowedDomains 清單中找到的網域進行同盟。如果使用 DNS 服務路由，則需要此參數。預設值為 False。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableUserReplicator</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>預設值為 False ($False)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要傳回之 Access Edge 組態設定的唯一識別碼。因為您只會有這些設定的單一全域執行個體，所以不需在呼叫 <strong>Set-CsAccessEdgeConfiguration</strong> Cmdlet 時包含 Identity。但是，您可以視需要使用下列語法來修改全域設定：-Identity global。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>DisplayAccessEdgeSettingsDnsSrvRouting 物件或 DisplayAccessEdgeSettingsDefaultRoute 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="even">
<td><p><em>IsPublicProvider</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果預設路由要求公用立即訊息授權，則必須設定為 True。</p></td>
</tr>
<tr class="odd">
<td><p><em>KeepCrlsUpToDateForPeers</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>判斷 Edge Server 是否會定期檢查同盟網域憑證的憑證撤銷清單 (CRL)。預設值為 True。</p></td>
</tr>
<tr class="even">
<td><p><em>MarkSourceVerifiableOnOutgoingMessages</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若為 True，傳出訊息將標記為可驗證；這讓同盟的網域可以判斷每則訊息的驗證層級。若為 False，傳出訊息將全部標記為無法驗證。預設值為 True。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxAcceptedCertificatesStored</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>Edge Server 快取允許的憑證數目上限。預設值為 1000。</p></td>
</tr>
<tr class="even">
<td><p><em>MaxContactsPerDiscoveredPartner</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>每個探索到的協力廠商允許的連絡人數目上限。預設值為 1000。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxRejectedCertificatesStored</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>Edge Server 快取遭拒的憑證數目上限。預設值為 500。</p></td>
</tr>
<tr class="even">
<td><p><em>OutgoingTlsCountForFederatedPartners</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>指定可用於每個同盟協力廠商的傳輸層安全性 (TLS) 連線數量上限。TLS 連線數目下限為 1，上限為 4。依據預設，OutgoingTlsCountForFederatedPartners 設為 4。除非受到 Microsoft 支援人員的指示，否則不應變更此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>UseDefaultRouting</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>表示系統管理員必須指定用於傳送及接收同盟要求之伺服器的完整網域名稱。如果加入 UseDefaultRouting 參數，則也必須加入 DefaultRouteFqdn 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>UseDnsSrvRouting</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>指出 Edge Server 在傳送和接收同盟要求時，應依賴 DNS SRV 記錄。此為預設的路由方法。</p></td>
</tr>
<tr class="odd">
<td><p><em>VerificationLevel</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Edge.VerificationLevelType</p></td>
<td><p>如果您正在使用預設路由，可使用 VerificationLevel 屬性來檢視和評估傳入訊息的驗證層級。有效值為：</p>
<p>AlwaysVerifiable:在預設路由上接收到的所有要求都會標記為已驗證。若未出現驗證標頭，它將會自動新增至訊息中。</p>
<p>AlwaysUnverifiable:唯有當收件者 (接收該訊息的使用者) 已針對傳送訊息的人員設定 Allow ACE (存取控制項目) 時，才會傳遞訊息。</p>
<p>UseSourceVerification:訊息驗證會以訊息所含的驗證層級為基礎。若未出現任何驗證標頭，則訊息將標記為無法驗證。</p></td>
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

無。**Set-CsAccessEdgeConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Set-CsAccessEdgeConfiguration** Cmdlet 不會傳回任何物件或值。

## 請參閱

#### 其他資源

[Get-CsAccessEdgeConfiguration](get-csaccessedgeconfiguration.md)

