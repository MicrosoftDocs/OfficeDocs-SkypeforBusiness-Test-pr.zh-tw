---
title: Lync 2013 相容性
TOCTitle: Lync 2013 相容性
ms:assetid: ac3a1046-b438-4e21-9d4f-3b0057dd685d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412817(v=OCS.15)
ms:contentKeyID: 52056178
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync 2013 相容性

 

_**上次修改主題的時間：** 2015-03-09_

本節描述 Lync 2013 與各種版本的 Microsoft Office 套件、Microsoft Exchange Server、Windows 作業系統及精選的公用立即訊息 (IM) 用戶端的相容性。

## Office 和 Lync 2013

下表描述各版本 Office 所支援的 Lync 2013 功能。

### Lync 2013 與 Microsoft Office 相容性

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>Microsoft Office 2003 Service Pack 3 (SP3) (必要) 或最新的 Service Pack (建議)。</th>
<th>Microsoft Office 2007</th>
<th>Microsoft Office 2010</th>
<th>Microsoft Office 2013</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>自訂 Outlook 會議邀請 (新增標誌、說明 URL、免責聲明、註腳文字)</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>在 Outlook 中，設定會議選項，將出席者音訊及視訊預設為靜音</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>跨 Office 和 Lync 管理連絡人清單的整合連絡人存放區</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>是 (需要 Exchange 2013)1</p></td>
</tr>
<tr class="even">
<td><p>高解析度圖片</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>是 (需要 Exchange 2013)1</p></td>
</tr>
<tr class="odd">
<td><p>整合至 Office 安裝程式 的 Lync 2013 安裝</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>OneNote 共用記事本</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>PowerPoint 簡報內容</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Outlook [收件者] 和 [副本] 欄位中的目前狀態</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>以顯示狀態功能表中的電話會議回覆</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>是 (從連絡人卡片)</p></td>
<td><p>是 (從連絡人卡片)</p></td>
</tr>
<tr class="even">
<td><p>[排程助理員] 索引標籤上會議邀請中的目前狀態</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>以收到的電子郵件工具列或功能區中的 IM 或電話回覆</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>Outlook [寄件者] 欄位中的目前狀態</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>以顯示狀態功能表中的 IM 或語音回覆</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>是 (從連絡人卡片)</p></td>
<td><p>是 (從連絡人卡片)</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Word 和 Microsoft Excel 檔案 (已啟用智慧標籤) 中的 IM 和目前狀態</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>僅限 Microsoft Word</p></td>
<td><p>僅限 Microsoft Word</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft SharePoint 網站 (必須已安裝 Outlook) 中的 IM 和目前狀態</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
</tbody>
</table>


1 如需詳細資訊，請參閱部署文件中的＜[整合 Microsoft Lync Server 2013 與 Microsoft Exchange Server 2013](lync-server-2013-integrating-with-microsoft-exchange-server-2013.md)＞。

以下功能僅由 Office 2010 或 Office 2013 提供：

  - 連絡人卡片，包含擴充選項，例如視訊通話和桌面共用

  - 從 Outlook 的 \[尋找連絡人\] 欄位執行的快速搜尋

  - 在 \[郵件\]、\[行事曆\]、\[連絡人\] 和 \[工作\] 資料夾中，從 Outlook 的 \[常用\] 功能區以 IM 或電話回覆

  - Outlook \[待辦事項列\] 中的 Lync \[連絡人\] 清單

  - Office Backstage (\[檔案\] 索引標籤) 目前狀態、程式共用和檔案傳輸

  - Microsoft Office SharePoint Workspace 2010 (前身為 Microsoft Office Groove 2007) 中的 \[目前狀態\] 功能表

  - \[目前狀態\] 功能表擴充性

## Exchange Server 和 Lync 2013

下表描述 Lync 2013 對於各版本 Exchange Server 的支援。Outlook 必須安裝到用戶端電腦上，才能處理 Extended MAPI 通話，而且有些功能需要使用 Exchange Web 服務 (EWS)。

### Lync 2013 與 Exchange Server 相容性

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange Server 版本</th>
<th>Lync 2013 支援</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Server 2013</p></td>
<td><p>與 Exchange Server 2010 支援相同，增加了整合連絡人存放區、高解析度圖片，以及封存整合。</p>
<div class="alert">
> [!NOTE]  
> 如需詳細資訊，請參閱＜<a href="lync-server-2013-integrating-with-microsoft-exchange-server-2013.md">整合 Microsoft Lync Server 2013 與 Microsoft Exchange Server 2013</a>＞。


