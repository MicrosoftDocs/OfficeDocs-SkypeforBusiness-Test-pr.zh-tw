---
title: Lync Server 2013 中的架構屬性和描述
TOCTitle: Lync Server 2013 中的架構屬性和描述
ms:assetid: b009df76-9c22-471d-b57a-bda009a98261
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412841(v=OCS.15)
ms:contentKeyID: 49292028
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的架構屬性和描述

 

_**上次修改主題的時間：** 2015-03-09_

本節描述 Lync Server 2013 所使用的所有架構屬性。針對與屬性相關聯的類別，請參閱[Lync Server 2013 中的架構屬性 (按類別)](lync-server-2013-schema-attributes-by-class.md)。如需Lync Server 2013 中新類別與屬性的清單，請參閱 [Lync Server 2013 中的結構描述變更](lync-server-2013-schema-changes-in-lync-server-2013.md)。

成對連結的屬性會被指定為前導連結或反向連結。參考其他物件的屬性為前導連結；反向參考第一個物件的其他物件屬性稱為反向連結。前導連結可以更新，而反向連結則是唯讀的。

部分屬性擁有位元遮罩值。這些屬性的每一項設定都會以位元表示，而顯示的十進位值表示位元位置。位元位置開頭為位元 0。例如 1 (二進位) 是設定位元 0，而 10000 (二進位) 是設定位元 4。每一個位元代表一個屬性。以下為部分範例：

  - 10000 (二進位) 的十進位值為 16 (即設定位元 4)。

  - 100000000 (二進位) 的十進位值為 256 (即設定位元 8)。

  - 1100 (二進位) 的十進位值為 12 (亦即，設定位元 2 和 3，並且會啟用這兩個位元代表的屬性)。

  - 1111000001 (二進位) 的十進位值為 961 (亦即，設定位元 0、6、7、8 和 9，並且會啟用這些位元分別代表的屬性)。

