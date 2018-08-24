---
title: Lync Server 2013：使用者模型
TOCTitle: Lync Server 2013 使用者模型
ms:assetid: c551371c-d740-4372-bada-f0d713ec0d33
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398811(v=OCS.15)
ms:contentKeyID: 49890302
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的使用者模型

 

_**上次修改主題的時間：** 2015-03-09_

此處描述的使用者模型為 [使用使用者模型針對 Lync Server 2013 規劃容量](lync-server-2013-capacity-planning-using-the-user-models.md)描述的容量規劃方法與建議提供基礎。

## Lync Server 2013 使用者模型

下表描述 Lync Server 2013 中註冊、連絡人、立即訊息 (IM) 和目前狀態的使用者模型。

### 環境和註冊使用者模型

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>類別</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>部署規模與分佈情形</p></td>
<td><p>假設有一個大型部署的模型，其中有三個中央網站，每個網站各一個前端集區。</p></td>
</tr>
<tr class="even">
<td><p>Active Directory 使用者的百分比</p></td>
<td><p>我們假設組織中 70% 的 Active Directory 使用者已啟用 Lync Server。80% 已啟用的使用者每天都會登入 Lync Server (80% 並行)。並行使用者是本節中其餘內容的數據基礎。</p></td>
</tr>
<tr class="odd">
<td><p>Active Directory 變更</p></td>
<td><p>我們假設每週在 Active Directory 中為 Lync 建立和啟用的使用者佔總數的 0.5%，每週從 Active Directory 和 Lync 中停用的使用者佔總數的 0.5%。每週有 5% 的使用者至少變更一個 Active Directory 屬性。</p></td>
</tr>
<tr class="even">
<td><p>Active Directory 通訊群組</p></td>
<td><p>我們假設組織中 Active Directory 通訊群組的數目是 Active Directory 所有使用者的 3 倍。通訊群組的大小包括下列幾種：</p>
<ul>
<li><p>64% 擁有 2-30 位使用者</p></li>
<li><p>13% 擁有 31-50 位使用者</p></li>
<li><p>10% 擁有 51-100 位使用者</p></li>
<li><p>13% 擁有 101-500 位使用者</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>VoIP 使用者</p></td>
<td><p>60% 的 Lync Server 使用者已啟用整合通訊 (UC) (也就是說，其電話號碼為 Lync Server 所擁有)。</p></td>
</tr>
<tr class="even">
<td><p>註冊的用戶端分佈情形</p></td>
<td><p>65% 的用戶端執行 Lync 2013 軟體，包括 Lync 和 Lync Phone Edition。</p>
<p>30% 的用戶端執行舊版 Lync 的用戶端軟體。</p>
<p>5% 的用戶端使用 Lync Web App。</p>
<p>如果啟用行動性，則假設 40% 的使用者同時使用行動性以及其他上述註冊的用戶端項目，且用戶端多點存在 (MPOP) 比率是 1:1.9。如果停用行動性，則 MPOP 比率是 1:1.5。</p></td>
</tr>
<tr class="odd">
<td><p>遠端使用者分佈情形</p></td>
<td><p>70% 的使用者是內部連線。</p>
<p>30% 的使用者透過 Edge Server 與 Director 進行連線。</p></td>
</tr>
<tr class="even">
<td><p>連絡人分佈情形</p></td>
<td><p>使用者擁有的連絡人數目上限為 1,000。不到 1% 的使用者擁有 1,000 個連絡人。不到 25% 的使用者擁有 100 個以上的連絡人。</p>
<p>使用公用雲端連線的使用者平均擁有 80 個連絡人。這些使用者中：</p>
<ul>
<li><p>50% 的連絡人在組織內。這些使用者的 10% 為遠端使用者，從防火牆外部連線。</p></li>
<li><p>40% 的連絡人為公用雲端使用者 (例如 AOL、Yahoo!、MSN 或 Google Talk 使用者)。</p></li>
<li><p>10% 的連絡人來自同盟協力廠商。</p>
<div>

> [!Important]  
> <ul>
> <li><p>自 2012 年 9 月 1 日起，Microsoft Lync 公用 IM 連線使用者訂閱授權 (&quot;PIC USL&quot;) 無法再以新合約或續約的方式購買。持有使用中授權的客戶將可繼續與 Yahoo! Messenger 維持同盟關係直至服務終止日。目前已公佈 AOL 與 Yahoo! 在 2014 年 6 月的結束日期。如需詳細資訊，請參閱 <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Lync Server 2013 中的公用立即訊息連線的支援</a>。</p></li>
> <li><p>PIC USL 是針對每位使用者的每月訂閱授權，為 Lync Server 或 Office Communications Server 與 Yahoo! Messenger 同盟的必要授權。Microsoft 是否提供此項服務視 Yahoo! 的支援而定，而此基礎合約將告結束。</p></li>
> <li><p>更勝以往，Lync 成為連接全世界組織之間以及個人之間的強大工具。除了 Lync Standard CAL 之外，與 Windows Live Messenger 同盟不需要其他使用者/裝置授權。此清單更將加入 Skype 同盟，讓 Lync 使用者可透過 IM 和語音觸及數億位使用者。</p></li>
> </ul>

