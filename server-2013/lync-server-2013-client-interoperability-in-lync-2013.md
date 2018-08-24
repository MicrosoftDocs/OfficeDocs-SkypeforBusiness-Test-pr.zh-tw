---
title: Lync Server 2013：Lync 2013 中的用戶端互通性
TOCTitle: Lync 2013 中的用戶端互通性
ms:assetid: 0f126571-91a2-45d5-855c-1e4ddb45fc04
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204672(v=OCS.15)
ms:contentKeyID: 49290099
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync 2013 中的用戶端互通性

 

_**上次修改主題的時間：** 2015-03-09_

本主題說明 Microsoft Lync Server 2013 用戶端與舊版 Lync Server 和 Office Communications Server 用戶端並存及互動的能力。

## 伺服器與用戶端相容性

下表顯示可支援的用戶端版本與伺服器版本組合。此表格指出當用戶端嘗試連線到所指定的伺服器時，是否支援登入。Lync Server 2013 支援先前的用戶端版本。此外，與舊版不同的是，Lync Server 2010 可支援新的 Lync 2013 用戶端。這樣可以讓從 Lync Server 2010 升級的組織執行新的用戶端，而不需要 Lync Server 升級。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>用戶端</th>
<th>Lync Server 2013</th>
<th>Lync Server 2010</th>
<th>Office Communications Server 2007 R2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Lync 2013</p></td>
<td><p>支援</p></td>
<td><p>支援5</p></td>
<td><p>不支援</p></td>
</tr>
<tr class="even">
<td><p>Lync 2013 Basic</p></td>
<td><p>支援</p></td>
<td><p>支援</p></td>
<td><p>不支援</p></td>
</tr>
<tr class="odd">
<td><p>Lync Web App 2013</p></td>
<td><p>支援</p></td>
<td><p>不支援</p></td>
<td><p>不支援</p></td>
</tr>
<tr class="even">
<td><p>Lync 2010</p></td>
<td><p>支援</p></td>
<td><p>支援</p></td>
<td><p>不支援</p></td>
</tr>
<tr class="odd">
<td><p>Lync 2010 Attendant</p></td>
<td><p>支援</p></td>
<td><p>支援</p></td>
<td><p>不支援</p></td>
</tr>
<tr class="even">
<td><p>Lync 2010 群組聊天</p></td>
<td><p>支援1</p></td>
<td><p>支援2</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="odd">
<td><p>Lync Web App 2010</p></td>
<td><p>不支援</p></td>
<td><p>支援</p></td>
<td><p>不支援</p></td>
</tr>
<tr class="even">
<td><p>Lync 2010 Attendee</p></td>
<td><p>不支援3</p></td>
<td><p>支援</p></td>
<td><p>不支援</p></td>
</tr>
<tr class="odd">
<td><p>Office Communicator 2007 R2</p></td>
<td><p>可互通4</p></td>
<td><p>支援</p></td>
<td><p>支援</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Office Communications Server 2007 R2 Attendant</p></td>
<td><p>不支援</p></td>
<td><p>支援</p></td>
<td><p>支援</p></td>
</tr>
<tr class="odd">
<td><p>Office Communicator 2007</p></td>
<td><p>不支援</p></td>
<td><p>支援</p></td>
<td><p>支援</p></td>
</tr>
<tr class="even">
<td><p>Office Live Meeting 2007</p></td>
<td><p>不支援</p></td>
<td><p>支援</p></td>
<td><p>支援</p></td>
</tr>
<tr class="odd">
<td><p>Lync Windows 市集應用程式</p></td>
<td><p>支援</p></td>
<td><p>支援</p></td>
<td><p>不支援</p></td>
</tr>
</tbody>
</table>


1如需詳細資訊，請參閱＜[從 Lync Server 2010 群組聊天或 Office Communications Server 2007 R2 群組聊天移轉至 Lync Server 2013 常設聊天室伺服器](migration-from-lync-server-2010-group-chat-or-office-communications-server-2007-r2-group-chat-to-lync-server-2013-persistent-chat-server.md)＞。

2Microsoft Lync Server 2010 可利用群組聊天伺服器提供群組聊天功能，此為 Lync Server 2010 適用的協力廠商信任應用程式。Lync 2013 用戶端與 Lync Server 2010 群組聊天不相容。

3Lync Web App 2013 現在提供完整的會議參與經驗，包括電腦音訊與視訊，且被視為可取代 Lync 2010 Attendee。Lync 2010 Attendee 只有當您使用不支援的瀏覽器 (Internet Explorer 6 或 Internet Explorer 7) 和 Windows XP 時才會連接到 Lync Server 2013。

4Office Communicator 2007 R2 的目前狀態和 IM 功能可與 Lync Server 2013 相容，但會議功能則不相容。從 Office Communications Server 2007 R2 移轉的期間，Office Communicator 2007 R2 適用於目前狀態和 IM 互通性，但使用者應該使用 Lync Web App 2013 加入 Lync Server 2013 會議。

