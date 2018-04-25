---
title: Lync Server 2013：對等工作階段詳細資料報告
TOCTitle: 對等工作階段詳細資料報告
ms:assetid: 6be1d676-68f7-4a53-a72a-de73296c5571
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg558659(v=OCS.15)
ms:contentKeyID: 49291226
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的對等工作階段詳細資料報告

 

_**上次修改主題的時間：** 2015-03-09_

對等工作階段詳細資料報告會傳回有關對等工作階段的詳細資訊。例如，如果您選取立即訊息工作階段，報告會告訴您工作階段中兩名使用者中的各自傳送的訊息數目。

## 存取對等工作階段詳細資料報告

對等工作階段詳細資料報告可從任何下列報告存取 (所有這些報告皆可從 \[監控報告\] 的首頁存取)：

  - IP 電話清查報告

  - 使用者活動報告

  - 通話許可控制服務報告

  - 失敗清單報告

您可以在對等工作階段詳細資料報告中，按一下 \[診斷報告 (詳細資料)\] 計量以存取 [Lync Server 2013 中的診斷報告](lync-server-2013-diagnostic-report.md)。您也可以按一下以下兩個計量來存取最大失敗報告：

  - 回應

  - 診斷識別碼

## 充分利用對等工作階段詳細資料報告

對等工作階段詳細資料報告包括大量的計量資料，許多這些資料可能不為系統管理員所熟悉。不過您可以常常將滑鼠停留在計量標籤上，以檢視可提供該計量簡短說明的工具提示。

請注意，顯示於特定報告上的實際計量將依您選取的對等工作階段類型而定。音訊/視訊工作階段會回報一組與立即訊息工作階段不同的計量。

您也可以將滑鼠停留在回應代碼和診斷 ID 計量上，以取得那些值的描述：

## 篩選器

無。您無法篩選對等工作階段詳細資料報告無法篩選。

## 工作階段資訊公制

下表列出了對等工作階段詳細資料報告所提供之每個工作階段的資訊。

### 工作階段資訊公制

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>名稱</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>集區 FQDN</strong></p></td>
<td><p>本工作階段所涉及的登錄器集區或 Edge Server 的完整網域名稱 (FQDN)。</p></td>
</tr>
<tr class="even">
<td><p><strong>邀請時間</strong></p></td>
<td><p>本工作階段邀請最初發送的日期與時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>回應時間</strong></p></td>
<td><p>收到接受邀請的日期與時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>來源使用者</strong></p></td>
<td><p>啟動工作階段之使用者的 SIP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><strong>來源使用者代理程式</strong></p></td>
<td><p>啟動工作階段之使用者端點所用的軟體。</p></td>
</tr>
<tr class="even">
<td><p><strong>是來源使用者內部</strong></p></td>
<td><p>指出起始工作階段的使用者是否登入內部網路。</p></td>
</tr>
<tr class="odd">
<td><p><strong>是與電話機整合的來源使用者</strong></p></td>
<td><p>指出起始工作階段之使用者所用的端點是否整合了使用者的電話機。</p></td>
</tr>
<tr class="even">
<td><p><strong>工作階段優先順序</strong></p></td>
<td><p>指派給工作階段的優先順序。有效的優先順序為：未知；非急迫；一般；急迫；緊急狀況。</p></td>
</tr>
<tr class="odd">
<td><p><strong>回應碼</strong></p></td>
<td><p>工作階段失敗時所傳送的 SIP 回應碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>前端</strong></p></td>
<td><p>會議中所用到的前端伺服器名稱。</p></td>
</tr>
<tr class="odd">
<td><p><strong>擷取時間</strong></p></td>
<td><p>記錄此工作階段資訊的日期和時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>結束時間</strong></p></td>
<td><p>工作階段結束的日期和時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>目標使用者</strong></p></td>
<td><p>獲邀加入工作階段之使用者的 SIP 位址。</p></td>
</tr>
<tr class="even">
<td><p><strong>目標使用者代理程式</strong></p></td>
<td><p>獲邀加入工作階段之使用者端點所使用的軟體。</p></td>
</tr>
<tr class="odd">
<td><p><strong>是目標使用者內部</strong></p></td>
<td><p>指出獲邀加入工作階段的使用者是否登入內部網路。</p></td>
</tr>
<tr class="even">
<td><p><strong>是與電話機整合的目標使用者</strong></p></td>
<td><p>指出獲邀加入工作階段之使用者所用的端點是否整合了使用者的電話機。</p></td>
</tr>
<tr class="odd">
<td><p><strong>是重試的工作階段</strong></p></td>
<td><p>指出此工作階段是否為先前重試工作階段的嘗試。</p></td>
</tr>
<tr class="even">
<td><p><strong>診斷識別碼</strong></p></td>
<td><p>附加在 SIP 訊息中的唯一識別碼 (採用 ms-diagnostics 標頭的格式)，常可以在疑難排解錯誤時提供實用的資訊。將滑鼠游標移至識別碼上方，就可以查看該識別碼的其他相關資訊。</p></td>
</tr>
</tbody>
</table>


## 形式的計量

下表列出對等工作階段詳細資料報告所提供之每個工作階段形式的資訊。

### 形式的計量

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>名稱</th>
<th>可以排序這個項目嗎？</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>形式</strong></p></td>
<td><p>否</p></td>
<td><p>本工作階段所採用的形式。例如，立即訊息 (IM) 或檔案傳輸。</p></td>
</tr>
<tr class="even">
<td><p><strong>來源使用者訊息</strong></p></td>
<td><p>否</p></td>
<td><p>起始工作階段之使用者所傳送的訊息數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>目標使用者訊息</strong></p></td>
<td><p>否</p></td>
<td><p>獲邀加入工作階段之使用者所傳送的訊息數。</p></td>
</tr>
</tbody>
</table>


## 診斷報告的計量

下表列出對等工作階段詳細資料報告所提供之每份診斷報告的資訊。

### 診斷報告的計量

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>名稱</th>
<th>可以排序這個項目嗎？</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>詳細資料</strong></p></td>
<td><p>否</p></td>
<td><p>按一下此項目，報告就會顯示該工作階段的診斷報告。</p></td>
</tr>
<tr class="even">
<td><p><strong>報告時間</strong></p></td>
<td><p>否</p></td>
<td><p>報告的記錄日期與時間</p></td>
</tr>
<tr class="odd">
<td><p><strong>要求</strong></p></td>
<td><p>否</p></td>
<td><p>SIP 要求類型。例如，INVITE 或 BYE。</p></td>
</tr>
<tr class="even">
<td><p><strong>診斷識別碼</strong></p></td>
<td><p>否</p></td>
<td><p>附加在 SIP 訊息中的唯一識別碼 (採用 ms-diagnostics 標頭的格式)，常可以在疑難排解錯誤時提供實用的資訊。</p></td>
</tr>
<tr class="odd">
<td><p><strong>內容類型</strong></p></td>
<td><p>否</p></td>
<td><p>會議中使用的媒體內容類型。常見的內容類型如 Application/sdp。工作階段描述通訊協定 (SDP) 是用於工作階段宣告、工作階段邀請、以及其他形式之多媒體工作階段邀請的標準網際網路通訊協定。</p></td>
</tr>
<tr class="even">
<td><p><strong>報告者</strong></p></td>
<td><p>否</p></td>
<td><p>回報問題的電腦 (也就是用戶端或伺服器)。</p></td>
</tr>
</tbody>
</table>