</div></li>
</ul>
<p>未使用公用雲端連線的使用者平均擁有 50 個連絡人。這些使用者中：</p>
<ul>
<li><p>80% 的連絡人在組織內。這些使用者的 10% 為遠端使用者，從防火牆外部連線。</p></li>
<li><p>20% 的連絡人來自同盟協力廠商。</p>
<p>每個使用者在自己的連絡人清單中有 1 個通訊群組。為了進行效能測試，我們假設通訊群組永遠是展開的。</p></li>
</ul>
<p>使用者有 25% 的連絡人使用 XMPP。</p></td>
</tr>
<tr class="odd">
<td><p>工作階段時間</p></td>
<td><p>使用者登入工作階段平均持續 12 小時。所有使用者都在工作階段啟動後的 120 分鐘內登入。</p></td>
</tr>
</tbody>
</table>


### IM 和目前狀態使用者模型

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>類別</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>對等 IM 工作階段</p></td>
<td><p>每位使用者每天平均使用六個對等 IM 工作階段。</p>
<p>每個工作階段 10 則立即訊息。</p>
<p>每則訊息都對應兩個 SIP INFO 訊息和兩個 SIP 200 OK 訊息 (針對如「&lt;名字&gt; 正在輸入」之類的狀態指示器)</p></td>
</tr>
<tr class="even">
<td><p>目前狀態輪詢</p></td>
<td><p>整體而言，我們假設目前狀態輪詢的頻率為每位使用者每小時平均 60 次輪詢。假設每位使用者平均：</p>
<ul>
<li><p>每天在使用者的組織索引標籤 (不是 [連絡人] 清單) 中的使用者目前狀態會有一次輪詢。在使用者的組織索引標籤中非連絡人的平均數目為 15 個使用者。每天兩次連絡人卡片檢視作業。</p></li>
<li><p>每次使用者點選其他使用者開始交談時一次目前狀態輪詢，預估每小時一次。</p></li>
<li><p>每小時六次使用者搜尋。每次執行搜尋時，會為搜尋結果清單中的每個人傳送批次輪詢。我們假設平均搜尋結果筆數是 20 筆。如果搜尋結果停留在螢幕上，則批次輪詢每 5 分鐘會重新整理一次；我們假設每小時會有兩次這種重新整理動作。</p></li>
<li><p>當使用者在 Outlook 中開啟或預覽電子郵件時，電子郵件的 [收件者:] 和 [副本:] 欄位中有一次使用者目前狀態的輪詢，預估每小時五封電子郵件且每封電子郵件四位使用者。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>目前狀態訂閱</p></td>
<td><p>某一位使用者將另一位使用者加入為連絡人時，表示第一位使用者 <em>「訂閱」</em> (Subscribe) 有關第二位使用者的五種資訊。這五種資訊的更新會自動傳送給第一位使用者。</p>
<p>對於每個用戶端，會傳送單一批次訂閱要求，以取得平均 40 位連絡人的目前狀態 (有額外 40 個對話來獲得同盟連絡人的目前狀態)。</p>
<p>對於展開的通訊群組來說，要查出其成員的目前狀態，是透過常設目前狀態訂閱 (而非輪詢) 進行，且模型設為每位使用者每 2 小時展開 1 次。</p>
<p>「短期訂閱」 發生在：使用者登入，有一個針對使用者所有連絡人的批次訂閱，然後使用者不久就登出。我們假設每位使用者每小時有 6 次短期訂閱，每次訂閱維持 10 分鐘。</p></td>
</tr>
<tr class="even">
<td><p>目前狀態發行</p></td>
<td><p>平均每位使用者每小時發行目前狀態 4 次，最多為每位使用者每小時 6 次。</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>目前狀態文件大小</p></td>
<td><p>完整目前狀態文件的平均大小假設為 4K，最大為 25K。</p></td>
</tr>
</tbody>
</table>


下表描述使用通訊錄的使用者模型。

