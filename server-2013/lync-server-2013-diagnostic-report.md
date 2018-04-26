---
title: Lync Server 2013：診斷報告
TOCTitle: 診斷報告
ms:assetid: b389dbd9-f2e8-4184-93d0-2e504796ac16
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg615445(v=OCS.15)
ms:contentKeyID: 49292054
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的診斷報告

 

_**上次修改主題的時間：** 2015-03-09_

診斷報告提供失敗工作階段的診斷與疑難排解資訊。此資訊包含工作階段失敗時，所報告的診斷識別碼與診斷標頭。診斷識別碼是可附加至 SIP 訊息的唯一識別碼 (採用 ms-diagnostics 標頭的格式)，而診斷標頭則提供診斷識別碼的隨附說明。報告可能也會包含所報告元件已知的寶貴疑難排解詳細資料。例如：

  - 產生失敗的 PSTN 閘道提供的原因碼。PSTN 網路上的撥出電話無法作用時，系統會自動產生 ISDN User Part (ISUP) 原因碼。 例如，PSTN 閘道可能傳送原因碼 34，代表沒有可用的電路或通訊管道可以完成通話。

  - 連線失敗的對等 FQDN、連接埠與 Winsock 錯誤。

  - 針對 DNS 解析失敗而查詢的名稱。當用戶端連絡名稱伺服器並要求對應到指定裝置名稱的 IP 位址時，就會發生 DNS 解析。

## 存取診斷報告

可按一下 [Lync Server 2013 中的對等工作階段詳細資料報告](lync-server-2013-peer-to-peer-session-detail-report.md)或 \[會議詳細資料報告\] 上的 \[診斷報告 (詳細資料)\] 計量來存取診斷報告。

## 篩選器

無。診斷報告無法篩選。

## 計量

下表列出診斷報告針對每個工作階段所提供的資訊。

### 診斷報告計量

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
<td><p><strong>報告時間</strong></p></td>
<td><p>否</p></td>
<td><p>報告的記錄日期與時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>回應碼</strong></p></td>
<td><p>否</p></td>
<td><p>工作階段失敗時所傳送的 SIP 回應碼。</p></td>
</tr>
<tr class="odd">
<td><p><strong>要求類型</strong></p></td>
<td><p>否</p></td>
<td><p>失敗的 SIP 要求類型。例如 INVITE、BYE 或 SERVICE。</p></td>
</tr>
<tr class="even">
<td><p><strong>來源</strong></p></td>
<td><p>否</p></td>
<td><p>錯誤的來源</p></td>
</tr>
<tr class="odd">
<td><p><strong>來源使用者 URI</strong></p></td>
<td><p>否</p></td>
<td><p>啟動工作階段之使用者的 SIP 位址。</p></td>
</tr>
<tr class="even">
<td><p><strong>來源使用者代理程式</strong></p></td>
<td><p>否</p></td>
<td><p>啟動工作階段之使用者端點所用的軟體。</p></td>
</tr>
<tr class="odd">
<td><p><strong>診斷識別碼</strong></p></td>
<td><p>否</p></td>
<td><p>附加在 SIP 訊息中的唯一識別碼 (採用 ms-diagnostics 標頭的格式)，常可以在疑難排解錯誤時提供實用的資訊。</p></td>
</tr>
<tr class="even">
<td><p><strong>內容類型</strong></p></td>
<td><p>否</p></td>
<td><p>失敗的媒體內容類型。常見的內容類型是 Application/sdp。工作階段描述通訊協定 (SDP) 是標準的網際網路通訊協定，會用於工作階段宣告、工作階段邀請，以及其他形式之多媒體工作階段邀請。</p></td>
</tr>
<tr class="odd">
<td><p><strong>應用程式</strong></p></td>
<td><p>否</p></td>
<td><p>發生錯誤的應用程式。</p></td>
</tr>
<tr class="even">
<td><p><strong>目標使用者 URI</strong></p></td>
<td><p>否</p></td>
<td><p>獲邀加入工作階段之使用者的 SIP 位址。</p></td>
</tr>
<tr class="odd">
<td><p>會議加入時間 (毫秒)</p></td>
<td><p>否</p></td>
<td><p>使用者加入會議所花的時間 (毫秒)。</p></td>
</tr>
<tr class="even">
<td><p><strong>診斷標題</strong></p></td>
<td><p>否</p></td>
<td><p>診斷識別碼的描述。</p></td>
</tr>
</tbody>
</table>


診斷錯誤清單可在 [Ms-Diagnostics 標頭頁面](http://msdn.microsoft.com/en-us/library/gg132446\(v=office.12\).aspx) (英文) 找到。