5 有關限制，請參閱本主題稍後的＜Lync Server 2010 會議中對於 Lync 2013 用戶端的會議功能支援＞。

## 用戶端之間的互通性

透過 Lync Server 2013 版本，各種用戶端版本都可以在對等及會議案例中緊密互動。本節討論當使用者與使用不同用戶端及伺服器版本的其他使用者互動時，功能的可用性。

## 對等功能支援

針對安置在不同伺服器版本以及使用不同用戶端版本的使用者，可支援對等功能。使用者經驗及可用功能，與使用者用戶端以及使用者登入之伺服器版本的功能一致。換句話說：

  - 如果使用者以較舊的用戶端登入 Lync Server 2013，使用者的經驗會和以前一樣。在使用者的用戶端升級前，都無法使用 Lync Server 2013 中引進的新功能。範例包括視訊圖庫檢視、HD 視訊、PowerPoint 共用，以及進入會議時將所有出席者的音訊視訊靜音的選項。新功能概述於 [Lync Server 2013 中的新會議功能](lync-server-2013-new-conferencing-features.md)和 [Lync Server 2013 中的用戶端最新訊息](lync-server-2013-what-s-new-for-clients.md)。

  - 如果使用者以 Lync 2013 用戶端登入 Lync Server 2010，在使用者移到 Lync Server 2013 之前，Lync Server 2010 不支援的任何新功能都無法使用。

下表是用戶端登入 Lync Server 2013 或 Lync Server 2010 時，對等工作階段中的功能可用性比較。

> [!NOTE]  
> Lync Web App 和 Lync 2010 Attendee 是僅限會議功能的用戶端，不包含在此表格中。




<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>用戶端</th>
<th>立即訊息</th>
<th>目前狀態</th>
<th>語音</th>
<th>視訊</th>
<th>應用程式共用</th>
<th>檔案傳輸</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Lync 2013</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>Lync 2013 Basic</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>Lync 2010</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>Lync 2010 Attendant</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Lync 2010 Mobile</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Lync Phone Edition</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Office Communicator 2007 R2</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是1</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>公用 IM (AOL、Yahoo!)</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>公用 IM (MSN、Windows Live Messenger)</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


> [!Important]  
> <li><p>自 2012 年 9 月 1 日起，Microsoft Lync 公用 IM 連線使用者訂閱授權 (&quot;PIC USL&quot;) 無法再以新合約或續約的方式購買。持有使用中授權的客戶將可繼續與 Yahoo! Messenger 維持同盟關係直至服務終止日。目前已公佈 AOL 與 Yahoo! 在 2014 年 6 月的結束日期。如需詳細資訊，請參閱 <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Lync Server 2013 中的公用立即訊息連線的支援</a>。</p></li>
> <li><p>PIC USL 是針對每位使用者的每月訂閱授權，為 Lync Server 或 Office Communications Server 與 Yahoo! Messenger 同盟的必要授權。Microsoft 是否提供此項服務視 Yahoo! 的支援而定，而此基礎合約將不再續約。</p></li>
> <li><p>Lync 更勝以往成為連接全世界組織之間以及個人之間的強大工具。除了 Lync Standard CAL 之外，與 Windows Live Messenger 同盟不需要其他使用者/裝置授權。此清單更將加入 Skype 同盟，讓 Lync 使用者可透過 IM 和語音觸及數億位使用者。</p></li>
> </ul>


1 在 Office Communicator 2007 R2 中，只能使用桌面共用 (而無法使用程式共用)。

## Lync Server 2010 會議中對於 Lync 2013 用戶端的會議功能支援

當使用者以 Lync 2013 用戶端加入 Lync Server 2010 會議時，他們便能夠存取 Lync 2013 用戶端功能，但有以下例外：

  - 在 **\[參與者\]** 管理選項中 (其可透過指向會議視窗中的人員圖示來存取)，**\[無會議 IM\]** 選項無法作用。

  - 「圖庫檢視」在視訊會議中無法作用。使用者只會看見目前發言者，不會看見所有發言者。在 **\[挑選版面配置\]** 選項的清單中，**\[圖庫檢視\]** 無法使用

  - 參與者清單預設會顯示在視訊會議中。

  - 以滑鼠右鍵按一下參與者清單中的使用者時，**\[鎖定視訊焦點\]** 與 **\[固定至圖庫\]** 參與者管理選項無法使用。

## Lync Server 2013 會議中的會議功能支援

使用者的帳戶必須移至 Lync Server 2013 並以 Lync 2013 用戶端登入後，使用者才能使用 Lync Server 2013 提供的新會議功能。範例包括視訊圖庫檢視、HD 視訊、PowerPoint 共用，以及進入會議時將所有出席者的音訊視訊靜音的選項。新功能概述於 [Lync Server 2013 中的新會議功能](lync-server-2013-new-conferencing-features.md)和 [Lync Server 2013 中的用戶端最新訊息](lync-server-2013-what-s-new-for-clients.md)。

在 Lync Server 2013 會議中，可針對位在不同版本伺服器及使用不同用戶端和用戶端版本的使用者，支援部分會議功能。當用戶端加入 Lync Server 2013 會議時，使用者可以存取此表格中顯示的特性和功能。