### 通訊錄使用狀況使用者模型

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>通訊錄搜尋模式</th>
<th>使用狀況</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>僅限通訊錄 Web 查詢 (通訊錄 Web 查詢服務執行的所有查詢)</p></td>
<td><p>每位使用者每天四個前置詞查詢。</p>
<p>每位使用者每天 60 個全字相符查詢。其中 40% 為批次，每個查詢平均包含 20 個連絡人。另外 60% 為單一連絡人查詢。</p>
<p>每位使用者每天 25 次相片查詢。其中 24 次為單一相片查詢，另一次為平均包含 20 個連絡人的批次查詢。</p>
<p>每位使用者每天一次整個組織搜尋。</p></td>
</tr>
<tr class="even">
<td><p>混合模式，同時使用通訊錄檔案和 Web 查詢。這是預設模式。</p></td>
<td><p>只有兩種類型查詢會移至網路，也就是相片和整個組織搜尋查詢。</p>
<p>每位使用者每天 25 次相片查詢。其中 24 次為單一相片查詢，另一次為平均包含 20 個連絡人的批次查詢。</p>
<p>每位使用者每天一次整個組織搜尋。</p></td>
</tr>
</tbody>
</table>


下表描述會議模型。

### 會議模型

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>類別</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>排定的會議與「立即開會」的會議</p></td>
<td><p>60% 為已排程，40% 未排程。</p>
<p>在排程會議中，假設 80% 是指派的會議，亦即經常性會議的個體、10% 是單次公開會議、8% 是單次匿名會議，而 2% 是單次非公開會議。</p></td>
</tr>
<tr class="even">
<td><p>會議用戶端分佈情形</p></td>
<td><p>已排程的會議：</p>
<ul>
<li><p>65% 的會議使用者使用 Lync 2013。</p></li>
<li><p>5% 的會議使用者使用 Microsoft Lync Web App。</p></li>
<li><p>30% 的會議使用者使用舊版用戶端，包括 Microsoft Lync 2010、 Office Communicator 2007 R2、 Office Communicator 2007 和 Microsoft Office Communicator Web Access (2007 版本)。</p></li>
</ul>
<p>未排程的會議：</p>
<ul>
<li><p>70% 的會議使用者使用 Lync 2013。</p></li>
<li><p>30% 的會議使用者使用舊版用戶端，包括 Microsoft Lync 2010、 Office Communicator 2007 R2、 Office Communicator 2007 和 Microsoft Office Communicator Web Access (2007 版本)。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>會議並行</p></td>
<td><p>工作時間內會有 5% 的使用者在開會。因此，在 80,000 位使用者的集區中，多達 4,000 位使用者可能隨時都在開會。</p></td>
</tr>
<tr class="even">
<td><p>會議音訊分佈情形</p></td>
<td><p>40% 混合 VoIP 音訊和電話撥入式會議，其中 VoIP 使用者與電話撥入式使用者的比例為 3:1。</p>
<p>35% 僅使用 VoIP 音訊。</p>
<p>15% 僅使用電話撥入式會議音訊。</p>
<p>10% 無音訊 (僅使用 IM 的會議，其中每位使用者平均傳送五則訊息)。</p></td>
</tr>
<tr class="odd">
<td><p>混合媒體的會議</p></td>
<td><p>75% 的會議為 Web 會議，包括使用音訊加上一些其他共同作業的形式。</p>
<p>這些會議的其他共同作業方法包括：</p>
<div>

> [!NOTE]  
> 這些數字相加超過 100%，因為一場會議可能採用多種共同作業方法。


</div>
<ul>
<li><p>50% 加入應用程式共用。我們假設一位使用者以每秒 1.1 MB 的尖峰頻率傳送資料。</p></li>
<li><p>50% 加入立即訊息 (每位使用者平均 2 則訊息)。</p></li>
<li><p>20% 加入資料共同作業，包括 PowerPoint 或白板。其中每場會議平均使用兩個 PowerPoint 檔案，平均 PowerPoint 檔案大小為 10 MB (無內嵌視訊) 或 30 MB (含內嵌視訊)。每個白板平均有 20 個註釋。</p></li>
<li><p>20% 加入視訊。在這些使用者當中，有 70% 參加啟用多重檢視視訊的會議，其中每位使用者收到 2-3 個視訊資料流。</p></li>
<li><p>15% 加入共用附註。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>會議參與者分佈情形</p></td>
<td><p>50% 為內部驗證的使用者。</p>
<p>25% 為遠端存取的驗證使用者。</p>
<p>15% 為匿名使用者。</p>
<p>10% 為同盟使用者。</p></td>
</tr>
<tr class="odd">
<td><p>會議加入分佈情形</p></td>
<td><p>使用者模擬狀況為會議開始 5 分鐘內就座完畢。</p></td>
</tr>
</tbody>
</table>


在一般前端集區內， Lync Server 2013 支援的會議規模上限為 250 位使用者。每個集區一次可以舉行一場 250 位使用者的會議。這場大型會議舉行的同時，集區還可以舉行其他較小型的會議。此外，您也可以設定專用集區，用來舉行高達 1000 位使用者的會議。如需詳細資訊，請參閱 [Lync Server 2013 中的大型會議支援](lync-server-2013-support-for-large-meetings.md)。