</div></td>
</tr>
<tr class="even">
<td><p>Exchange Server 2010</p></td>
<td><p>與 Exchange Server 2007 支援相同 (加上 Exchange 連絡人同步)</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server 2007 Service Pack 1 (SP1) (必要) 或最新的 Service Pack (建議)。</p></td>
<td><p>以下功能僅由 EWS 提供：</p>
<ul>
<li><p>讀取或刪除 [交談記錄] 資料夾中的項目</p></li>
<li><p>讀取或刪除語音信箱項目</p></li>
<li><p>顯示更詳細的空閒/忙碌資訊和會議主題與地點</p></li>
</ul>
<p>Exchange Server 2007 Service Pack 1 (SP1) (必要) 或最新的 Service Pack 或版本 (建議) 中的公用資料夾是選用的。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server 2003</p></td>
<td><p>僅限 Outlook MAPI。未提供 EWS 專屬功能 (請參閱前列內容)</p></td>
</tr>
</tbody>
</table>


## Windows 和 Lync 2013

如需 Lync 2013 和 Windows 支援的詳細資訊，請參閱規劃文件中的＜[Lync Server 2013 中的 Lync 用戶端軟體支援](lync-server-2013-lync-client-software-support.md)＞。

## Macintosh 和 Lync 2013

Lync Server 2013 支援執行 Macintosh 作業系統之電腦上的某些用戶端。如需詳細資訊，請參閱規劃文件中的＜[Lync Server 2013 中的 Lync 用戶端軟體支援](lync-server-2013-lync-client-software-support.md)＞。

## 公用立即訊息用戶端和 Lync 2013

如果您已將伺服器設定為使用公用 IM 連線，則 Lync 支援下列使用公用 IM 網路的功能。目前狀態已篩選出公用 IM 用戶端支援的目前狀態。如需詳細資訊，請參閱規劃文件中的＜[規劃 Lync Server 2013 中的公用立即訊息連線](lync-server-2013-planning-for-public-instant-messaging-connectivity.md)＞以及作業文件中的＜[在 Lync Server 2013 中管理外部使用存取原則](lync-server-2013-manage-external-access-policy-for-your-organization.md)＞。

此外，Lync Server 2013 的 XMPP 整合功能可讓使用者與使用可延伸傳訊與顯示通訊協定 (例如 Google Talk) 之公用 IM 提供者的使用者交換立即訊息和狀態資訊。如需詳細資訊，請參閱規劃文件中的＜[規劃 Lync Server 2013 中的可延伸的訊息和顯示狀態通訊協定 (XMPP) 同盟](lync-server-2013-planning-for-extensible-messaging-and-presence-protocol-xmpp-federation.md)＞。

### Lync 2013 和 公用 IM 用戶端相容性

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>用戶端</th>
<th>支援的功能</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Live Messenger</p></td>
<td><p>IM、基本目前狀態、音訊/視訊 (A/V)*</p></td>
</tr>
<tr class="even">
<td><p>Skype</p></td>
<td><p>IM、基本目前狀態、音訊</p></td>
</tr>
<tr class="odd">
<td><p>AOL</p></td>
<td><p>IM 和基本目前狀態</p></td>
</tr>
<tr class="even">
<td><p>Yahoo!</p></td>
<td><p>IM 和基本目前狀態</p></td>
</tr>
<tr class="odd">
<td><p>Google Talk</p></td>
<td><p>IM 和基本目前狀態</p></td>
</tr>
</tbody>
</table>


\*最新版 Windows Live Messenger 支援 A/V。如果您透過 Windows Live Messenger 實作音訊/視訊 (A/V) 同盟，您還必須修改伺服器加密層級。根據預設，加密層級為 \[必要\]。您必須使用 Lync Server 管理命令介面將此設定變更為 \[支援\]。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>自 2012 年 9 月 1 日起，Microsoft Lync 公用 IM 連線使用者訂閱授權 (&quot;PIC USL&quot;) 無法再以新合約或續約的方式購買。持有使用中授權的客戶將可繼續與 Yahoo! Messenger 維持同盟關係直至服務終止日。目前已公佈 AOL 與 Yahoo! 在 2014 年 6 月的確切結束日期。如需詳細資訊，請參閱＜<a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Lync Server 2013 中的公用立即訊息連線的支援</a>＞。</p></li>
<li><p>PIC USL 是針對每位使用者的每月訂閱授權，為 Lync Server 或 Office Communications Server 與 Yahoo! Messenger 同盟的必要授權。Microsoft 是否提供此項服務視 Yahoo! 的支援而定，而此基礎合約將告結束。</p></li>
<li><p>更勝以往，Lync 成為連接全世界組織之間以及個人之間的強大工具。除了 Lync 標準 CAL 之外，與 Windows Live Messenger 同盟不需要其他使用者/裝置授權。</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 請參閱

#### 概念

[Lync 2013 中的用戶端互通性](lync-server-2013-client-interoperability-in-lync-2013.md)  
[Lync Server 2013 中的 Lync 用戶端軟體支援](lync-server-2013-lync-client-software-support.md)  
[Lync Server 2013 的 Lync Web App 支援平台](lync-server-2013-lync-web-app-supported-platforms.md)  
[Lync Windows 市集應用程式需求](lync-server-2013-lync-windows-store-app-requirements.md)  

#### 其他資源

[用戶端系統需求](lync-server-2013-client-system-requirements.md)