### Lync Server 2013 的架構屬性

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>屬性</th>
<th>說明</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>dnsHostName</p></td>
<td><p>目前與 <strong>msRTCSIP-Pool</strong> 和 <strong>msRTCSIP-MonitoringServer</strong> 類別相關聯之 Active Directory 網域服務 中的現有屬性。此屬性會指定集區或監控伺服器的完整網域名稱 (FQDN)。</p>
<p>每個區段的有效值為 63 個字元，整個 FQDN 的有效值為 255 個字元。</p></td>
<td><p>Microsoft Office Live Communications Server 2005 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msDS-SourceObjectDN</p></td>
<td><p>此屬性包含另一個樹系中與此物件對應之物件的辨別名稱 (DN) 字串表示法。此屬性用於通訊群組擴充和自動語音應答。此屬性是在 Windows Server 2003 R2 的預設 Active Directory 架構中定義的。</p>
<p>為了不必將 AD DS 升級成 Windows Server 2003 R2，Active Directory 架構準備會使用這個屬性定義擴充 Windows Server 2003 架構。</p></td>
<td><p>Microsoft Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msExchUCVoiceMailSettings</p></td>
<td><p>這個多重值屬性會保存語音信箱設定。此屬性會與 Exchange 整合通訊 (UM) 共用。</p></td>
<td><p>Microsoft Lync Server 2010 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msExchUserHoldPolicies</p></td>
<td><p>這個多重值屬性會保存套用至使用者之保存原則的識別碼。保存原則會保留使用者在保存期間的信箱項目。這個屬性與 Exchange 2013 共用。</p></td>
<td><p>Lync Server 2013 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-AcpInfo</p></td>
<td><p>此屬性會為使用者儲存音訊會議提供者資訊。</p></td>
<td><p>Lync Server 2010 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-ApplicationDestination</p></td>
<td><p>此屬性會指向應用程式連絡人的受信任服務項目。</p></td>
<td><p>Microsoft Office Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-ApplicationList</p></td>
<td><p>此屬性包含應用程式伺服器上主控應用程式的清單。</p></td>
<td><p>Office Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-ApplicationOptions</p></td>
<td><p>此屬性會指定應用程式連絡人的選項。</p></td>
<td><p>Office Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-ApplicationPrimaryLanguage</p></td>
<td><p>此屬性包含應用程式連絡人的主要語言。</p></td>
<td><p>Office Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-ApplicationSecondaryLanguages</p></td>
<td><p>此多重值屬性包含應用程式連絡人的次要語言。</p></td>
<td><p>Office Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-ApplicationServerBL</p></td>
<td><p>此屬性包含此集區所屬應用程式伺服器的清單。此反向連結屬性的對應前導連結為 <strong>msRTCSIP-ApplicationServerPoolLink</strong>。</p></td>
<td><p>Office Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-ApplicationServerPoolLink</p></td>
<td><p>此屬性指向此應用程式伺服器所屬的集區。這是前導連結。對應的反向連結是 <strong>msRTCSIP-ApplicationServerBL</strong>。</p></td>
<td><p>Office Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-ArchiveDefault (過時的)</p></td>
<td><p>-</p></td>
<td><p>Live Communications Server 2005 的新增項目。</p>
<p>在 Office Communications Server 2007 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-ArchiveDefaultFlags (過時的)</p></td>
<td><p>此屬性為封存所有使用者通訊作業，指定樹系界限內的全域預設。這由封存代理程式層強制執行。此屬性的值範圍如下：</p>
<ul>
<li><p><strong>TRUE</strong>：封存所有使用者</p></li>
<li><p><strong>FALSE</strong>：不封存所有使用者</p></li>
</ul>
<p>此屬性在樹系界限內，全域控制如何封存內部網路中的使用者通訊。</p>
<p><strong>Live Communications Server 2005 行為 (現已撤銷)</strong></p>
<p>此屬性的值範圍如下：</p>
<ul>
<li><p>0: 封存訊息本文 [位元 0]</p></li>
<li><p>1: 不封存訊息本文 [位元 0]</p></li>
</ul>
<p><strong>Office Communications Server 2007 行為</strong></p>
<p>此屬性的值範圍如下：</p>
<ul>
<li><p>0: ArchiveFederationDefaultWithoutBody (已撤銷)</p></li>
<li><p>1-2: ArchiveInternalCommunications</p></li>
<li><p>3-4: ArchiveFederatedCommunications</p></li>
<li><p>5: RecordPresenceRegistrations</p></li>
<li><p>6: RecordIMCallDetails</p></li>
<li><p>7: RecordGroupIMCallDetails</p></li>
<li><p>8: RecordFileTransferInstances</p></li>
<li><p>9: RecordAudioCallDetails</p></li>
<li><p>10: RecordVideoCallDetails</p></li>
<li><p>11: RecordRemoteAssistanceCallDetails</p></li>
<li><p>12: RecordApplicationSharingDetails</p></li>
<li><p>13: RecordMeetingInstantiations</p></li>
<li><p>14: RecordMeetingJoins</p></li>
<li><p>15: RecordDataJoins</p></li>
<li><p>16: RecordAVJoins</p></li>
</ul></td>
<td><p>Live Communications Server 2005 的新增項目。</p>
<p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-ArchiveFederationDefault (過時的)</p></td>
<td><p>-</p></td>
<td><p>Live Communications Server 2005 的新增項目。</p>
<p>在 Office Communications Server 2007 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-ArchiveFederationDefaultFlags (過時的)</p></td>
<td><p>-</p></td>
<td><p>Live Communications Server 2005 的新增項目。</p>
<p>在 Office Communications Server 2007 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-ArchivingEnabled</p></td>
<td><p>此屬性是做為位元欄位使用的整數，用以控制是否封存單一使用者的通訊。這項控制由封存代理程式層強制執行。這是標示要用於通用類別目錄複寫。</p>
<p>此屬性的範圍是單一使用者或連絡人特有的。Lync Server 中的有效值 (以及相關聯的位元位置) 如下：</p>
<ul>
<li><p>0: 不要封存 (未設定位元)</p></li>
<li><p>1: 已撤銷 (位元位置 0)</p></li>
<li><p>2: 已撤銷 (位元位置 1)</p></li>
<li><p>4: 封存內部通訊 (位元位置 2)</p></li>
<li><p>8: 封存同盟通訊 (位元位置 3)</p></li>
</ul>
<p>先前在 Live Communications Server 2005 中的有效值如下：</p>
<ul>
<li><p>0：依照此優先順序，使用 <strong>msRTCSIP-ArchiveDefault</strong> 和 <strong>msRTCSIP-ArchiveFederation</strong> 所定義的預設值：</p>
<ul>
<li><p>1: 封存</p></li>
<li><p>2: 不要封存</p></li>
<li><p>3: 封存，不含訊息本文</p></li>
</ul></li>
</ul></td>
<td><p>Live Communications Server 2005 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-ArchivingServerData (過時的)</p></td>
<td><p>此屬性保留供未來使用。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-ArchivingServerVersion (過時的)</p></td>
<td><p>此屬性定義封存服務的版本。此屬性是會隨著每個正式產品版本而一再重複遞增的整數型別。可能的有效值如下：</p>
<ul>
<li><p>未定義：Live Communications Server 2003</p>
<p>                 Live Communications Server 2005</p>
<p>                 Live Communications Server 2005 含 SP1</p></li>
<li><p>3: Office Communications Server 2007</p></li>
<li><p>4: Office Communications Server 2007 R2</p></li>
</ul></td>
<td><p>Office Communications Server 2007 的新增項目。</p>
<p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-BackEndServer</p></td>
<td><p>此屬性指定集區之後端伺服器的 FQDN。由於每個集區只能有單一後端伺服器，因此，這是單一值的屬性。</p>
<p>每個區段的有效值為 63 個字元，整個 FQDN 的有效值為 255 個字元。</p></td>
<td><p>Live Communications Server 2005 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-ConferenceDirectoryHomePool</p></td>
<td><p>此屬性包含裝載會議目錄之集區的識別元。</p></td>
<td><p>Office Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-ConferenceDirectoryId</p></td>
<td><p>此屬性包含會議目錄的識別元。</p></td>
<td><p>Office Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-ConferenceDirectoryTargetPool</p></td>
<td><p>此屬性包含會議目錄要移動到的集區之識別元。</p></td>
<td><p>Office Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-Default</p></td>
<td><p>此布林屬性定義電話使用方式是否為預設使用方式。如果此屬性設為 <strong>TRUE</strong>，表示電話使用方式為預設使用方式，系統管理員無法刪除。如果此屬性設為 <strong>FALSE</strong>，則可以刪除此使用方式。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-DefaultCWAExternalURL</p></td>
<td><p>此屬性會識別組織外部之使用者的 Communicator Web Access URL。</p></td>
<td><p>Office Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-DefaultCWAInternalURL</p></td>
<td><p>此屬性會識別組織內部之使用者的 Communicator Web Access URL。</p></td>
<td><p>Office Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-DefaultLocationProfileLink (過時的)</p></td>
<td><p>此單一值屬性包含指派給此屬性的位置設定檔類別物件的辨別名稱 (DN)。</p>
<p>前導連結：<strong>連結 ID 11036</strong></p>
<p>對應的反向連結是 <strong>msRTCSIP-ServerReferenceBL</strong>。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-DefaultPolicy (過時的)</p></td>
<td><p>此布林屬性指定原則是否為預設原則。設為 <strong>TRUE</strong> 時，表示原則為預設原則。</p></td>
<td><p>Office Communications Server 2007 的新增功能</p>
<p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-DefaultRouteToEdgeProxy (過時的)</p></td>
<td><p>此屬性會指定執行 Access Edge Service 之 Edge Server 的 FQDN (如果可以直接存取它)，或是執行 Access Edge Service 之伺服器集區的硬體負載平衡器的 FQDN。如果執行 Access Edge Service 的伺服器只能透過一個或多個 Director 存取，則此屬性會指定 FQDN，並選擇性地指定 Director 或做為 Director 集區的硬體負載平衡器的連接埠編號。</p>
<p>每個區段的有效值為 63 個字元，整個 FQDN 的有效值為 255 個字元。</p></td>
<td><p>Live Communications Server 2005 的新增項目。</p>
<p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-DefaultRouteToEdgeProxyPort (過時的)</p></td>
<td><p>此屬性代表應該用來連線到執行 Access Edge Service 之伺服器的連接埠編號。</p>
<p>有效值為整數值，指定要使用的連接埠。預設值為 5061。</p></td>
<td><p>Live Communications Server 2005 的新增項目。</p>
<p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-DefPresenceSubscriptionTimeout (過時的)</p></td>
<td><p>此屬性代表預設的顯示狀態訂閱逾時期間。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-DefRegistrationTimeout (過時的)</p></td>
<td><p>此屬性代表預設的註冊逾時時限。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-DefRoamingDataSubscriptionTimeout (過時的)</p></td>
<td><p>此屬性代表預設的漫遊資料訂閱逾時時限。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-DeploymentLocator</p></td>
<td><p>此屬性用於分割網域拓撲且包含完整網域名稱 (FQDN)。</p></td>
<td><p>Lync Server 2010 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-Description (過時的)</p></td>
<td><p>此單一值 UNICODE 字串屬性包含此電話路由或正規化規則的易記描述。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p>
<p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-DomainData</p></td>
<td><p>此屬性保留供未來使用。</p></td>
<td><p>-</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-DomainName</p></td>
<td><p>此屬性代表為登錄器設定的網域。</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-EdgeProxyData</p></td>
<td><p>此屬性保留供未來使用。</p></td>
<td><p>Live Communications Server 2005 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-EdgeProxyFQDN</p></td>
<td><p>此屬性指定執行 Access Edge Service 之伺服器的 FQDN。</p>
<p>每個區段的有效值為 63 個字元，整個 FQDN 的有效值為 255 個字元。</p></td>
<td><p>Live Communications Server 2005 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-EnableBestEffortNotify (過時的)</p></td>
<td><p>此屬性控制伺服器在回應用戶端的 SUBSCRIBE 要求時，是否會產生 Best Effort NOTIFY (BENOTIFY) 要求，而非 NOTIFY 要求。BENOTIFY 增強了訂閱通知信號交換的效能，讓伺服器產生 BENOTIFY 要求，而非一般的 NOTIFY 要求。這項效能優勢在於，BENOTIFY 要求不會像 NOTIFY 要求一樣，要求來自用戶端的 200 OK 回應。</p>
<p>有效值為 <strong>TRUE</strong> 或 <strong>FALSE</strong>。</p>
<div>