會議模擬條件如下：

  - 85% 的會議有 4 位參與者。

  - 10% 的會議有 6 位參與者。

  - 5% 的會議有 11 位參與者。

  - 一場大型會議，共有 250 位使用者。

下表提供包含電話撥入式使用者之會議使用者模型的詳細資訊。

### 電話撥入式會議使用者模型

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>類別</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>驗證/匿名</p></td>
<td><p>70% 的來電者以匿名身分加入，且系統提示其輸入供記錄的名稱。30% 以通過驗證的使用者身分加入。</p></td>
</tr>
<tr class="even">
<td><p>通話時間和等候音樂</p></td>
<td><p>平均通話時間，不含等候音樂：50 秒。</p>
<p>50% 的通話使用者會聽到平均 5 分鐘的等候音樂。</p></td>
</tr>
<tr class="odd">
<td><p>複頻式 (DTMF)</p></td>
<td><p>15% 的僅限電話撥入式會議有電話主席。10% 包含電話撥入式使用者的混合會議也有電話主席。</p>
<p>20% 的電話主席每場會議使用兩種 DTMF 命令。</p></td>
</tr>
<tr class="even">
<td><p>宣告語言</p></td>
<td><p>模擬使用英文作為宣告語言。</p></td>
</tr>
</tbody>
</table>


下表提供會議大廳的使用者模型詳細資訊。

### 會議大廳使用者模型

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>類別</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>大廳內的使用者人數</p></td>
<td><p>5% 的撥入使用者會經過大廳，25% 的其他使用者會經過大廳。</p></td>
</tr>
<tr class="even">
<td><p>從大廳獲准加入</p></td>
<td><p>在模擬中，所有使用者都在用戶端逾時之前由簡報者核准加入。</p></td>
</tr>
</tbody>
</table>


下表描述其他對等工作階段的使用者模型。

### 對等工作階段使用者模型

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>類別</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>應用程式共用</p></td>
<td><p>每位使用者每個月參與 5 個對等應用程式共用工作階段，每天平均 0.25 個工作階段。</p></td>
</tr>
<tr class="even">
<td><p>檔案傳輸</p></td>
<td><p>每位使用者每個月參與 1 次對等檔案傳輸工作階段 (IM 工作階段的一部分)，每天平均 0.05 個工作階段。平均傳輸的工作階段檔案大小為 1 MB。</p></td>
</tr>
</tbody>
</table>


下表說明原則的使用者模型。

### 原則使用者模型

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>類別</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>會議、目前狀態和封存原則</p></td>
<td><p>我們假設有一個全域原則、10 個標記會議原則、4 個封存原則，以及 10 個標記目前狀態原則。</p></td>
</tr>
<tr class="even">
<td><p>語音原則</p></td>
<td><p>我們假設每個網站有一個全域原則和 2 個標記原則。100% 的網站有網站原則，30% 的使用者被指派使用者層級原則。我們假設每個網站有一個撥號對應表和兩個路由。</p></td>
</tr>
</tbody>
</table>


## 忙碌時段

對等工作階段中，尖峰用量是使用忙碌時段通話嘗試 (BHCA) 計算。此語音業界用語假設當天所有通話的 50% 將在 20% 的時間內結束。使用的計算公式如下：

`BHCA=(total calls * 0.5) / 1.6`

效能測試會以每天至少 1.6 小時的忙碌時段負載執行 VoIP 和其他對等工作階段的方式進行模擬。

會議尖峰用量時段假設所有一天八小時的會議中，有 75% 是在 4 個尖峰時段進行。這些尖峰時段是平均會議用量的 1.5 倍。

## 企業語音打 PSTN 電話

以下為對 企業語音通話的假設：

  - 50% 的使用者啟用 企業語音、其中 60% 的使用者啟用 PSTN 通話。

  - 這每位啟用 PSTN 通話的使用者在忙碌時段撥打 4 通 PSTN 電話，每通電話通話 3 分鐘。

  - 其中 65% 的 PSTN 語音通話使用媒體旁路。

## 行動性

假設有 40% 的註冊使用者啟用行動性。對於每位啟用行動性的使用者，我們假設行動用戶端的活動會累加至該使用者其他 MPOP 執行個體的活動，但是會議互動除外，因為對會議互動來說，行動用戶端只不過是另一種可用來參與會議的用戶端類型。

## 常設聊天室

我們假設 25% 的註冊使用者會進入常設聊天室工作階段，並具有下列特性：

  - 每位使用者平均有 1.5 個聊天室

  - 每個聊天室每小時產生 12 個輪詢要求，每個要求平均以 10 位使用者為目標

## 回應群組和通話駐留

我們假設 0.15% 的註冊使用者屬於回應群組，並假設任何時刻都有 0.02% 的註冊使用者駐留通話。

