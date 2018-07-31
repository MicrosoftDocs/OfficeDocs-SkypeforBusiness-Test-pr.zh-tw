---
title: Lync Server 2013：CDR 表格清單
TOCTitle: CDR 表格清單
ms:assetid: 031843fd-c7ff-4534-9b02-8847aad70807
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398084(v=OCS.15)
ms:contentKeyID: 49289920
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 CDR 表格清單

 

_**上次修改主題的時間：** 2015-03-09_

詳細通話記錄 (CDR) 資料庫結構描述包含下列表格。

## 靜態表格


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>表格</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="lync-server-2013-callpriorities-table.md">Lync Server 2013 中的 CallPriorities 表格</a></p></td>
<td><p>儲存通話可能優先順序的清單 (如「緊急」、「急」、「一般」、「非緊急」等)。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-conferencejointimethresholds-table.md">Lync Server 2013 中的 ConferenceJoinTimeThresholds 表</a></p></td>
<td><p>儲存會議加入時間摘要報告所使用的分類範圍。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-deregistertype-table.md">Lync Server 2013 中的 DeRegisterType 表格</a></p></td>
<td><p>儲存使用者取消註冊可能原因的清單 (如「由用戶端起始」、「註冊到期」或「用戶端損毀」等)。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-medialist-table.md">Lync Server 2013 中的 MediaList 表格</a></p></td>
<td><p>儲存各種媒體類型清單，這些類型會產生資料庫中的項目 (例如 IM、音訊、視訊以及檔案傳輸)。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-purgesettings-table.md">Lync Server 2013 中的 PurgeSettings 表</a></p></td>
<td><p>儲存指定是否要從 CDR 資料庫自動刪除過時詳細通話記錄及何時刪除的資訊。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-roles-table.md">Lync Server 2013 中的 Roles 表格</a></p></td>
<td><p>儲存會議可能角色清單 (例如出席者和簡報者)。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-sipresponsemetadata-table.md">Lync Server 2013 中的 SIPResponseMetaData 表</a></p></td>
<td><p>儲存 SIP 回應碼及這些回應碼的分類和定義清單。</p></td>
</tr>
</tbody>
</table>


## 支援的表格


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>表格</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="lync-server-2013-clientversions-table.md">Lync Server 2013 中的 ClientVersions 表格</a></p></td>
<td><p>儲存通話方之每個用戶端的用戶端 (用戶端類型與版本號碼) 以及此資料庫中擷取的資訊。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-conferenceuris-table.md">Lync Server 2013 中的 ConferenceUris 表格</a></p></td>
<td><p>儲存會議相關通話中所使用的 ConferenceURI 清單。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-contenttypes-table.md">Lync Server 2013 中的 ContentTypes 表格</a></p></td>
<td><p>儲存工作階段初始通訊協定 (SIP) 內容類型清單，這些類型是用於對等式通話和電話會議。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-devices-table.md">Lync Server 2013 中的 Devices 表格</a></p></td>
<td><p>儲存裝置清單 (包括，製造商、硬體版本以及 MAC 位址)。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-dialogs-table.md">Lync Server 2013 中的 Dialogs 表格</a></p></td>
<td><p>儲存資料庫中每個工作階段的對話方塊 ID 相關資訊。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-edgeservers-table.md">Lync Server 2013 中的 EdgeServers 表格</a></p></td>
<td><p>儲存用於撥打外線的 Edge Server 清單。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-gateways-table.md">Lync Server 2013 中的 Gateways 表格</a></p></td>
<td><p>儲存用於 Voice over Internet Protocol (VoIP) 通話的閘道清單。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-hardwareversions-table.md">Lync Server 2013 中的 HardwareVersions 表格</a></p></td>
<td><p>儲存裝置 (電話機) 硬體版本清單。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-manufacturers-table.md">Lync Server 2013 中的 Manufacturers 表格</a></p></td>
<td><p>儲存裝置 (電話機) 製造商清單。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-mcus-table.md">Lync Server 2013 中的 Mcus 表格</a></p></td>
<td><p>儲存各種 A/V 會議伺服器及其 URI 的資訊。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-mediationservers-table.md">Lync Server 2013 中的 MediationServers 表格</a></p></td>
<td><p>儲存用於 VoIP 通話的中繼伺服器清單。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-phones-table.md">Lync Server 2013 中的 Phones 表格</a></p></td>
<td><p>儲存用於已封存或其通話詳細資料已記錄之 VoIP 通話中的所有電話號碼。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-pools-table.md">Lync Server 2013 中的 Pools 表格</a></p></td>
<td><p>儲存擷取 IM 訊息的集區名稱。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-servers-table.md">Lync Server 2013 中的 Servers 表格</a></p></td>
<td><p>儲存通話方的伺服器名稱。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-tenants-table.md">Lync Server 2013 中的 Tenants 表格</a></p></td>
<td><p>儲存目前部署支援的租用戶；包括企業使用者、同盟使用者、公共 IM 連線使用者以及匿名使用者的部分內建租用戶。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-useragentdef-table.md">Lync Server 2013 中的 UserAgentDef 表</a></p></td>
<td><p>將使用者代理程式識別碼對應至代理程式的描述性名稱。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-users-table.md">Lync Server 2013 中的 Users 表格</a></p></td>
<td><p>儲存資料庫中所記錄或封存的工作階段之使用者的使用者 URI。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-userstatistics-table.md">Lync Server 2013 中的 UserStatistics 表</a></p></td>
<td><p>儲存個別使用者使用系統之情況的資訊。</p></td>
</tr>
</tbody>
</table>


