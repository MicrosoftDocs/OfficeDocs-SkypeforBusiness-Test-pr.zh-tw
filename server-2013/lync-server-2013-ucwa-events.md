---
title: UCWA 事件
TOCTitle: UCWA 事件
ms:assetid: 26cb409d-f4e4-43c7-873f-b694702d491d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945621(v=OCS.15)
ms:contentKeyID: 52056076
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# UCWA 事件

 

_**上次修改主題的時間：** 2015-03-09_

    The information in this topic pertains to Cumulative Updates for Lync Server 2013: February 2013.

Lync Server 2013 在多個用途上都會使用 Unified Communications Web API (UCWA)，例如在搜尋連絡人時存取 Microsoft Exchange，或更新行動用戶端的目前狀態。

UCWA 會以資訊、警告及錯誤事件類型寫入操作行為的記錄。下表說明 UCWA 元件會寫入的事件。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>事件識別碼</th>
<th>事件類型</th>
<th>摘要</th>
<th>原因與解決方式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>20001</p></td>
<td><p>資訊</p></td>
<td><p>UCWA 已初始化</p></td>
<td><p>不適用</p>
<p>不適用</p></td>
</tr>
<tr class="even">
<td><p>20002</p></td>
<td><p>錯誤</p></td>
<td><p>UCWA 在初始化期間發生未預期的例外狀況</p></td>
<td><p>在初始化期間發生未預期的錯誤</p>
<p>在相關的事件記錄項目中檢查例外狀況詳細資料以判斷可能的原因</p></td>
</tr>
<tr class="odd">
<td><p>20003</p></td>
<td><p>錯誤</p></td>
<td><p>UCWA 發生未處理的例外狀況</p></td>
<td><p>發生未處理的例外狀況</p>
<p>重新啟動伺服器。如果問題持續發生，請連絡產品支援</p></td>
</tr>
<tr class="even">
<td><p>20004</p></td>
<td><p>錯誤</p></td>
<td><p>無法針對 HD 相片存取 Exchange</p></td>
<td><p>Exchange 連線無法使用</p>
<p>請確認 Exchange 連線可用</p></td>
</tr>
<tr class="odd">
<td><p>20005</p></td>
<td><p>資訊</p></td>
<td><p>針對 HD 相片存取 Exchange 失敗已復原</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="even">
<td><p>20006</p></td>
<td><p>錯誤</p></td>
<td><p>無法存取 Exchange 以搜尋連絡人</p></td>
<td><p>Exchange 連線無法使用</p>
<p>請確認 Exchange 連線可用</p></td>
</tr>
<tr class="odd">
<td><p>20007</p></td>
<td><p>資訊</p></td>
<td><p>在 Exchange 中搜尋連絡人失敗已復原</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="even">
<td><p>20008</p></td>
<td><p>警告</p></td>
<td><p>嘗試訂閱超過每個應用程式可允許的目前狀態訂閱數</p></td>
<td><p>嘗試訂閱超過每個應用程式可允許的目前狀態訂閱數</p>
<p>檢查用戶端是否有不必要的訂閱</p></td>
</tr>
<tr class="odd">
<td><p>20009</p></td>
<td><p>警告</p></td>
<td><p>嘗試訂閱超過每個批次可允許的目前狀態訂閱數</p></td>
<td><p>嘗試訂閱超過每個批次可允許的目前狀態訂閱數</p>
<p>檢查用戶端是否有不必要的訂閱</p></td>
</tr>
<tr class="even">
<td><p>20010</p></td>
<td><p>錯誤</p></td>
<td><p>無法擷取頻內資料</p></td>
<td><p>無法擷取頻內資料</p>
<p>如果問題持續發生，請連絡產品支援</p></td>
</tr>
<tr class="odd">
<td><p>20011</p></td>
<td><p>錯誤</p></td>
<td><p>無法訂閱目前狀態</p></td>
<td><p>無法訂閱目前狀態</p>
<p>如果問題持續發生，請連絡產品支援</p></td>
</tr>
<tr class="even">
<td><p>20012</p></td>
<td><p>錯誤</p></td>
<td><p>登錄端點失敗</p></td>
<td><p>登錄端點失敗</p>
<p>如果問題持續發生，請連絡產品支援</p></td>
</tr>
<tr class="odd">
<td><p>20013</p></td>
<td><p>錯誤</p></td>
<td><p>IM MCU 無法使用</p></td>
<td><p>IM MCU 無法使用</p>
<p>請查看 IM MCU 是否正在執行</p></td>
</tr>
<tr class="even">
<td><p>20014</p></td>
<td><p>資訊</p></td>
<td><p>連線至 IM MCU 失敗已復原</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="odd">
<td><p>20015</p></td>
<td><p>錯誤</p></td>
<td><p>AV MCU 無法使用</p></td>
<td><p>AV MCU 無法使用</p>
<p>請查看 AV MCU 是否正在執行</p></td>
</tr>
<tr class="even">
<td><p>20016</p></td>
<td><p>資訊</p></td>
<td><p>連線至 AV MCU 失敗已復原</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="odd">
<td><p>20017</p></td>
<td><p>錯誤</p></td>
<td><p>AS MCU 無法使用</p></td>
<td><p>AS MCU 無法使用</p>
<p>請查看 AS MCU 是否正在執行</p></td>
</tr>
<tr class="even">
<td><p>20018</p></td>
<td><p>資訊</p></td>
<td><p>連線至 AS MCU 失敗已復原</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="odd">
<td><p>20019</p></td>
<td><p>錯誤</p></td>
<td><p>資料 MCU 無法使用</p></td>
<td><p>資料 MCU 無法使用</p>
<p>請查看資料 MCU 是否正在執行</p></td>
</tr>
<tr class="even">
<td><p>20020</p></td>
<td><p>資訊</p></td>
<td><p>連線至資料 MCU 失敗已復原</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="odd">
<td><p>20021</p></td>
<td><p>錯誤</p></td>
<td><p>無法加入 IM MCU</p></td>
<td><p>無法加入 IM MCU</p>
<p>請查看 IM MCU 是否正在執行</p></td>
</tr>
<tr class="even">
<td><p>20022</p></td>
<td><p>錯誤</p></td>
<td><p>無法加入 AV MCU</p></td>
<td><p>無法加入 AV MCU</p>
<p>請查看 AV MCU 是否正在執行</p></td>
</tr>
<tr class="odd">
<td><p>20023</p></td>
<td><p>錯誤</p></td>
<td><p>無法加入 AS MCU</p></td>
<td><p>無法加入 AS MCU</p>
<p>請查看 AS MCU 是否正在執行</p></td>
</tr>
<tr class="even">
<td><p>20024</p></td>
<td><p>錯誤</p></td>
<td><p>無法加入資料 MCU</p></td>
<td><p>無法加入資料 MCU</p>
<p>請查看資料 MCU 是否正在執行</p></td>
</tr>
<tr class="odd">
<td><p>20025</p></td>
<td><p>錯誤</p></td>
<td><p>無法針對相片存取 Active Directory</p></td>
<td><p>Active Directory 連線無法使用</p>
<p>請確認 Active Directory 連線可用</p></td>
</tr>
<tr class="even">
<td><p>20026</p></td>
<td><p>資訊</p></td>
<td><p>針對相片存取 Active Directory 失敗已復原</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="odd">
<td><p>20027</p></td>
<td><p>警告</p></td>
<td><p>無法還原序列化</p></td>
<td><p>無法還原序列化</p>
<p>如果問題持續發生，請連絡產品支援</p></td>
</tr>
</tbody>
</table>

