---
title: 行動效能計數器
TOCTitle: 行動效能計數器
ms:assetid: d18ed85a-673d-4695-aa3f-ac83a38ab90a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690046(v=OCS.15)
ms:contentKeyID: 49292393
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 行動效能計數器

 

_**上次修改主題的時間：** 2015-03-09_

下表列出您可以用來監控執行整合通訊 Web API (UCWA) 和 Lync Server 2013 Mcx Mobility Service 的伺服器其效能計數器的名稱和描述。

UCWA 表中的計數器類別名稱為 \[LS:WEB – UCWA\]。

Mcx Mobility Service 表中的計數器類別名稱為 \[LS:WEB - Mobile Communication Service\]。

## UCWA 效能計數器


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>計數器</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Active Application Count</p></td>
<td><p>目前的應用程式數目</p></td>
</tr>
<tr class="even">
<td><p>Active Application Sharing Modality Count</p></td>
<td><p>目前的應用程式共用形式數目</p></td>
</tr>
<tr class="odd">
<td><p>Active Audio Modality Count</p></td>
<td><p>目前的音訊形式數目</p></td>
</tr>
<tr class="even">
<td><p>Active Data Collaboration Modality Count</p></td>
<td><p>目前的資料共同作業形式數目</p></td>
</tr>
<tr class="odd">
<td><p>Active Directory Photo Get Latency (ms)</p></td>
<td><p>此計數器顯示從 Active Directory 擷取相片的平均時間 (毫秒)</p></td>
</tr>
<tr class="even">
<td><p>Active Messaging Modality Count</p></td>
<td><p>目前的通訊形式數目</p></td>
</tr>
<tr class="odd">
<td><p>Active Panoramic Video Modality Count</p></td>
<td><p>目前的全景視訊形式數目</p></td>
</tr>
<tr class="even">
<td><p>Active Pending Get Count</p></td>
<td><p>目前使用中的擱置取得數目；長期保留的伺服器連線</p></td>
</tr>
<tr class="odd">
<td><p>Active Session Count</p></td>
<td><p>目前在每一個應用程式或全部的 UCWA 中已註冊的端點數目</p></td>
</tr>
<tr class="even">
<td><p>Active User Instance Count</p></td>
<td><p>目前的使用者執行個體數目</p></td>
</tr>
<tr class="odd">
<td><p>Active User Instances without Application</p></td>
<td><p>目前無應用程式的使用者執行個體數目</p></td>
</tr>
<tr class="even">
<td><p>Active Video Modality Count</p></td>
<td><p>目前的視訊形式數目</p></td>
</tr>
<tr class="odd">
<td><p>Application Creation Requests Received/Second</p></td>
<td><p>每秒已接收應用程式建立要求的速率</p></td>
</tr>
<tr class="even">
<td><p>AS MCU Join Failures</p></td>
<td><p>AS MCU 加入失敗數目</p></td>
</tr>
<tr class="odd">
<td><p>AV MCU Join Failures</p></td>
<td><p>AV MCU 加入失敗數目</p></td>
</tr>
<tr class="even">
<td><p>Average Application Startup Time (ms)</p></td>
<td><p>應用程式平均啟動時間 (毫秒)</p></td>
</tr>
<tr class="odd">
<td><p>Average Lifetime for Session (ms)</p></td>
<td><p>工作階段的平均存留期 (毫秒)</p></td>
</tr>
<tr class="even">
<td><p>Data MCU Join Failures</p></td>
<td><p>Data MCU 加入失敗數目</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Contact Search Latency (ms)秒)</p></td>
<td><p>此計數器會顯示在 Exchange 中搜尋聯絡人的平均時間 (毫秒)</p></td>
</tr>
<tr class="even">
<td><p>Exchange HD Photo Get Latency (ms)</p></td>
<td><p>此計數器會顯示從 Exchange 擷取相片的平均時間 (毫秒)</p></td>
</tr>
<tr class="odd">
<td><p>HTTP 4xx Responses/Second</p></td>
<td><p>每秒使用 HTTP 4xx 代碼回應的速率</p></td>
</tr>
<tr class="even">
<td><p>HTTP 5xx Responses/Second</p></td>
<td><p>每秒使用 HTTP 5xx 代碼回應的速率</p></td>
</tr>
<tr class="odd">
<td><p>IM MCU Join Failures</p></td>
<td><p>IM MCU 加入失敗數目</p></td>
</tr>
<tr class="even">
<td><p>Number of Active Directory Photo Get Failures</p></td>
<td><p>從 Active Directory 擷取相片的失敗總數</p></td>
</tr>
<tr class="odd">
<td><p>Number of Contact Search failures</p></td>
<td><p>在 Exchange 中搜尋聯絡人的失敗總數</p></td>
</tr>
<tr class="even">
<td><p>Number of Deserialization Failures</p></td>
<td><p>還原序列化失敗總數</p></td>
</tr>
<tr class="odd">
<td><p>Number of HD Photo Get Failures</p></td>
<td><p>從 Exchange 擷取 HD 相片的失敗總數</p></td>
</tr>
<tr class="even">
<td><p>Over The Maximum Subscriptions Per Application</p></td>
<td><p>每個應用程式所允許的訂閱要求數目上限</p></td>
</tr>
<tr class="odd">
<td><p>Over The Maximum Subscriptions Per Batch</p></td>
<td><p>每一批次所允許的訂閱要求數目上限</p></td>
</tr>
<tr class="even">
<td><p>Presence Subscription Failures</p></td>
<td><p>訂閱目前狀態的失敗數目</p></td>
</tr>
<tr class="odd">
<td><p>Registering Endpoint Failures</p></td>
<td><p>註冊端點的失敗數目</p></td>
</tr>
<tr class="even">
<td><p>Requests Received/Second</p></td>
<td><p>每秒接收要求的速率。</p></td>
</tr>
<tr class="odd">
<td><p>Requests Succeeded/Second</p></td>
<td><p>每秒要求成功的速率 (HTTP 2xx/3xx 回應代碼)</p></td>
</tr>
<tr class="even">
<td><p>Succeeded Create Application Requests/Second</p></td>
<td><p>每秒應用程式建立要求成功的速率</p></td>
</tr>
<tr class="odd">
<td><p>Timed Out Pending Get Count</p></td>
<td><p>逾時的擱置取得數目</p></td>
</tr>
<tr class="even">
<td><p>Total Application Creation Requests Received</p></td>
<td><p>自服務啟動後已接收的應用程式建立要求總數</p></td>
</tr>
<tr class="odd">
<td><p>Total HTTP 4xx Responses</p></td>
<td><p>HTTP 4xx 回應總數responses</p></td>
</tr>
<tr class="even">
<td><p>Total HTTP 5xx Responses</p></td>
<td><p>HTTP 5xx 回應總數</p></td>
</tr>
<tr class="odd">
<td><p>Total Requests Received on the Command Channel</p></td>
<td><p>命令通道上接收的要求總數</p></td>
</tr>
<tr class="even">
<td><p>Total Requests Succeeded</p></td>
<td><p>已成功之要求的總數</p></td>
</tr>
<tr class="odd">
<td><p>Total Sessions Initiated</p></td>
<td><p>自服務啟動後已起始的工作階段總數</p></td>
</tr>
<tr class="even">
<td><p>Total Sessions Terminated Because of Idle Timeout</p></td>
<td><p>由於使用者閒置逾時而終止的工作階段總數</p></td>
</tr>
<tr class="odd">
<td><p>Total Throttled Applications</p></td>
<td><p>調整流速之應用程式的數目</p></td>
</tr>
</tbody>
</table>