## 會議 CDR 記錄特有表格


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>表格</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="lync-server-2013-conferences-table.md">Lync Server 2013 中的 Conferences 表格</a></p></td>
<td><p>儲存已封存或其詳細資料已記錄之所有會議的資訊，包括 ConferenceURI，以及開始時間和結束時間。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-conferencesessiondetails-table.md">Lync Server 2013 中的 ConferenceSessionDetails 表格</a></p></td>
<td><p>儲存每個 SIP 型會議工作階段的相關資訊，包括每個工作階段的開始時間和結束時間、使用者識別碼、回應碼以及診斷 ID。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-focusjoinsandleaves-table.md">Lync Server 2013 中的 FocusJoinsAndLeaves 表格</a></p></td>
<td><p>儲存會議加入和離開的相關資訊，包括使用者的角色和用戶端版本。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-mcujoinsandleaves-table.md">Lync Server 2013 中的 McuJoinsAndLeaves 表格</a></p></td>
<td><p>儲存參與會議的 A/V 會議伺服器以及使用者加入或離開時間之資訊。</p></td>
</tr>
</tbody>
</table>


## IM 會議中的訊息表格


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>表格</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="lync-server-2013-conferencemessagecount-table.md">Lync Server 2013 中的 ConferenceMessageCount 表格</a></p></td>
<td><p>針對每個 IM 會議，儲存每個使用者所傳送的訊息數目。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-imreportsummary-table.md">Lync Server 2013 中的 IMReportSummary 表</a></p></td>
<td><p>提供組織內所保留之立即訊息工作階段的整體報告。</p></td>
</tr>
</tbody>
</table>


## 對等工作階段表格


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>表格</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="lync-server-2013-sessiondetails-table.md">Lync Server 2013 中的 SessionDetails 表格</a></p></td>
<td><p>儲存每個對等工作階段的資訊，包括每個使用者的開始時間和結束時間、使用者識別碼、回應碼以及訊息計數。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-filetransfers-table.md">Lync Server 2013 中的 FileTransfers 表格</a></p></td>
<td><p>儲存檔案傳輸工作階段的資訊，包括檔案名稱和結果 (接受、拒絕或取消)。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-media-table.md">Lync Server 2013 中的媒體資料表格</a></p></td>
<td><p>儲存與對等工作階段相關之不同媒體類型的資訊。</p></td>
</tr>
</tbody>
</table>


