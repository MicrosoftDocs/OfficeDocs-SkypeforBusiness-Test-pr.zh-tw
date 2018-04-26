---
title: Lync Server 2013 中的架構類別和描述
TOCTitle: Lync Server 2013 中的架構類別和描述
ms:assetid: 7d43b920-ac37-40cc-adfe-be289bda6e9e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398625(v=OCS.15)
ms:contentKeyID: 49291440
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的架構類別和描述

 

_**上次修改主題的時間：** 2015-03-09_

本節將說明 Lync Server 2013 使用的所有架構類別。

## 架構類別和描述


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>類別</th>
<th>說明</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mail-Recipient</p></td>
<td><p>Exchange 整合通訊 (UM) 電子郵件收件者。</p></td>
<td><p>這是與 Exchange UM 共用的輔助類別。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-ApplicationContacts</p></td>
<td><p>此類別是多個應用程式連絡人的容器，本身不包含任何屬性。</p></td>
<td><p>Microsoft Office Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-ApplicationServer</p></td>
<td><p>此類別包含一個項目，代表整合通訊應用程式服務 (UCAS) 的服務控制點。</p></td>
<td><p>Office Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-ApplicationServerService</p></td>
<td><p>此類別提供從特定集區到其應用程式服務的關聯。</p></td>
<td><p>Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-ApplicationServerSettings</p></td>
<td><p>msRTCSIP-ApplicationServer 的這個輔助類別包含代表 應用程式服務 執行個體設定的屬性。</p></td>
<td><p>Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-Archive (過時的)</p></td>
<td><p>msRTCSIP-GlobalContainer 的這個輔助類別包含與封存相關的所有設定。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-ArchivingServer (過時的)</p></td>
<td><p>此類別代表單一立即訊息封存伺服器。將電腦當做立即訊息封存伺服器 (例如，已安裝「立即訊息封存服務」的電腦) 啟動時，就會建立此類別的執行個體。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-ConferenceDirectories</p></td>
<td><p>此類別是多個會議目錄執行個體的容器，本身不包含任何屬性。</p></td>
<td><p>Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-ConferenceDirectory</p></td>
<td><p>這個類別包含代表特定會議目錄設定的屬性。</p></td>
<td><p>Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-ConnectionPoint</p></td>
<td><p>一般服務控制點 (SCP)，以指定電腦是執行 Lync Server 的伺服器。</p></td>
<td><p>Lync 2010 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-DefaultCWABank</p></td>
<td><p>此輔助類別包含 Microsoft Lync Web App 儲存所的設定。</p></td>
<td><p>Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-Domain</p></td>
<td><p>此類別包含的屬性可定義 SIP 登錄器所設定的網域。</p></td>
<td><p>-</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-EdgeProxy</p></td>
<td><p>此類別容器代表單一 Access Edge Service。因為 Access Edge Service 部署在周邊網路中，而客戶通常不允許來自周邊網路的 Active Directory 網域服務 存取，所以 Access Edge Service 不會加入內部網路的 Active Directory 網路。因此 AD DS 中不會自動註冊存取 Proxy。系統管理員必須手動在 AD DS 中設定每個 Access Edge Service 執行個體。</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-EnterpriseMCUSettings</p></td>
<td><p>msRTCSIP-MCU 的這個輔助類別包含代表會議伺服器設定的屬性。</p></td>
<td><p>Microsoft Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-EnterpriseMediationServerSettings</p></td>
<td><p>msRTCSIP-MediationServer 的這個輔助類別包含代表中繼伺服器設定的屬性。</p></td>
<td><p>Office Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-EnterpriseServerSettings</p></td>
<td><p>msRTCSIP-Server 的這個輔助類別包含代表 SIP 伺服器設定的屬性。</p></td>
<td><p>-</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-Federation</p></td>
<td><p>msRTCSIP-GlobalContainer 的這個輔助類別包含與同盟相關的所有設定。</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-GlobalContainer</p></td>
<td><p>此類別包含適用於整個 Lync Server 部署的所有設定。</p></td>
<td><p>-</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-GlobalUserPolicy (過時的)</p></td>
<td><p>此類別代表單一 Office Communications Server 會議原則。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-GlobalTopologySetting</p></td>
<td><p>本機全域拓撲設定物件。</p></td>
<td><p>Lync Server 2010 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-GlobalTopologySettings</p></td>
<td><p>用以存放全域拓撲設定物件的容器。</p></td>
<td><p>Lync Server 2010 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-LocalNormalization</p></td>
<td><p>此類別是代表一個位置正規化規則執行個體的容器。</p></td>
<td><p>-</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-LocationContactMapping</p></td>
<td><p>此類別由會議服務員應用程式所建立，內含依地區將會議電話號碼分類所使用的屬性。</p></td>
<td><p>Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-LocationContactMappings</p></td>
<td><p>此類別是多個位置連絡人對應執行個體的容器，本身不包含任何屬性。</p></td>
<td><p>Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-LocationProfile</p></td>
<td><p>此類別是代表特定位置設定檔的容器。</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-LocationProfiles (過時的)</p></td>
<td><p>此類別是多個位置設定檔的容器，本身不包含任何屬性。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-LocalNormalizations (過時的)</p></td>
<td><p>此類別是多個本機正規化規則的容器，本身不包含任何屬性。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-MCU</p></td>
<td><p>此類別代表單一會議伺服器。</p></td>
<td><p>Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-MCUFactories</p></td>
<td><p>此類別包含多個 msRTCSIP-MCUFactory 類別，本身不包含任何屬性。</p></td>
<td><p>Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-MCUFactory</p></td>
<td><p>此類別是代表單一媒體類型之會議伺服器中心的容器。每當啟動這個特定類型和廠商的第一個會議伺服器時，就會建立此類別的執行個體。</p></td>
<td><p>Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-MCUFactoryService</p></td>
<td><p>此類別提供從特定集區到其會議伺服器中心的關聯。</p></td>
<td><p>Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-MediationServer</p></td>
<td><p>此類別包含「中繼伺服器」的服務控制點項目。</p></td>
<td><p>Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-Meeting (過時的)</p></td>
<td><p>msRTCSIP-GlobalContainer 的這個輔助類別包含代表可設定會議設定的屬性。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-Mobility</p></td>
<td><p>用以儲存全域行動性設定的容器。</p></td>
<td><p>-</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-MonitoringServer</p></td>
<td><p>此類別包含代表單一監控伺服器相關設定的屬性。</p></td>
<td><p>Communications Server 2007 R2 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-PhoneRoute (過時的)</p></td>
<td><p>此類別是代表一個或一組閘道之最低成本路由執行個體的容器。這項資訊供所有 Enterprise Pool 或執行 Standard Edition 的伺服器，用於將傳出通話以最符合成本效益的方式路由到公用交換電話網路 (PSTN)。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-PhoneRoutes (過時的)</p></td>
<td><p>此類別是多個最低成本路由的容器，本身不包含任何屬性。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-Policies (過時的)</p></td>
<td><p>此類別包含多個 Lync Server 原則類別，本身不包含任何屬性。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-Pool</p></td>
<td><p>此類別代表單一 Lync Server 集區。</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-Pools</p></td>
<td><p>此類別包含多個 Lync Server 集區，本身不包含任何屬性。</p></td>
<td><p>-</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-PoolService</p></td>
<td><p>此類別代表集區的服務控制點連線點。位於集區內的使用者擁有自己的 msRTCSIP-PrimaryHomeServer 屬性，指向此類別的執行個體。</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-Presence</p></td>
<td><p>用以儲存全域顯示狀態設定的容器。</p></td>
<td><p>-</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-Registrar</p></td>
<td><p>msRTCSIP-GlobalContainer 的這個輔助類別包含代表 SIP 登錄器伺服器所維護使用者設定的屬性。</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-RouteUsage (過時的)</p></td>
<td><p>此類別是代表電話路由使用方式執行個體的容器。電話路由使用方式類別由一個屬性欄位和一個描述欄位組成。屬性欄位定義使用方式類型，描述欄位則讓系統管理員能夠描述此屬性在電話路由中的使用方式。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-RouteUsages (過時的)</p></td>
<td><p>此類別包含 msRTCSIP-RouteUsage 類別的多個執行個體，本身沒有任何屬性。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-Search</p></td>
<td><p>msRTCSIP-GlobalContainer 的這個輔助類別，包含限制並控制搜尋結果範圍的屬性。</p></td>
<td><p>-</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-Server</p></td>
<td><p>此類別代表執行 Lync Server 的單一伺服器。</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-Service</p></td>
<td><p>此類別包含全域設定容器和 msRTCSIP-Domain 物件。</p></td>
<td><p>-</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-TrustedMCU</p></td>
<td><p>這個類別包含代表受信任會議伺服器相關設定的屬性。</p></td>
<td><p>Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-TrustedMCUs</p></td>
<td><p>此類別包含 msRTCSIP-TrustedMCU 類別的多個執行個體，本身沒有任何屬性。</p></td>
<td><p>Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-TrustedProxies</p></td>
<td><p>此類別包含多個 msRTCSIP-TrustedProxy 類別，本身不包含任何屬性。</p></td>
<td><p>Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-TrustedProxy</p></td>
<td><p>此類別是代表執行 Proxy 伺服器之伺服器的容器。每當在加入 AD DS 的電腦上啟動新的 Proxy 伺服器時，就會建立此類別的執行個體。</p></td>
<td><p>Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-TrustedServer</p></td>
<td><p>此類別包含代表受信任伺服器相關設定的屬性。</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-TrustedService</p></td>
<td><p>此類別是代表受信任服務的容器，這類服務可使用「可全域路由傳送使用者代理程式 URI」(GRUU) 位址進行路由。每當啟動受 Lync Server 信任的新伺服器時，就會建立此類別的執行個體。這個受信任的伺服器必須加入 Active Directory 網域。</p></td>
<td><p>Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-TrustedServices</p></td>
<td><p>此類別是多部 GRUU 伺服器的容器，本身不包含任何屬性。</p></td>
<td><p>Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-TrustedWebComponentsServer</p></td>
<td><p>此類別包含代表受信任 Web 元件相關設定的屬性。</p></td>
<td><p>Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-TrustedWebComponentsServers</p></td>
<td><p>此類別包含 msRTCSIP-TrustedWebComponentServer 類別的多個執行個體，本身沒有任何屬性。</p></td>
<td><p>Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-UnifiedCommunications (過時的)</p></td>
<td><p>msRTCSIP-GlobalContainer 的這個輔助類別包含與整合通訊相關的屬性。</p></td>
<td><p>在 Lync Server 2010 中已過時。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-WebComponents</p></td>
<td><p>此類別包含 Internet Information Server (IIS) 的服務控制點。它會將伺服器識別為 Web 元件伺服器。</p></td>
<td><p>Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-WebComponentsService</p></td>
<td><p>此類別提供從特定集區到該集區所將使用 Web 元件的關聯。</p></td>
<td><p>Communications Server 2007 的新增項目。</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-WebComponentSettings</p></td>
<td><p>msRTCSIP-WebComponents 的這個輔助類別包含代表 Web 元件相關設定的屬性。</p></td>
<td><p>Communications Server 2007 的新增項目。</p></td>
</tr>
</tbody>
</table>