> [!NOTE]   
> Live Communications Server 2003 不支援 BENOTIFY 要求。若要與使用 Live Communications Server 2003 伺服器 API (在 Live Communications Server 2005 及協力廠商伺服器上執行) 所撰寫的伺服器應用程式相互操作，可以將值設為 <strong>FALSE</strong> 以停用 BENOTIFY 要求。BENOTIFY 目前不是 IETF (網際網路工程任務推動小組) SIP 標準程序的一部分。


</div></td>
<td><p>Live Communications Server 2005 的新增項目。</p>
<p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-EnableFederation (過時的)</p></td>
<td><p>此屬性為全域參數，IT 管理員用它來設定使用者是否能夠與來自其他組織的使用者進行通訊。它讓系統管理員可以覆寫個別使用者的 <strong>FederationEnabled</strong> 屬性。此屬性可以有效保護內部網路，免於受到因蠕蟲、病毒或針對公司所發動攻擊而引起的網際網路攻擊。</p>
<p>有效值 (和相關聯的位元位置) 如下：</p>
<ul>
<li><p>1: 啟用公用 IM 連線 (位元位置 0)</p></li>
<li><p>2: 已保留 (位元位置 1)</p></li>
<li><p>4: 已保留 (位元位置 2)</p></li>
<li><p>8: 已保留 (位元位置 3)</p></li>
<li><p>16: 已啟用遠端呼叫控制 [電話語音] (位元位置 4)</p></li>
<li><p>64: AllowOrganizeMeetingWithAnonymousParticipants (允許使用者邀請匿名使用者加入會議) (位元位置 6)</p></li>
<li><p>128: UCEnabled (允許使用者進行整合通訊) (位元位置 7)</p></li>
<li><p>256: EnabledForEnhancedPresence (允許使用者進行公用 IM 連線) (位元位置 8)</p></li>
<li><p>512: RemoteCallControlDualMode (位元位置 9)</p></li>
</ul></td>
<td><p>Live Communications Server 2005 的新增項目。</p>
<p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-EnterpriseServices</p></td>
<td><p>此屬性指示是否要在特定伺服器上載入企業服務。</p></td>
<td><p>-</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-ExtensionData</p></td>
<td><p>此屬性保留供未來使用。</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-ExternalAccessCode</p></td>
<td><p>此屬性包含用於外部存取的撥接代碼。</p></td>
<td><p>Office Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-FederationEnabled</p></td>
<td><p>此屬性控制是否允許單一使用者使用同盟。這由「企業服務」層強制執行。這是標示要用於通用類別目錄複寫。</p>
<p>有效值為 <strong>TRUE</strong> 或 <strong>FALSE</strong>。</p></td>
<td><p>Live Communications Server 2005 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-FrontEndServers</p></td>
<td><p>此屬性是多重值清單，列出與集區相關聯之所有 Enterprise Edition Server 的網域名稱。</p>
<p>反向連結：<strong>連結 ID 11023</strong></p>
<p>此反向連結的對應前導連結為 <strong>msRTCSIP-PoolAddress</strong>。</p></td>
<td><p>Live Communications Server 2005 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-Gateways (過時的)</p></td>
<td><p>此多重值字串屬性包含閘道和 (每一閘道的) 連接埠清單。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-GlobalSettingsData (過時的)</p></td>
<td><p>此屬性儲存成對的「名稱:值」。已定義的成對「名稱：值」是用於<strong>「允許出席投票」</strong>設定。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-GroupingID</p></td>
<td><p>此屬性是用來分組通訊錄項目之群組的唯一識別碼。</p></td>
<td><p>Lync Server 2010 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-HomeServer (過時的)</p></td>
<td><p>-</p></td>
<td><p>Live Communications Server 2003 的新增功能 (未使用)。</p>
<p>在 Live Communications Server 2005 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-HomeServerString (過時的)</p></td>
<td><p>-</p></td>
<td><p>Live Communications Server 2003 的新增項目。</p>
<p>在 Live Communications Server 2005 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-HomeUsers (過時的)</p></td>
<td><p>-</p></td>
<td><p>Live Communications Server 2003 的新增功能 (未使用)。</p>
<p>在 Live Communications Server 2005 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-InternetAccessEnabled</p></td>
<td><p>此屬性控制是否要啟用單一使用者，讓外部使用者存取。這由「企業服務」層強制執行。這是標示要用於通用類別目錄複寫。</p>
<p>有效值為 <strong>TRUE</strong> 或 <strong>FALSE</strong>。</p></td>
<td><p>Live Communications Server 2005 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-IsMaster (過時的)</p></td>
<td><p>-</p></td>
<td><p>Live Communications Server 2003 的新增功能</p>
<p>在 Live Communications Server 2005 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-Line</p></td>
<td><p>此單一值屬性包含 Lync 用於電話語音的裝置 ID (使用者所控制電話的 SIP URI 或 TEL URI)。此屬性是標示要用於「通用類別目錄」複寫，而且使用索引。如果使用者已啟用 Enterprise Voice，此屬性會儲存使用者電話號碼的 E.164 正規化版本。</p></td>
<td><p>Microsoft Office Live Communications Server 2005 含 SP1 的新增功能</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-LineServer</p></td>
<td><p>此單一值屬性包含 CSTA-SIP 閘道伺服器的 SIP URI。此屬性是標示要用於「通用類別目錄」複寫，但不使用索引。</p></td>
<td><p>Microsoft Office Live Communications Server 2005 含 SP1 的新增功能</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-LocalNormalizationData (過時的)</p></td>
<td><p>此屬性保留供未來使用。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p>
<p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-LocalNormalizationLinks (過時的)</p></td>
<td><p>此多重值屬性包含與此位置設定檔相關聯的本機正規化辨別名稱 (DN) 清單。此屬性的型別是 DN 二進位。位置設定檔和本機正規化規則之間是一對多的關係。本機正規化 DN 清單的次序必須維持系統管理員所指定的次序。保留次序就是藉由 DN 二進位中用於指定次序索引的二進位部分來維持。</p>
<p>Forward link:<strong>連結 ID 11034</strong></p>
<p>此前導連結屬性的對應反向連結為 <strong>msRTCSIP-LocationProfileBL</strong>。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p>
<p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-LocalNormalizationOptions</p></td>
<td><p>此屬性包含正規化規則的選項清單。</p></td>
<td><p>Office Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-LocationName (過時的)</p></td>
<td><p>此單一值屬性包含位置設定檔的易記名稱，以指示這個設定檔所代表的位置。因為可能有多個位置設定檔，系統管理員需要這種方法來分辨不同設定檔。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p>
<p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-locationProfileBL (過時的)</p></td>
<td><p>此多重值屬性包含位置設定檔的辨別名稱清單。此屬性指定指向一個或多個位置設定檔的反向連結。</p>
<p>Back link:<strong>連結 ID 11035</strong></p>
<p>此屬性對應到前導連結 <strong>msRTCSIP-LocalNormalizationLinks</strong>。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p>
<p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-LocationProfileData (過時的)</p></td>
<td><p>此屬性保留供未來使用。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p>
<p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-LocationProfileOptions</p></td>
<td><p>此屬性包含位置設定檔的選項。</p></td>
<td><p>Office Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-MappingContact</p></td>
<td><p>此多重值屬性包含應用程式連絡人的清單。</p></td>
<td><p>Office Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-MappingLocation</p></td>
<td><p>此多重值屬性包含位置設定檔的清單。</p></td>
<td><p>Office Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-MaxNumOutstandingSearchPerServer (過時的)</p></td>
<td><p>此屬性代表每部伺服器未完成搜尋要求的數目上限。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-MaxNumSubscriptionsPerUser (過時的)</p></td>
<td><p>此屬性代表每個使用者的訂閱數目上限。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-MaxPresenceSubscriptionTimeout (過時的)</p></td>
<td><p>此屬性代表訂閱逾時時限的上限。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-MaxRegistrationsTimeout (過時的)</p></td>
<td><p>此屬性代表註冊逾時時限的上限。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-MaxRoamingDataSubscriptionTimeout (過時的)</p></td>
<td><p>此屬性代表漫遊資料訂閱逾時時限的上限。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-MCUData</p></td>
<td><p>此屬性保留供未來使用。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-MCUFactoryAddress</p></td>
<td><p>此屬性是電腦類別下的服務控制點屬性，用以指定返回此電腦所屬 Multipoint Control Unit (MCU) Factory 的連結。系統會為每個 Microsoft MCU 建立這個服務控制點和屬性。每個 Microsoft MCU 必須找到它所屬集區的後端伺服器，才能夠從該處擷取集區層級的設定。</p>
<p>此屬性的值為 MCU Factory 的辨別名稱 (DN)。這是單一值屬性，而且標示要用於通用類別目錄複寫。</p>
<p>Forward link:<strong>連結 ID 11026</strong></p>
<p>此前導連結屬性的對應反向連結是 <strong>msRTCSIP-MCUServers</strong>。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-MCUFactoryData</p></td>
<td><p>這是多重字串的保留屬性。儲存在此屬性中的設定以成對的「名稱=值」方式表示。目前已定義的成對「名稱=值」有：</p>
<ul>
<li><p>FactoryURL = &lt;URL&gt;</p></li>
</ul></td>
<td><p>Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-MCUFactoryPath</p></td>
<td><p>此為單一值屬性，其中包含與集區相關聯的單一 MCU Factory 辨別名稱 (DN)。</p>
<p>Forward link:<strong>連結 ID 11024</strong></p>
<p>此前導連結屬性的對應反向連結為 <strong>msRTCSIP-PoolAddresses</strong>。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-MCUFactoryProviderID</p></td>
<td><p>此屬性是單一值字串，會指定 MCU Factory 提供者的 GUID。MCU Factory 處理序會根據 GUID 值，決定是否服務此 MCU 類型。如果 GUID 值是 <strong>{F0810510-424F-46ef-84FE-6CC720DF1791}</strong>，MCU Factory 處理序 (Lync Server 預設會提供) 就會處理它。如果是其他任何 GUID 值，則 MCU Factory 處理序將不會服務該 MCU 類型。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-MCUServers</p></td>
<td><p>此屬性是辨別名稱 (DN) 的多重值清單。此屬性包含與此 MCU Factory 相關聯之相同類型和廠商的所有 MCU 伺服器清單。每個區段的有效值為 63 個字元，整個 FQDN 的有效值為 255 個字元。</p>
<p>反向連結：連結 ID 11027</p>
<p>此反向連結的對應前導連結為 <strong>msRTCSIP-MCUFactoryAddress</strong>。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-MCUType</p></td>
<td><p>此屬性是單一值字串，會指定 MCU 可處理的媒體。</p>
<p>支援的有效類型如下：</p>
<ul>
<li><p>meeting</p></li>
<li><p>audio-video</p></li>
<li><p>chat</p></li>
<li><p>phone-conf</p></li>
</ul></td>
<td><p>Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-MCUVendor</p></td>
<td><p>此屬性是單一值字串，會指定 MCU 廠商的名稱。所有 Microsoft MCU 都會將此屬性指定為 <strong>Microsoft Corporation</strong>。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-MeetingFlags (過時的)</p></td>
<td><p>此屬性定義為所有使用者或連絡人物件全域啟用的不同會議選項。此屬性是整數型別的位元遮罩值。</p>
<p>有效值 (和相關聯的位元位置) 如下：</p>
<ul>
<li><p>0: AllowOrganizeMeetingWithAnonymousParticipants 為 None (不允許使用者邀請匿名使用者加入會議) (未設定位元)</p></li>
<li><p>4: AllowOrganizeMeetingWithAnonymousParticipants 為 Everyone (允許所有使用者邀請匿名使用者加入會議) (位元位置 2)</p></li>
<li><p>8: AllowOrganizeMeetingWithAnonymousParticipants 為 UsePerUserSetting (根據每個使用者設定，允許使用者邀請匿名使用者加入會議) (位元位置 3)</p></li>
<li><p>16: UserPerUserMeetingPolicy (針對每個使用者分別定義會議原則) (位元位置 4)</p></li>
</ul></td>
<td><p>Office Communications Server 2007 的新增項目。</p>
<p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-MeetingPolicy (過時的)</p></td>
<td><p>此屬性指定系統管理員以單一值屬性方式為此使用者指派的原則辨別名稱 (DN)。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p>
<p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-MinPresenceSubscriptionTimeout (過時的)</p></td>
<td><p>此屬性代表顯示狀態訂閱逾時時限的下限。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-MinRegistrationTimeout (過時的)</p></td>
<td><p>此屬性代表註冊逾時時限的下限。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p>
<p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-MinRoamingDataSubscriptionTimeout (過時的)</p></td>
<td><p>此屬性代表漫遊資料訂閱逾時時限的下限。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p>
<p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-MirrorBackEndServer</p></td>
<td><p>此屬性用來儲存前端集區所使用的鏡像 SQL Server 後端。</p></td>
<td><p>Lync Server 2013 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-MobilityFlags</p></td>
<td><p>此屬性包含定義行動性設定的選項和旗標。</p></td>
<td><p>Office Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-MobilityPolicy</p></td>
<td><p>此屬性包含行動性原則物件的 DN。</p></td>
<td><p>Office Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-NumDevicesPerUser (過時的)</p></td>
<td><p>此屬性代表允許的裝置數目，使用者可在這個數目的裝置上註冊 SIP 通訊並訂閱顯示狀態。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p>
<p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-OptionFlags</p></td>
<td><p>此屬性指定已為使用者或連絡人物件啟用的選項。此屬性是整數型別的位元遮罩值。每個選項由一個位元代表。此屬性是標示要用於「通用類別目錄」複寫。</p>
<p>有效值 (和相關聯的位元位置) 如下：</p>
<ul>
<li><p>1: 啟用公用立即訊息 (IM) 連線 (位元位置 0)</p></li>
<li><p>2: 已保留 (位元位置 1)</p></li>
<li><p>4: 已保留 (位元位置 2)</p></li>
<li><p>8: 已保留 (位元位置 3)</p></li>
<li><p>16: 已啟用遠端呼叫控制 [電話語音] (位元位置 4)</p></li>
<li><p>64: AllowOrganizeMeetingWithAnonymousParticipants (允許使用者邀請匿名使用者加入會議) (位元位置 6)</p></li>
<li><p>128: UCEnabled (允許使用者進行 UC) (位元位置 7)</p></li>
<li><p>256: EnabledForEnhancedPresence (允許使用者進行公用 IM 連線) (位元位置 8)</p></li>
<li><p>512: RemoteCallControlDualMode (位元位置 9)</p></li>
</ul></td>
<td><p>Live Communications Server 2005 含 SP1 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-OriginatorSID</p></td>
<td><p>此屬性用於資源和中央樹系拓撲中，在來自 Windows NT Server 主體帳戶的使用者 ObjectSID 複製到資源或中央樹系中對應使用者或連絡人物件的這個屬性時，允許單一登入。Communicator Web Access 會使用此屬性或使用者的 ObjectSID，在 AD DS 中搜尋使用者。此屬性是標示要用於「通用類別目錄」複寫。</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-OwnerUrn</p></td>
<td><p>此屬性是應用程式連絡人的擁有者統一資源名稱 (URN)。</p></td>
<td><p>Lync Server 2010 的新增項目。</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-Pattern (過時的)</p></td>
<td><p>此單一值字串屬性包含將撥號號碼比對成 E.164 格式時所用的模式。如果撥號號碼符合此模式，就會轉譯此撥號號碼。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p>
<p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-PhoneRouteBL (過時的)</p></td>
<td><p>此多重值屬性包含電話路由辨別名稱 (DN) 清單。此屬性指定指向一個或多個電話路由的反向連結。</p>
<p>Back link:<strong>連結 ID 11033</strong></p>
<p>此屬性對應到前導連結 <strong>msRTCSIP-RouteUsageLinks</strong>。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p>
<p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-PhoneRouteData (過時的)</p></td>
<td><p>此屬性保留供未來使用。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-PhoneRouteName (過時的)</p></td>
<td><p>此單一值 UNICODE 字串屬性指定電話路由的易記名稱，以方便系統管理員參考。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-PhoneUsageData (過時的)</p></td>
<td><p>此屬性保留供未來使用。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p>
<p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-PolicyContent (過時的)</p></td>
<td><p>此屬性是單一值 Unicode 字串。此字串屬性包含 XML 格式的原則定義。XML 結構描述定義在不同原則類型之間是共通的，只有各原則類型的設定不相同。</p>
<p>XML 結構描述定義 (XSD) 定義如下：</p>
<pre><code>&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;
&lt;xs:schema id=&quot;instance&quot;  xmlns:xs=&quot;http://www.w3.org/2001/XMLSchema&quot; xmlns:msdata=&quot;urn:schemas-microsoft-com:xml-msdata&quot;&gt;
  &lt;xs:element name=&quot;instance&quot; msdata:IsDataSet=&quot;true&quot;&gt;
    &lt;xs:complexType&gt;
      &lt;xs:choice maxOccurs=&quot;unbounded&quot;&gt;
        &lt;xs:element name=&quot;property&quot; nillable=&quot;true&quot;&gt;
          &lt;xs:complexType&gt;
            &lt;xs:simpleContent msdata:ColumnName=&quot;property_Text&quot; msdata:Ordinal=&quot;1&quot;&gt;
              &lt;xs:extension base=&quot;xs:string&quot;&gt;
                &lt;xs:attribute name=&quot;name&quot; type=&quot;xs:string&quot; /&gt;
              &lt;/xs:extension&gt;
            &lt;/xs:simpleContent&gt;
          &lt;/xs:complexType&gt;
        &lt;/xs:element&gt;
      &lt;/xs:choice&gt;
    &lt;/xs:complexType&gt;
  &lt;/xs:element&gt;