## VoIP 通話詳細資訊的表格


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>表格</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="lync-server-2013-voipdetails-table.md">Lync Server 2013 中的 VoipDetails 表格</a></p></td>
<td><p>會針對每次雙方 VoIP/PSTN 通話，儲存通話的相關資訊，例如 VoIP 電話的電話 ID、所用閘道，以及哪一方中斷連線。請參考 <a href="lync-server-2013-sessiondetails-table.md">Lync Server 2013 中的 SessionDetails 表格</a> 以取得通話開始/結束時間與回應碼。</p>
<div class="alert">

> [!NOTE]  
> 如果通話任一方是 VoIP 使用者或者有中繼伺服器參與通話，此表格中會建立一筆記錄。 <a href="lync-server-2013-sessiondetails-table.md">Lync Server 2013 中的 SessionDetails 表格</a> 中會擷取不參與公用交換電話網路 (PSTN) 電話的 VoIP/VoIP 通話之相關資訊。


</div></td>
</tr>
</tbody>
</table>


## E9-1-1 通話稽核表格


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>表格</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="lync-server-2013-locations-table.md">Lync Server 2013 中的 Locations 表格</a></p></td>
<td><p>會針對每個緊急電話，如增強型 9-1-1 (E9-1-1) 通話，儲存通話的位置資訊。請參考 <a href="lync-server-2013-sessiondetails-table.md">Lync Server 2013 中的 SessionDetails 表格</a> 以取得通話開始/結束時間與回應碼。</p>
<div class="alert">

> [!NOTE]  
> 此表格僅包含針對 E9-1-1 通話的位置二進位大型物件。請參考 SessionDetails 表格以取得通話的其他詳細資訊。


</div></td>
</tr>
</tbody>
</table>


## 疑難排解表格


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>表格</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="lync-server-2013-application-table.md">Lync Server 2013 中的應用程式表</a></p></td>
<td><p>儲存 Lync Server 2013 中與路由及連線相關之各種程序的資訊。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-calltype-table.md">Lync Server 2013 中的 CallType 表格</a></p></td>
<td><p>儲存通話類型的資訊，例如「音訊」、「立即訊息」、「音訊和視訊」以及「應用程式共用」。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-errorcategory-table.md">Lync Server 2013 中的 ErrorCategory 表</a></p></td>
<td><p>儲存每個 Microsoft Lync Server 2013 診斷分類的易記名稱。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-errordef-table.md">Lync Server 2013 中的 ErrorDef 表格</a></p></td>
<td><p>儲存錯誤類型與其定義的相關資訊。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-errorreport-table.md">Lync Server 2013 中的 ErrorReport 表格</a></p></td>
<td><p>儲存所發生錯誤的相關資訊。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-progressreport-table.md">Lync Server 2013 中的 ProgressReport 表格</a></p></td>
<td><p>儲存與 Lync Server 2013 程序相關之各種步驟的進度報告資訊。</p></td>
</tr>
</tbody>
</table>


下列清單列出供 Lync Server 內部使用的表格。本文件不提供其詳細資料。

## Lync Server 內部使用的表格


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>表格</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DbConfigDateTime</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="even">
<td><p><strong>DbConfigInt</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DbErrorMessage</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="even">
<td><p><strong>FrontEnd 表格</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MSMQProcessing 表格</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="even">
<td><p><strong>SummaryTableConfiguration</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Syndicators 表格</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="even">
<td><p><strong>SyndicatorsTenantMap 表格</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Task 表格</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="even">
<td><p><strong>UserStatistics</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UsageSummary_UQ</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="even">
<td><p><strong>UsageSummary</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DaylightSavingYears</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="even">
<td><p><strong>TimeZoneConfiguration</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="odd">
<td><p><strong>TimeZones</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="even">
<td><p><strong>FailureSummary_UQ</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FailureSummary</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="even">
<td><p><strong>ServerSummary</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MsDiagMetaData</strong></p></td>
<td><p>僅限內部使用。</p></td>
</tr>
</tbody>
</table>

