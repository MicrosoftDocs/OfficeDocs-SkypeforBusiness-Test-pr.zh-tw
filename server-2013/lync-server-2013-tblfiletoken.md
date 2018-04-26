---
title: Lync Server 2013：tblFileToken
TOCTitle: tblFileToken
ms:assetid: 49e7dd79-1607-443c-818a-88c160e4ed06
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg558646(v=OCS.15)
ms:contentKeyID: 49290824
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 tblFileToken

 

_**上次修改主題的時間：** 2015-03-09_

tblFileToken 包含用於檔案傳輸的臨時權杖。

### 欄

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>欄</th>
<th>類型</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>fileToken</p></td>
<td><p>nvarchar (50)，非 null</p></td>
<td><p>唯一 Token (GUID)。</p></td>
</tr>
<tr class="even">
<td><p>fileTokenUserID</p></td>
<td><p>int，非 null</p></td>
<td><p>傳輸檔案之主體的識別碼。</p></td>
</tr>
<tr class="odd">
<td><p>fileTokenChannelID</p></td>
<td><p>GUID，非 null</p></td>
<td><p>聊天室節點的 GUID。</p></td>
</tr>
<tr class="even">
<td><p>fileTokenExpireDate</p></td>
<td><p>datetime，非 null</p></td>
<td><p>到期時間 (權杖於 30 分鐘後到期，除非已固定 (請參閱此欄中下列說明)。</p></td>
</tr>
<tr class="odd">
<td><p>fileTokenComplianceFileUrl</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>已傳輸檔案的 URL (供 Compliance Service 使用)。</p></td>
</tr>
<tr class="even">
<td><p>fileTokenComplianceThumbnailUrl</p></td>
<td><p>nvarchar(256)</p></td>
<td><p>已傳輸檔案的縮圖 URL (供 Compliance Service 使用)。</p></td>
</tr>
<tr class="odd">
<td><p>fileTokenComplianceTime</p></td>
<td><p>datetime2</p></td>
<td><p>實際檔案傳輸作業的時間戳記 (供 Compliance Service 使用)。</p></td>
</tr>
<tr class="even">
<td><p>fileTokenComplianceIsUpload</p></td>
<td><p>bit</p></td>
<td><p>若上傳則為 True；若下載則為 False (供 Compliance Service 使用)。</p></td>
</tr>
<tr class="odd">
<td><p>fileTokenCompliancePinned</p></td>
<td><p>bit，非 null</p></td>
<td><p>若權杖已固定則為 True，用於將權杖保存在表格中，直到 Compliance Service 有機會從中擷取相關欄位。</p></td>
</tr>
</tbody>
</table>


### 索引鍵

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>欄</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>fileToken</p></td>
<td><p>主索引鍵。</p></td>
</tr>
<tr class="even">
<td><p>fileTokenChannelID</p></td>
<td><p>在 Node.nodeGuid 表格中查閱外部索引鍵。</p></td>
</tr>
</tbody>
</table>