&lt;/xs:schema&gt;</code></pre></td>
<td><p>Office Communications Server 2007 的新增項目。</p>
<p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-PolicyData (過時的)</p></td>
<td><p>此屬性保留供未來使用。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p>
<p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-PolicyType (過時的)</p></td>
<td><p>此單一值 Unicode 字串屬性包含原則類型。有效原則類型如下：</p>
<ul>
<li><p>meeting</p></li>
<li><p>telephony</p></li>
</ul></td>
<td><p>Office Communications Server 2007 的新增項目。</p>
<p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-PoolAddress</p></td>
<td><p>此屬性指定返回電腦所屬集區的連結。不論電腦執行的是 Standard Edition 或 Enterprise Edition 的 Lync Server，都會設定此屬性。此屬性是標示要用於「通用類別目錄」複寫。</p>
<p>有效值為集區的網域名稱。</p>
<p>Forward link:<strong>連結 ID 11022</strong></p>
<p>此前導連結屬性的對應反向連結是 <strong>msRTCSIP-FrontEndServers</strong>。</p></td>
<td><p>Live Communications Server 2005 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-PoolAddresses</p></td>
<td><p>此多重值屬性包含與 MCU Factory 相關聯之集區的辨別名稱 (DN) 清單。</p>
<p>Back link:<strong>連結 ID 11025</strong></p>
<p>此反向連結的對應前導連結為 <strong>msRTCSIP-MCUFactoryPath</strong>。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-PoolData</p></td>
<td><p>此屬性保留供未來使用。</p></td>
<td><p>Live Communications Server 2005 含 SP1 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-PoolDisplayName</p></td>
<td><p>此屬性指定管理主控台所顯示的任意集區名稱。系統管理員可以變更此名稱。</p>
<p>有效值為代表集區名稱的字串。</p></td>
<td><p>Live Communications Server 2005 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-PoolDomainFQDN</p></td>
<td><p>此屬性是單一值字串值。此屬性若有值，即代表集區的網域 FQDN，當系統管理員想要以不符合前端集區建立所在之 Active Directory 網域結構的 FQDN，建立前端集區 (例如，SIP 命名空間與網域名稱系統 (DNS) 命名空間分離) 時，便會使用此 FQDN。</p>
<p>我們建議將前端集區的網域 FQDN，對應到集區所在 Active Directory 網域的網域名稱部分。因此，當此屬性沒有值時，前端集區 FQDN 將預設為 Active Directory 網域名稱結構 (如 <strong>dnsHostName</strong> 屬性所表示)。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-PoolFunctionality</p></td>
<td><p>這是多重值清單，列出所有與集區相關聯之 Lync Server Enterprise Edition 伺服器的網域名稱。此整數型別的屬性會定義集區是否具有立即訊息 (IM)、顯示狀態和會議功能。</p>
<p>可能的有效值型別如下：</p>
<ul>
<li><p>未定義：IM 和目前狀態服務 (Live Communications Server 2005 和 2003)</p></li>
<li><p>1: IM 和目前狀態服務 (Lync Server)</p></li>
<li><p>2: IM、顯示狀態和會議服務 (Lync Server)</p></li>
</ul></td>
<td><p>Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-PoolType</p></td>
<td><p>此屬性會指定伺服器集區執行的是 Standard Edition 伺服器還是 Enterprise Edition 伺服器。此屬性是整數型別的位元遮罩值。每個選項由一個位元代表。</p>
<p>有效值 (和相關聯的位元位置) 如下：</p>
<ul>
<li><p>1: Standard Edition 伺服器，裝載使用者 (位元位置 0)</p></li>
<li><p>2: Enterprise Edition 伺服器，裝載使用者 (位元位置 1)</p></li>
<li><p>4: Standard Edition 伺服器，裝載應用程式 (位元位置 2)</p></li>
<li><p>8: Enterprise Edition 伺服器，裝載應用程式 (位元位置 3)</p></li>
</ul>
<p>由於 Lync Server 不支援只裝載應用程式的集區，因此，有效值如下：</p>
<ul>
<li><p>5: Standard Edition 伺服器，裝載使用者和應用程式 (位元位置 0 和 2)</p></li>
<li><p>10: Enterprise Edition 伺服器，裝載使用者和應用程式 (位元位置 1 和 3)</p></li>
</ul></td>
<td><p>Live Communications Server 2005 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-PoolVersion</p></td>
<td><p>此屬性定義集區版本。它是會隨著每個主要產品版本遞增的整數型別。</p>
<p>可能的有效值型別如下：</p>
<ul>
<li><p>0: Live Communications Server 2003</p></li>
<li><p>1: Live Communications Server 2005</p></li>
<li><p>2: Live Communications Server 2005 含 SP1</p></li>
<li><p>3: Office Communications Server 2007</p></li>
<li><p>4: Office Communications Server 2007 R2</p></li>
<li><p>5: Lync Server 2010</p></li>
</ul></td>
<td><p>Live Communications Server 2005 含 SP1.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-PresenceFlags</p></td>
<td><p>此屬性包含定義顯示狀態設定的選項和旗標。</p></td>
<td><p>Office Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-PresencePolicy</p></td>
<td><p>此屬性包含顯示狀態原則物件的 DN。</p></td>
<td><p>Office Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-PrimaryHomeServer</p></td>
<td><p>此屬性讓使用者或連絡人可以使用 SIP 訊息。它會加入至連絡人類別，因為在中央樹系拓撲中，連絡人物件 (非使用者物件) 已啟用 SIP。</p>
<p>有效值為 Standard Edition Server 的 DN，或使用者所在之 Enterprise Edition 前端集區的 DN。</p></td>
<td><p>Live Communications Server 2005 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-PrimaryUserAddress</p></td>
<td><p>此屬性包含特定使用者的 SIP 位址。</p></td>
<td><p>-</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-PrivateLine</p></td>
<td><p>此屬性包含專用線路裝置的裝置 ID。</p></td>
<td><p>Lync Server 2010 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-Routable</p></td>
<td><p>此屬性是布林屬性，用於決定 Lync Server 是否已獲得授權，可使用其 GRUU 位址路由到此服務。如果此值設為 <strong>TRUE</strong>，即授權 Lync Server 路由到此服務。如果此值設為 <strong>FALSE</strong>，則 Lync Server 未獲授權路由到此服務。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-RouteUsageAttribute (過時的)</p></td>
<td><p>此單一值 UNICODE 字串屬性定義用以決定電話路由使用方式是否符合資格的屬性。電話路由的選擇是視兩個元素而定：指派給電話路由的使用方式屬性以及呼叫者允許的原則使用方式屬性。系統選取的電話路由，是其使用方式屬性與呼叫者允許的使用方式相符的第一個電話路由。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p>
<p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-RouteUsageLinks (過時的)</p></td>
<td><p>此多重值辨別名稱 (DN) 屬性包含路由使用方式的辨別名稱清單。</p>
<p>Forward link:<strong>連結 ID 11032</strong></p>
<p>此屬性是對應反向連結 <strong>msRTCSIP-PhoneRouteBL</strong> 的前導連結。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-RoutingPoolDN</p></td>
<td><p>此屬性包含 DN，此 DN 會指向所有 SIP 流量要到此 MCU 或信任服務時必須經過的集區。</p></td>
<td><p>Office Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-RuleName (過時的)</p></td>
<td><p>此單一值 UNICODE 字串屬性指定正規化規則的易記名稱，以方便系統管理員參考。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p>
<p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-SchemaVersion</p></td>
<td><p>此屬性代表組織目前部署的架構版本。</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-SearchMaxRequests (過時的)</p></td>
<td><p>當使用者使用 Communicator 搜尋連絡人時，此屬性限制從目錄搜尋傳回的搜尋結果數。此屬性將覆寫由用戶端所提供的值。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-SearchMaxResults (過時的)</p></td>
<td><p>此屬性會限制傳回之搜尋要求的數目。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-ServerBL</p></td>
<td><p>此多重值屬性是包含辨別名稱 (DN) 清單的反向連結。這些 DN 會指向集區或 <strong>TrustedService</strong> 物件。</p>
<p>此屬性對應到前導連結 <strong>msRTCSIP-TrustedServiceLinks</strong>。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-ServerData</p></td>
<td><p>此屬性保留供未來使用。</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-ServerReferenceBL (過時的)</p></td>
<td><p>此多重值屬性包含辨別名稱清單。這些辨別名稱是反向連結，會參考其他可接受指派而具有預設位置設定檔的伺服器物件。</p>
<p>Back link:<strong>連結 ID 11037</strong></p>
<p>此反向連結的對應前導連結為 <strong>msRTCSIP-DefaultLocationProfileLink</strong>。</p>
<p>此反向連結屬性只會參考集區和中繼伺服器。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p>
<p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-ServerVersion</p></td>
<td><p>此屬性定義伺服器的版本資訊。此版本號碼會套用到所有伺服器角色。這是會隨著每個正式產品版本而一再重複遞增的整數。</p>
<p>可能的有效值如下：</p>
<ul>
<li><p>未定義：Live Communications Server 2003</p>
<p>                 Live Communications Server 2005</p>
<p>                 Live Communications Server 2005 含 SP1</p></li>
<li><p>3: Office Communications Server 2007</p></li>
<li><p>4: Office Communications Server 2007 R2</p></li>
<li><p>5: Lync Server 2010</p></li>
<li><p>6: Lync Server 2013</p></li>
</ul></td>
<td><p>Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-SourceObjectType</p></td>
<td><p>此整數型別的單一值屬性指定 <strong>msDS-SourceObjectDN</strong> 所指物件的型別，如下所示：</p>
<ul>
<li><p>null | 0x00000001:代表來自不同樹系的 Windows NT Server 主體使用者物件</p></li>
<li><p>下列屬性代表來自不同樹系的群組類型，以用於通訊群組擴充：</p>
<ul>
<li><p>0x00000002：ADS_GROUP_TYPE_GLOBAL_GROUP</p></li>
<li><p>0x00000004：ADS_GROUP_TYPE_DOMAIN_LOCAL_GROUP</p></li>
<li><p>0x00000004：ADS_GROUP_TYPE_LOCAL_GROUP</p></li>
<li><p>0x00000008：ADS_GROUP_TYPE_UNIVERSAL_GROUP</p></li>
<li><p>0x80000000：ADS_GROUP_TYPE_SECURITY_ENABLED</p></li>
<li><p>0x90000000：代表來自相同樹系或不同樹系的自動語音應答或訂戶存取物件</p></li>
</ul></li>
</ul></td>
<td><p>Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-SubscriptionAuthRequired (過時的)</p></td>
<td><p>-</p></td>
<td><p>Live Communications Server 2003 的新增項目。</p>
<p>在 Live Communications Server 2005 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-TargetHomeServer</p></td>
<td><p>此屬性可讓您將使用者或連絡人物件從一個 Lync Server 集區移至另一個。此屬性會加入至連絡人類別，因為在中央樹系拓撲中，連絡人物件 (非使用者物件) 已啟用 SIP。</p>
<p>有效值為使用者即將移動過去之目的地 Standard Edition 伺服器或前端集區的 DN。</p></td>
<td><p>Live Communications Server 2005 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-TargetPhoneNumber (過時的)</p></td>
<td><p>此單一值字串屬性包含電話號碼模式或範圍，以路由到 <strong>msRTCSIP-Gateways</strong> 中定義的指定閘道。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-TargetUserPolicies</p></td>
<td><p>此屬性會為 Lync Server 使用者儲存目標原則的成對的名稱和值。</p></td>
<td><p>Lync Server 2010 的新增項目。</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-TenantId</p></td>
<td><p>此屬性會儲存承租人的唯一識別碼。</p></td>
<td><p>Lync Server 2010 的新增項目。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-Translation (過時的)</p></td>
<td><p>此屬性供 Lync Server 的語音功能使用，而且包含找到相符項目時要對撥號號碼套用的轉譯字串。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p>
<p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-TrustedMCUData</p></td>
<td><p>此屬性保留供未來使用。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-TrustedMCUFQDN</p></td>
<td><p>此屬性是字串值，內含 MCU 的 FQDN。這是單一值屬性。每個區段的有效值為 63 個字元，整個 FQDN 的有效值為 255 個字元。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-TrustedProxyData</p></td>
<td><p>此屬性保留供未來使用。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-TrustedProxyFQDN</p></td>
<td><p>此屬性是字串值，內含執行 Proxy 伺服器之伺服器的 FQDN。此屬性是單一值。每個區段的有效值為 63 個字元，整個 FQDN 的有效值為 255 個字元。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-TrustedServerData</p></td>
<td><p>此屬性保留供未來使用。</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-TrustedServerFQDN</p></td>
<td><p>此屬性是單一值屬性，代表受信任之伺服器的 FQDN。</p></td>
<td><p>Live Communications Server 2005 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-TrustedServerVersion</p></td>
<td><p>此屬性指定受信任伺服器清單中伺服器的版本號碼。</p>
<p>可能的有效值如下：</p>
<ul>
<li><p>NULL：Live Communications Server 2003</p></li>
<li><p>2: Live Communications Server 2005</p></li>
<li><p>3: Office Communications Server 2007</p></li>
<li><p>4: Office Communications Server 2007 R2</p></li>
<li><p>5: Lync Server 2010</p></li>
<li><p>6: Lync Server 2013</p></li>
</ul></td>
<td><p>Live Communications Server 2005 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-TrustedServiceFlags</p></td>
<td><p>此屬性定義已為受信任服務啟用的選項。</p></td>
<td><p>Office Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-TrustedServiceLinks</p></td>
<td><p>此多重值屬性包含辨別名稱 (DN) 清單，這些名稱參考信任服務物件，例如媒體轉送驗證服務。媒體轉送驗證服務 (實體配置在執行音訊/視訊會議服務的 Edge Server 上) 必須與集區相關聯，才能支援遠端使用者的音訊案例。</p>
<p>此前導連結屬性的對應反向連結是 <strong>msRTCSIP-ServerBL</strong>。</p></td>
<td><p>UC</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-TrustedServicePort</p></td>
<td><p>此屬性是一個整數，可定義連線到此 GRUU 服務時所用的連接埠編號。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-TrustedServiceType</p></td>
<td><p>此屬性是字串值，可定義它所代表的 GRUU 服務類型。</p>
<p>有效的 GRUU 服務類型如下：</p>
<ul>
<li><p>MediationServer</p></li>
<li><p>Gateway</p></li>
<li><p>媒體轉送驗證服務 (MRAS)</p></li>
<li><p>QoSM</p></li>
<li><p>msRTCSIP-UserExtension CWA</p></li>
</ul></td>
<td><p>Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-TrustedWebComponentsServerData</p></td>
<td><p>此屬性保留供未來使用。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-TrustedWebComponentsServerFQDN</p></td>
<td><p>此屬性是字串值，內含執行 Lync Server Web 服務之 IIS 的 FQDN。這是單一值屬性。每個區段的有效值為 63 個字元，整個 FQDN 的有效值為 255 個字元。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-UCFlags (過時的)</p></td>
<td><p>此屬性定義為所有使用者或連絡人物件全域啟用的不同 UC 選項。此屬性是整數型別的位元遮罩值。每個選項由一個位元代表。</p>
<p>可能的有效值 (和相關聯的位元位置) 如下：</p>
<ul>
<li><p>4: UsePerUserUCPolicy (位元位置 2)</p></li>
</ul>
<p>設定此位元時，表示是針對各使用者分別定義 UM 原則。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-UCPolicy (過時的)</p></td>
<td><p>此單一值屬性包含系統管理員已為此使用者指派之 UC 原則的辨別名稱 (DN)。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-UserDomainList (過時的)</p></td>
<td><p>此屬性提供裝載 SIP 使用者的樹系中所有網域的清單。預設為空白清單，表示樹系中的所有網域都已啟用 SIP。</p>
<p>有效值為多個字串，代表個別網域的網域名稱。</p></td>
<td><p>Live Communications Server 2005 的新增項目。</p>
<p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-UserEnabled</p></td>
<td><p>此屬性會判斷使用者目前是否已啟用 Lync Server。</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-UserExtension</p></td>
<td><p>此多重值屬性包含成對的名稱和值，格式為「名稱=值」。此屬性是標示要用於「通用類別目錄」複寫。</p></td>
<td><p>Live Communications Server 2005 含 SP1 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-UserLocationProfile</p></td>
<td><p>此屬性包含指向位置設定檔物件的辨別名稱 (DN)。</p></td>
<td><p>Office Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-UserPolicies</p></td>
<td><p>此屬性會儲存使用者原則的成對的名稱和值。</p></td>
<td><p>Lync Server 2010 的新增項目。</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-UserPolicy</p></td>
<td><p>此多重值屬性包含辨別名稱清單，辨別名稱中有二進位 (DN_WITH_BINARY) 指向不同類型的全域使用者原則。二進位部分指示 DN 部分所指的原則類型。</p>
<p>有效二進位值如下：</p>
<ul>
<li><p>0x00000001：會議原則</p></li>
<li><p>0x00000002：UC 原則</p></li>
<li><p>0x00000005：顯示狀態原則</p></li>
</ul></td>
<td><p>Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-UserRoutingGroupId</p></td>
<td><p>這是 SIP 路由群組識別碼。位於相同群組的使用者將會註冊相同的前端伺服器。</p></td>
<td><p>Lync Server 2013 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-WebComponentsData</p></td>
<td><p>這是多重值屬性。此屬性保留供未來使用。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-WebComponentsPoolAddress</p></td>
<td><p>此單一值屬性會指向 Web 元件所屬的集區或 Standard Edition 伺服器。</p>
<p>Forward link:<strong>連結 ID 11028</strong></p>
<p>此前導連結屬性的對應反向連結為 <strong>msRTCSIP-WebComponentsServers</strong>。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-WebComponentsServers</p></td>
<td><p>此屬性是辨別名稱的多重值清單。此屬性包含與此集區相關聯之所有 Web 伺服器的清單。</p>
<p>Back link:<strong>連結 ID 11029</strong></p>
<p>此反向連結的對應前導連結為 <strong>msRTCSIP-WebComponentsPoolAddress</strong>。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-WMIInstanceId (過時的)</p></td>
<td><p>-</p></td>
<td><p>Live Communications Server 2003 的新增項目。</p>
<p>在 Live Communications Server 2005 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>OtherIPPhone</p></td>
<td><p>這個現有的 Active Directory 屬性是由電話語音所使用，以指定電話的替代 TCP/IP 位址清單。</p></td>
<td><p>Windows Server 2008 作業系統的新增功能。</p></td>
</tr>
<tr class="even">
<td><p>PhoneOfficeOther</p></td>
<td><p>這個現有的 Active Directory 屬性供 Lync Server 中的語音元件使用 (只用於連絡人物件)，目的在於將通話路由傳送到整合訊息自動語音應答和訂戶存取號碼。無條件的來電轉接位址就儲存在此多重值屬性中。這個帳戶的建立目的只為用於自動語音應答和訂戶存取。系統管理員不得修改此帳戶的屬性。</p></td>
<td><p>Windows 2000 作業系統的新增功能。</p></td>
</tr>
<tr class="odd">
<td><p>ProxyAddresses</p></td>
<td><p>這個現有的 Active Directory 多重值屬性是 Windows 2000 所引入之基本 Active Directory 架構的一部分。此屬性包含使用者電子郵件的各種 X400、X500 和 SMTP 位址。在 Live Communications Server 2003 (含) 以後版本中，會使用 &quot;sip:&quot; 標記將使用者的 SIP URI 新增到此清單中。</p>
<p>下列應用程式會在此屬性中搜尋使用者的 SIP URI：</p>
<ul>
<li><p>Microsoft Office Outlook 2003 訊息與共同作業用戶端</p></li>
<li><p>Microsoft Office SharePoint Server 2007</p></li>
</ul></td>
<td><p>Windows 2000 作業系統的新增功能。</p></td>
</tr>
<tr class="even">
<td><p>TelephoneNumber</p></td>
<td><p>這個現有的 Active Directory 屬性包含使用者的電話號碼。</p></td>
<td><p>Windows 2000 作業系統的新增功能。</p></td>
</tr>
</tbody>
</table>

