---
title: Lync 2013 新增及變更的設定
TOCTitle: Lync 2013 新增及變更的設定
ms:assetid: bb13789c-7eda-461c-a387-02ea8ca4dabe
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205204(v=OCS.15)
ms:contentKeyID: 49292153
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync 2013 新增及變更的設定

 

_**上次修改主題的時間：** 2015-03-09_

本主題討論與用戶端管理直接相關的 Lync Server 管理命令介面 Cmdlet。Lync Server 2013 引進數個新參數，取代可透過其他方法設定之功能的參數。

## 新的用戶端管理參數


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>新參數</th>
<th>Lync Server 管理命令介面 Cmdlet</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TracingLevel</p></td>
<td><p>CsClientPolicy</p></td>
<td><p>設為 True 時，會在 Lync 中啟用軟體追蹤; 設為 False 時，則會停用軟體追蹤。軟體追蹤包括對程式進行的所有事項 (包括追蹤 API 呼叫) 持續詳細記錄，追蹤對於開發人員和應用程式支援人員很有用。此設定等同於 Communications Server 2007 R2 群組原則設定 [開啟 Communicator 的追蹤功能]。設定如下：</p>
<ul>
<li><p>關 = 停用追蹤，且使用者無法變更此設定。</p></li>
<li><p>輕 = 執行最小追蹤，且使用者無法變更此設定。</p></li>
<li><p>開 = 執行詳細追蹤，且使用者無法變更此設定。</p></li>
</ul>
<p>TracingLevel 預設是設為 null 值。這表示執行最小追蹤，但使用者可以啟用或停用此最小追蹤。</p></td>
</tr>
<tr class="even">
<td><p>EnableMediaRedirection</p></td>
<td><p>CsClientPolicy</p></td>
<td><p>設為 True ($True) 時，允許從其他網路流量區隔開音訊和視訊資料流，進而允許用戶端裝置在本機執行音訊和視訊的編碼和解碼。媒體重新導向通常可降低頻寬使用量、提高伺服器延展性，以及更理想的使用者經驗 (相較於裝置遠端或轉碼器壓縮等類似技術)。</p></td>
</tr>
<tr class="odd">
<td><p>AllowLargeMeetings</p></td>
<td><p>CsConferencing</p></td>
<td><p>設為 True 時，所有 Lync Meeting 都將視同「大型會議」。大型會議會對傳送給參與者的通知數目設有限制，此外預設傳輸的會議名冊大小也有限制。</p></td>
</tr>
<tr class="even">
<td><p>DisablePowerPointAnnotations</p></td>
<td><p>CsConferencing</p></td>
<td><p>設為 True ($True) 時，使用者無法新增註釋至會議使用的 PowerPoint 投影片。不過 (依 AllowAnnotations 屬性值而定)，使用者仍然可以存取其他白板功能。預設值為 False，代表允許新增 PowerPoint 註釋。</p></td>
</tr>
<tr class="odd">
<td><p>AllowSharedNotes</p></td>
<td><p>CsConferencing</p></td>
<td><p>設為 True (預設值) 時，任何連結到會議的開啟 OneNote 筆記本都會自動更新會議參與者和會議中共用內容等詳細資訊。</p></td>
</tr>
<tr class="even">
<td><p>EnableInviteCustomization</p></td>
<td><p>CsMeetingConfiguration</p></td>
<td><p>與其他新 CsMeetingConfiguration 參數一起使用，可自訂 Lync 2013 的線上會議增益集所產生的會議邀請。</p></td>
</tr>
<tr class="odd">
<td><p>LogoURL</p></td>
<td><p>CsMeetingConfiguration</p></td>
<td><p>新增組織標誌至 Lync 2013 的線上會議增益集產生的所有邀請。請指定 GIF 或 JPG 影像的 URL。</p></td>
</tr>
<tr class="even">
<td><p>HelpURL</p></td>
<td><p>CsMeetingConfiguration</p></td>
<td><p>新增組織的說明或支援 URL 至 Lync 2013 的線上會議增益集產生的所有邀請。</p></td>
</tr>
<tr class="odd">
<td><p>LegalURL</p></td>
<td><p>CsMeetingConfiguration</p></td>
<td><p>新增法律聲明文字或免責聲明文字至 Lync 2013 的線上會議增益集產生的所有邀請。請指定文字位置的 URL。</p></td>
</tr>
<tr class="even">
<td><p>CustomFooterText</p></td>
<td><p>CsMeetingConfiguration</p></td>
<td><p>新增自訂頁尾至 Lync 2013 的線上會議增益集產生的所有邀請。請指定自訂頁尾文字位置的 URL。</p></td>
</tr>
<tr class="odd">
<td><p>IsPublicDisclosureAllowed</p></td>
<td><p>CsWebServiceConfiguration</p></td>
<td><p>啟用 Lync Web App 的新 2013 版本。Lync Web App 的新版本預設不會啟用，且必須由系統管理員啟用。</p></td>
</tr>
</tbody>
</table>


## 被取代的用戶端管理參數


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>Lync Server 管理命令介面 Cmdlet</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EnableSQMData</p></td>
<td><p>CsClientPolicy</p></td>
<td><p>Lync Server 2013 已移除 Set-CSClientPolicy Cmdlet 的 EnableSQMData 參數，請改為使用軟體品質管理 (SQM) 資料的共用群組原則設定，來決定 Lync 用戶端 [一般] 選項頁面中 [客戶經驗改進] 選項的使用者介面：</p>
<p>HKEY_CURRENT_USER\Software\Policies\Microsoft\Office\Common\QMEnable</p>
<p>值：</p>
<p>1 = 顯示並選取核取方塊 (使用者可以清除核取方塊)</p>
<p>0 = 關閉並停用核取方塊 (使用者無法覆寫)</p>
<p>Null = 此值由 Ofice 設定決定，並顯示核取方塊給使用者以供設定</p></td>
</tr>
<tr class="even">
<td><p>AllowExchangeContactStore</p></td>
<td><p>CsClientPolicy</p></td>
<td><p>此參數已移除。當您部署 Lync Server 2013 並發行拓撲時，現在預設會為所有使用者啟用整合的連絡人存放區。這表示使用者的所有連絡人都保存在 Exchange 中，並可用於 Lync、Outlook 及 Outlook Web Access。您可使用 Set-CsUserServicesPolicy Cmdlet 來自訂哪些使用者可以使用整合的連絡人存放區。您可以啟用全域的使用者、依網站啟用、依租用戶啟用，也可以依個人或個人群組來啟用。如需詳細資訊，請參閱 <a href="lync-server-2013-enable-users-for-unified-contact-store.md">在 Lync Server 2013 中為使用者啟用整合連絡人存放區</a>。</p></td>
</tr>
<tr class="odd">
<td><p>MAPIPollInterval</p></td>
<td><p>CsClientPolicy</p></td>
<td><p>Lync 2013 未使用此參數。在舊版中，此參數指定用戶端從 Exchange 公用資料夾擷取 MAPI 資料的頻率</p></td>
</tr>
</tbody>
</table>