### Mcx Mobility Service 的效能計數器

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>計數器</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Average Lifetime for a Session in Milliseconds</p></td>
<td><p>工作階段的平均存留期 (毫秒)</p></td>
</tr>
<tr class="even">
<td><p>Current Push Notification Subscriptions</p></td>
<td><p>目前的推播通知訂閱數目。此數目搭配 Currently Active Session Count 可表示 Windows Mobile 或 iPhone 裝置已註冊之目前使用中的工作階段子集。</p></td>
</tr>
<tr class="odd">
<td><p>Currently Active Network Timeout Poll Count</p></td>
<td><p>已逾時的網路輪詢數目</p></td>
</tr>
<tr class="even">
<td><p>Currently Active Poll Count</p></td>
<td><p>目前作用中的輪詢數目 (長期保留的伺服器連線)</p></td>
</tr>
<tr class="odd">
<td><p>Currently Active Session Count</p></td>
<td><p>目前在 Mobility Service 中註冊的端點數目</p></td>
</tr>
<tr class="even">
<td><p>Currently Active Session Count with Active Presence Subscriptions</p></td>
<td><p>目前使用中的工作階段數目及作用中的目前狀態訂閱數目</p></td>
</tr>
<tr class="odd">
<td><p>Push Notification Requests Failed/Second</p></td>
<td><p>每秒失敗的推入通知速率</p></td>
</tr>
<tr class="even">
<td><p>Push Notification Requests Succeeded/Second</p></td>
<td><p>每秒成功的推入通知速率</p></td>
</tr>
<tr class="odd">
<td><p>Push Notification Requests Throttled/Second</p></td>
<td><p>每秒調整流速的推入通知速率</p></td>
</tr>
<tr class="even">
<td><p>Push Notification Requests/Second</p></td>
<td><p>每秒傳送推入通知的速率</p></td>
</tr>
<tr class="odd">
<td><p>Requests Failed/Second</p></td>
<td><p>每秒失敗的要求速率</p></td>
</tr>
<tr class="even">
<td><p>Requests Received/Second</p></td>
<td><p>每秒接收要求的速率</p></td>
</tr>
<tr class="odd">
<td><p>Requests Rejected/Second</p></td>
<td><p>每秒拒絕要求的速率。</p></td>
</tr>
<tr class="even">
<td><p>Requests Succeeded/Second</p></td>
<td><p>每秒成功的要求速率</p></td>
</tr>
<tr class="odd">
<td><p>Succeeded Initiate Session Requests/Second</p></td>
<td><p>每秒成功的取得位置要求速率。起始工作階段的要求會使用大量的伺服器 CPU。支援的最大使用量負載為 12/秒。是否能夠維持取決於伺服器上的其他負載。起始工作階段通常表示有很長一段時間登出的使用者重新登入。</p></td>
</tr>
<tr class="even">
<td><p>Total Declined Inbound Voice Calls</p></td>
<td><p>拒絕的撥入語音通話總數</p></td>
</tr>
<tr class="odd">
<td><p>Total Failed Inbound Voice Calls</p></td>
<td><p>失敗的撥入語音通話總數</p></td>
</tr>
<tr class="even">
<td><p>Total Failed Outbound Voice Calls</p></td>
<td><p>失敗的撥出語音通話總數</p></td>
</tr>
<tr class="odd">
<td><p>Total number of sessions terminated by user</p></td>
<td><p>使用者終止的工作階段總數</p></td>
</tr>
<tr class="even">
<td><p>Total Push Notification Requests</p></td>
<td><p>推入通知要求總數</p></td>
</tr>
<tr class="odd">
<td><p>Total Push Notification Requests Failed</p></td>
<td><p>失敗的推入通知要求總數</p></td>
</tr>
<tr class="even">
<td><p>Total Push Notification Requests Succeeded</p></td>
<td><p>成功的推入通知要求總數</p></td>
</tr>
<tr class="odd">
<td><p>Total Push Notification Requests Throttled</p></td>
<td><p>調整流速的推入通知要求總數</p></td>
</tr>
<tr class="even">
<td><p>Total Requests Failed</p></td>
<td><p>失敗的要求總數</p></td>
</tr>
<tr class="odd">
<td><p>Total Requests received on the Command Channel</p></td>
<td><p>命令通道上已接收的要求總數</p></td>
</tr>
<tr class="even">
<td><p>Total Requests Rejected</p></td>
<td><p>拒絕的要求總數</p></td>
</tr>
<tr class="odd">
<td><p>Total Requests Succeeded</p></td>
<td><p>對 Mobility Service 的要求之成功總數</p></td>
</tr>
<tr class="even">
<td><p>Total Session Initiated Count</p></td>
<td><p>啟動 Mobility Service 後已起始的工作階段總數</p></td>
</tr>
<tr class="odd">
<td><p>Total Sessions Terminated Because of User Idle Timeout</p></td>
<td><p>由於使用者閒置逾時而終止的工作階段總數</p></td>
</tr>
<tr class="even">
<td><p>Total Successful Inbound Voice Calls</p></td>
<td><p>撥入語音通話的成功總數</p></td>
</tr>
<tr class="odd">
<td><p>Total Successful Outbound Voice Calls</p></td>
<td><p>撥出語音通話的成功總數</p></td>
</tr>
</tbody>
</table>