<table style="width:100%;">
<colgroup>
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
</colgroup>
<thead>
<tr class="header">
<th>用戶端</th>
<th>對等 IM</th>
<th>語音</th>
<th>視訊</th>
<th>應用程式共用</th>
<th>PowerPoint</th>
<th>檔案傳輸</th>
<th>白板</th>
<th>輪詢</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Lync 2013</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>Lync 2013 Basic</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>Lync Web App</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是2</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>Lync 2010</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是3</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>Office Communicator 2007 R24</p></td>
<td><p>是</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


1 在 Office Communicator 2007 R2 中，只能使用桌面共用 (而無法使用程式共用)。

2Lync Server 2013 會使用更新的機制來上傳 PowerPoint 檔案。加入原本排定在 Lync Server 2010 上之會議的 Lync Web App 使用者，可以檢視及瀏覽 PowerPoint 簡報，但不能上傳 PowerPoint 檔案。

3 如果會議排定在 Lync Server 2013 上，而 PowerPoint 投影片是由 Lync 2013 用戶端上傳，Lync 2010 使用者就只有投影片的檢視存取權。相反地，如果 PowerPoint 投影片是由 Lync 2010 使用者上傳，Lync Server 2013 使用者將能夠檢視和移動投影片，而如果已設定 Office Web Apps Server，使用者就能存取新功能，例如以更高解析度顯示、動畫、投影片轉場以及內嵌視訊。如需更多資訊，請參閱＜[設定 Office Web Apps Server 與 Lync Server 2013 的整合](lync-server-2013-enabling-office-web-apps-server-and-lync-server-2013.md)＞。

4Office Communicator 2007 R2 的目前狀態和 IM 功能可與 Lync Server 2013 相容，但會議功能則不相容。從 Office Communications Server 2007 R2 移轉的期間， Office Communicator 2007 R2 適用於目前狀態和 IM 互通性，但使用者應該使用 Lync Web App 2013 加入 Lync Server 2013 會議。

## 排程增益集支援

對各種排程增益集的伺服器支援，與伺服器和用戶端版本相容性一致。一般而言，在 Lync Server 2013 上可支援下列排程增益集。不過，舊版增益集沒有提供新的 Lync 2013 增益集功能，例如在進入會議時，將所有出席者影音靜音的選項。

  - **Lync 2013 的線上會議增益集**   所提供的功能與 Lync 2010 的線上會議增益集相同，但增加了出席者靜音控制項，可讓會議召集人排定依預設將出席者影音靜音的會議。系統管理員也可以自訂組織的會議邀請函，增加自訂標誌、支援 URL、法律免責聲明 URL 或自訂頁尾文字等。

  - **Lync 2010 的線上會議增益集**   提供 Lync 會議的排程，以及移除排定 Office Live Meeting 會議的功能。

  - **Office Communicator 2007 R2 會議增益集**   提供 Office Live Meeting 會議及 Office Communicator 2007 R2 會議的排程。

> [!NOTE]  
> Live Meeting 會議不能排定在 Lync Server 2013 上。




<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>排程用戶端</th>
<th>Lync Server 2013</th>
<th>Lync Server 2010</th>
<th>Office Communications Server 2007 R2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Lync 2013 的線上會議增益集 (可搭配使用 Office 2013、Outlook 2010 及 Outlook 2007)</p></td>
<td><p>支援</p></td>
<td><p>支援 (無法使用新增益集功能)</p></td>
<td><p>不支援</p></td>
</tr>
<tr class="even">
<td><p>Lync 2013 Web 排程器</p></td>
<td><p>支援</p></td>
<td><p>不支援</p></td>
<td><p>不支援</p></td>
</tr>
<tr class="odd">
<td><p>Lync 2010 的線上會議增益集</p></td>
<td><p>支援</p></td>
<td><p>支援</p></td>
<td><p>不支援</p></td>
</tr>
<tr class="even">
<td><p>Office Communicator 2007 R2 會議增益集</p></td>
<td><p>不支援</p></td>
<td><p>支援</p></td>
<td><p>支援</p></td>
</tr>
</tbody>
</table>


## 支援加入會議

Lync Server 2013 支援的所有用戶端都可以加入 Lync 2013 會議。因為 Lync Web App 是伺服器的 Web 元件 (在使用 Lync Web App 來加入 Lync Server 2013 會議的情況下)，所以一律使用較新版的 Lync Web App。

Lync 2013 用戶端可以加入在具有縮小規模功能的 Lync 2010 和 Office Communications Server 2007 R2 上舉辦的會議。會議中功能受限於舉辦會議所在的伺服器版本。

## 請參閱

#### 概念

[Lync Windows 市集應用程式需求](lync-server-2013-lync-windows-store-app-requirements.md)  
[Lync Server 2013 中的新會議功能](lync-server-2013-new-conferencing-features.md)  
[Lync Server 2013 中的用戶端最新訊息](lync-server-2013-what-s-new-for-clients.md)

