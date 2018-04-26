---
title: Lync Server 2013 中的重要狀態指示器
TOCTitle: 海報：重要狀態指示器
ms:assetid: 8367dccf-adaa-4a0b-a4ed-bc9570cc5e24
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn593599(v=OCS.15)
ms:contentKeyID: 61084822
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的重要狀態指示器

 

_**上次修改主題的時間：** 2015-03-09_

本文為[重要狀態指示器：維持健全 Lync Server 的基礎](http://go.microsoft.com/fwlink/?linkid=391838) (英文) 海報的伴隨參考文件，您可從「下載中心」下載此海報。

![描述使用 KHI 資料疑難排解的海報](images/Dn594589.b6fe82bd-d70f-4c1f-a812-b615ac5fa7d7(OCS.15).jpg "描述使用 KHI 資料疑難排解的海報")

您可以使用此海報了解「重要狀態指示器」(KHI)，這是目的在找出使用者體驗問題的臨界值效能計數器。收集 KHI 資料通常是實作「通話品質方法」(CQM) 的第一步，其專注於確保 Lync 使用者能夠獲得高品質的聲音體驗。

如果您有關於使用 CQM 的疑問，您可將問題提交至 cqmfeedback@microsoft.com。

海報描述下列方面：

  - 什麼是「重要狀態指示器」？

  - 收集 KHI 資料

  - 所有伺服器角色的補救措施流程

  - 詞彙

  - 前端伺服器

  - 後端 SQL Server

  - 中繼伺服器

  - Edge Server

## 什麼是「重要狀態指示器」？

「重要狀態指示器」是目的在找出使用者體驗問題的臨界值效能計數器。收集 KHI 資料通常是實作「通話品質方法」(CQM) 的第一步，其專注於確保 Lync 使用者能夠獲得高品質的聲音體驗。

KHI 是標準 Lync 監控解決方案 (例如 System Center Operations Manager、綜合交易、監控伺服器) 以外的輔助工具，但不會取代這些解決方案。

收集 KHI 效能計數器並填入網路指南隨附的 KHI 試算表可產生計分卡，其將協助您判定 Lync 部署的伺服器狀況。填入之後，它會引導您修復環境，並讓您深入了解其他專案關係人。請每月評估一次 KHI 並將其納入任何部署的進行中操作程序。

下載 [Lync Server 網路指南](http://go.microsoft.com/fwlink/p/?linkid=390677)了解 KHI 的完整清單並取得相關的試算表。

## 收集 KHI 資料

1.  在每一部 Lync Server 上執行《Lync Server 網路指南》隨附的 KHI 指令碼。這將會在 \[效能監視器\] 內建立 \[資料收集器\] 並將其命名為 KHI。資料預設將每 15 秒輪詢一次。

2.  公司每天開始工作之前，請前往每部 Lync Server 並啟動 \[KHI 資料收集器\]。

3.  每天結束時，請停止 \[KHI 資料收集器\] 並將資料複製到中央位置。

4.  使用 \[效能監視器\] 填入《Lync Server 網路指南》下載所隨附的 KHI 試算表之後，請將結果與建議目標進行比較。

## 所有伺服器角色的補救措施流程

對於 Lync 實作中的每一部伺服器，請從確認伺服器元件的狀況與系統效能皆處於或高於所需層級開始。只有在此之後，您才應該查看與伺服器在整體 Lync 實作中的角色相關的指示器。

請從為所有伺服器收集「KHI 效能資料」開始。針對每一個系統角色 (在本文稍後有詳細討論) 判定基本系統元件是否符合建議目標。如果不符合，請修正系統效能，然後重新收集 KHI 資料，並確保系統狀況，再查看伺服器在 Lync 實作中之角色的特定計量。所有角色的元件狀況定義如下：

  - CPU 使用量 \< 80%

  - 平均磁碟寫入 \< 10 ms

  - 平均磁碟讀取 \< 10 ms

  - 可用記憶體 \>20% 系統的 MB 總數

  - 網路佇列長度 \< 2

  - 捨棄的封包 (入 / 出) = 0

## 詞彙

在此海報中使用了下列字詞與縮寫：

AS MCU = Application Sharing Multi-point Control Unit (應用程式共用多點控制設備)

AV MCU = Audio/Video MCU (音訊/視訊 MCU)

IM MCU = Instant Messaging MCU (即時訊息 MCU)

UCWA = Unified Communications Web API (整合通訊 Web API)

AV Edge = Traversal of audio/video via edge (透過 Edge 進行的音訊/視訊周遊)

AV Auth = Audio/Video Authentication (音訊/視訊驗證)

SIP Stack = Contains Lync’s core SIP implementation (包含 Lync 的核心 SIP 實作)

Data Proxy = Used for edge conferencing (用於Edge 會議)

LySS = Lync Storage Service (Lyunc 儲存服務)

## 前端伺服器

除了基本元件狀況以外，下列建議的 KHI 目標為前端伺服器所專屬：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>部門</th>
<th>目標計量</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AS/AV/IM MCU</p></td>
<td><p>MCU 狀況 &lt;2</p></td>
</tr>
<tr class="even">
<td><p>Web 元件</p></td>
<td><p>通訊群組清單 擴充 AD 逾時 &lt;0</p>
<p>ABWQ 失敗 = 0</p>
<p>LIS 失敗 = 0</p>
<p>驗證錯誤 &lt; 1/秒</p>
<p>拒絕的 ASP.NET v4 要求 = 0</p></td>
</tr>
<tr class="odd">
<td><p>SIP 堆疊</p></td>
<td><p>平均內送郵件處理 &lt; 1 秒</p>
<p>捨棄的內送回應 &lt; 1/秒 捨棄的內送要求 &lt; 1/秒</p>
<p>佇列延遲 &lt; 100 ms</p>
<p>Sproc 延遲 &lt; 100 ms</p>
<p>調整流速的要求 = 0</p>
<p>驗證錯誤 &lt; 1/秒</p>
<p>內送訊息逾時 &lt; 2</p>
<p>平均內送訊息保留 &lt; 1 秒</p>
<p>流動控制的連線 &lt; 2</p>
<p>平均輸出佇列延遲 &lt; 2 秒</p></td>
</tr>
<tr class="even">
<td><p>LySS</p></td>
<td><p>Storage Service DB 所使用的空間百分比 &lt; 80</p>
<p>複本複寫失敗數 = 0</p>
<p>資料遺失事件數 = 0</p></td>
</tr>
<tr class="odd">
<td><p>SQL</p></td>
<td><p>頁面生命預期 &gt; 300 秒</p>
<p>批次要求 / 秒 &lt; 2500</p></td>
</tr>
</tbody>
</table>


## 後端 SQL 伺服器

除了基本元件狀況以外，下列建議的 KHI 目標為 SQL Server 所專屬：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>部門</th>
<th>目標計量</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SQL</p></td>
<td><p>頁面生命預期 &gt; 300 秒</p>
<p>批次要求 / 秒 &lt; 2500</p></td>
</tr>
</tbody>
</table>


## 中繼伺服器

除了基本元件狀況以外，下列建議的 KHI 目標為中繼伺服器所專屬：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>部門</th>
<th>目標計量</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>中繼伺服器服務</p></td>
<td><p>載入呼叫失敗索引 = 0</p>
<p>由於 Proxy 所造成的失敗呼叫 &lt;10</p>
<p>由於閘道所造成的失敗呼叫 &lt;10</p>
<p>拒絕的呼叫 (入或出) = 0</p>
<p>遺失的媒體候選項目 = 0</p>
<p>媒體連接檢查失敗 = 0</p></td>
</tr>
</tbody>
</table>


## Edge Server

除了基本元件狀況以外，下列建議的 KHI 目標為 Edge Server 所專屬：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>部門</th>
<th>目標計量</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AV 驗證</p></td>
<td><p>錯誤的要求 &lt; 20/秒</p></td>
</tr>
<tr class="even">
<td><p>AV Edge</p></td>
<td><p>驗證失敗 &lt;20/秒</p>
<p>分派失敗 &lt;20/秒</p>
<p>捨棄的封包 &lt;300/秒</p></td>
</tr>
<tr class="odd">
<td><p>資料 Proxy</p></td>
<td><p>調整流速的伺服器連線 &lt; 3</p>
<p>正在調整流速的系統 &lt;1</p></td>
</tr>
<tr class="even">
<td><p>SIP 堆疊</p></td>
<td><p>捨棄的超過限制連線 &lt; 1</p>
<p>傳送逾時 &lt;10</p>
<p>流動控制的連線 &lt;100</p>
<p>捨棄的內送要求 &lt; 1/秒</p>
<p>平均訊息處理 &lt; 3 秒</p></td>
</tr>
</tbody>
</table>


## 請參閱

#### 其他資源

[Lync Server 網路指南](http://go.microsoft.com/fwlink/p/?linkid=390677)  
[重要狀態指示器：維持健全 Lync Server 的基礎](http://go.microsoft.com/fwlink/?linkid=391838)  
[Lync 通話品質方法](http://go.microsoft.com/fwlink/?linkid=391841)

