---
title: Lync Server 2013：SQL Server 資料和記錄檔位置
TOCTitle: SQL Server 資料和記錄檔位置
ms:assetid: 67aa525b-8aa3-474f-827e-8e1d4697f30f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398479(v=OCS.15)
ms:contentKeyID: 49291172
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 的 SQL Server 資料和記錄檔位置

 

_**上次修改主題的時間：** 2015-03-09_

基於效能考量，針對 Lync Server 2013前端集區規劃及部署 Microsoft SQL Server 2012 或 Microsoft SQL Server 2008 R2 SP1 期間的重點，是將資料及記錄檔放入實體硬碟中。建議的磁碟設定是使用 6 個主軸實作 1+0 RAID 集。利用 Lync Server 部署精靈將 前端集區使用的所有資料庫與記錄檔，以及相關聯的伺服器角色與服務 (也就是 封存與監控伺服器、 Lync Server 回應群組服務、 Lync Server 通話駐留服務) 放入 RAID 磁碟集，這樣可產生經測試之後效能良好的設定。下表詳述資料庫檔案及其負責內容。

> [!NOTE]  
> 如果您的原則和 SQL Server 設定需要更多特殊安裝，可使用 Lync Server 管理命令介面將資料庫與記錄檔安裝至任何預先定義的位置。如需詳細資訊，請參閱＜ <a href="lync-server-2013-database-installation-using-lync-server-management-shell.md">在 Lync Server 2013 中使用 Lync Server 管理命令介面安裝資料庫</a>＞。



### 中央管理存放區的資料及記錄檔

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>中央管理存放區資料庫檔案</th>
<th>資料檔案或記錄檔目的</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Xds.ldf</p></td>
<td><p>中央管理存放區的交易記錄檔</p></td>
</tr>
<tr class="even">
<td><p>Xds.mdf</p></td>
<td><p>維護目前 Lync Server 2013 拓撲的設定 (如 拓撲產生器所定義及發行)</p></td>
</tr>
<tr class="odd">
<td><p>Lis.mdf</p></td>
<td><p>位置資訊服務資料檔案</p></td>
</tr>
<tr class="even">
<td><p>Lis.ldf</p></td>
<td><p>位置資訊服務資料檔案的交易記錄檔</p></td>
</tr>
</tbody>
</table>


### 使用者、會議及通訊錄的資料及記錄檔

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>核心 Lync Server 2013 資料庫檔案</th>
<th>資料檔案或記錄檔目的</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Rtc.mdf</p></td>
<td><p>持續性使用者資訊 (例如，存取控制清單 (ACL)、連絡人、排程會議)</p></td>
</tr>
<tr class="even">
<td><p>Rtc.ldf</p></td>
<td><p>Rtc 資料的交易記錄檔</p></td>
</tr>
<tr class="odd">
<td><p>Rtcdyn.mdf</p></td>
<td><p>維護暫時性使用者資料 (目前狀態執行階段資料)</p></td>
</tr>
<tr class="even">
<td><p>Rtcdyn.ldf</p></td>
<td><p>Rtcdyn 資料的交易記錄檔。</p></td>
</tr>
<tr class="odd">
<td><p>Rtcab.mdf</p></td>
<td><p>即時通訊 (RTC) 通訊錄資料庫是儲存通訊錄服務資訊的 SQL Server 存放庫</p></td>
</tr>
<tr class="even">
<td><p>Rtcab.ldf</p></td>
<td><p>通訊錄服務的交易記錄檔</p></td>
</tr>
<tr class="odd">
<td><p>Rtclocal.mdb</p></td>
<td><p>裝載會議目錄</p></td>
</tr>
<tr class="even">
<td><p>Rtcxds.mdf</p></td>
<td><p>維護使用者資料的備份</p></td>
</tr>
<tr class="odd">
<td><p>Rtcxds.ldf</p></td>
<td><p>Rtcxds 資料的交易記錄檔</p></td>
</tr>
</tbody>
</table>


### 通話駐留及回應群組的資料及記錄檔

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>應用程式資料庫</th>
<th>資料檔案或記錄檔目的</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cpsdyn.mdf</p></td>
<td><p>通話駐留應用程式的動態資訊資料庫</p></td>
</tr>
<tr class="even">
<td><p>Cpsdyn.ldf</p></td>
<td><p>通話駐留應用程式資料檔案的交易記錄檔</p></td>
</tr>
<tr class="odd">
<td><p>Rgsconfig.mdf</p></td>
<td><p>服務設定的 Lync Server 回應群組服務資料檔案</p></td>
</tr>
<tr class="even">
<td><p>Rgsconfig.ldf</p></td>
<td><p>回應群組應用程式設定的交易記錄檔</p></td>
</tr>
<tr class="odd">
<td><p>Rgsdyn.mdf</p></td>
<td><p>執行階段作業的回應群組服務資料檔案</p></td>
</tr>
<tr class="even">
<td><p>Rgsdyn.ldf</p></td>
<td><p>回應群組服務執行階段資料檔案的交易記錄檔</p></td>
</tr>
</tbody>
</table>


### 封存和監控伺服器的資料及記錄檔

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>封存及監控資料庫檔案</th>
<th>資料檔案或記錄檔目的</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>LcsCdr.mdf</p></td>
<td><p>監控伺服器之詳細通話記錄 (CDR) 程序的資料存放區</p></td>
</tr>
<tr class="even">
<td><p>LcsCdr.ldf</p></td>
<td><p>詳細通話記錄 (CDR) 資料的交易記錄檔</p></td>
</tr>
<tr class="odd">
<td><p>QoEMetrics.mdf</p></td>
<td><p>從 監控伺服器儲存的經驗品質資料檔案</p></td>
</tr>
<tr class="even">
<td><p>QoEMetrics.ldf</p></td>
<td><p>監控資料的交易記錄檔</p></td>
</tr>
<tr class="odd">
<td><p>Lcslog.mdf</p></td>
<td><p>將立即訊息和會議資料保留在 封存伺服器的資料檔</p></td>
</tr>
<tr class="even">
<td><p>Lcslog.ldf</p></td>
<td><p>封存資料的交易記錄檔</p></td>
</tr>
</tbody>
</table>


在本主題中，會參考磁碟及 RAID 集。請注意，在 SQL Server 資源的設定中，參考磁碟表示單一硬體裝置。含有兩個分割 (一個分割保留記錄檔，而另一個分割保留資料檔案) 的單一硬碟與兩個磁碟 (各專用於記錄檔或資料檔案) 不同。

關於 RAID 集，有數個來自不同廠商的不同 RAID 技術。而且，隨著存放區域網路 (SAN) 的數量擴增，專用於單一系統的 RAID 集日益罕見。您應洽詢 RAID 或 SAN 廠商，以決定在使用 Lync Server 2013 設定 SQL Server 效能時的最佳磁碟配置設定。

也請注意，磁碟機的設計並非完全相同；部分磁碟機的效能可能會優於其他磁碟機。因為轉速、硬體快取大小及其他因素，即使是相同製造商的磁碟機，效能也可能不同。

