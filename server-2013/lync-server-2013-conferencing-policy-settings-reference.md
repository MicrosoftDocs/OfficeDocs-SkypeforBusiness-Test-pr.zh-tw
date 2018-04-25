---
title: Lync Server 2013 中的會議原則設定參考
TOCTitle: Lync Server 2013 中的會議原則設定參考
ms:assetid: ec8125f7-ef78-4a2b-8db0-4dd3cf5a4065
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg429724(v=OCS.15)
ms:contentKeyID: 49292711
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的會議原則設定參考

 

_**上次修改主題的時間：** 2014-04-22_

本主題中的表格列出您可使用 Lync Server 2013 控制台指定的所有會議原則設定。

## 召集人原則設定

下表列出可套用至會議召集人的所有會議原則設定。如需會議原則設定的最新清單，請參閱 [Set-CsClientPolicy](set-csclientpolicy.md) Cmdlet 的說明主題。

### 召集人原則設定

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>設定</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>最大會議大小</p></td>
<td><p>設定會議中所允許的參與者數目上限。</p></td>
</tr>
<tr class="even">
<td><p>允許參與者邀請匿名使用者</p></td>
<td><p>允許會議召集人邀請未經過驗證的使用者與會。</p></td>
</tr>
<tr class="odd">
<td><p>啟用錄製</p></td>
<td><p>允許主持人或出席者錄製會議。</p></td>
</tr>
<tr class="even">
<td><p>允許同盟和匿名參與者錄製</p></td>
<td><p>允許外部或未經過驗證的參與者錄製會議。</p></td>
</tr>
<tr class="odd">
<td><p>啟用 IP 音訊</p></td>
<td><p>允許在會議中使用音訊。</p></td>
</tr>
<tr class="even">
<td><p>啟用 IP 音訊/視訊</p></td>
<td><p>允許在會議中使用音訊和視訊。</p></td>
</tr>
<tr class="odd">
<td><p>啟用 PSTN 電話撥入式會議</p></td>
<td><p>允許使用者從公用交換電話網路 (PSTN) 撥入以參加會議。</p></td>
</tr>
<tr class="even">
<td><p>允許匿名參與者撥出</p></td>
<td><p>允許未經過驗證的使用者使用撥出電話來加入會議。透過撥出電話，會議伺服器會呼叫使用者，這時使用者可以接聽電話以加入會議。</p></td>
</tr>
<tr class="odd">
<td><p>會議允許的最大視訊解析度</p></td>
<td><p>設定視訊會議的最大解析度。有效值為 <strong>[640*480(VGA)]</strong> 和 <strong>[352*288(CIF)]</strong>。</p></td>
</tr>
<tr class="even">
<td><p>啟用資料共同作業</p></td>
<td><p>啟用資料共同作業會議或 Web 會議。</p></td>
</tr>
<tr class="odd">
<td><p>允許同盟和匿名參與者下載內容</p></td>
<td><p>允許外部或未經過驗證的參與者下載會議內容。</p></td>
</tr>
<tr class="even">
<td><p>允許參與者傳輸檔案</p></td>
<td><p>允許會議參與者在會議期間傳輸檔案。</p></td>
</tr>
<tr class="odd">
<td><p>啟用註釋</p></td>
<td><p>允許會議參與者在內容中建立註釋。</p></td>
</tr>
<tr class="even">
<td><p>啟用投票</p></td>
<td><p>允許會議參與者在會議期間舉行投票。</p></td>
</tr>
<tr class="odd">
<td><p>啟用應用程式共用</p></td>
<td><p>允許使用者排程支援應用程式共用的會議。</p></td>
</tr>
<tr class="even">
<td><p>允許參與者取得控制權</p></td>
<td><p>允許參與者取得對其他使用者之共用應用程式的控制權。</p></td>
</tr>
<tr class="odd">
<td><p>允許同盟和匿名參與者取得控制權</p></td>
<td><p>允許外部和匿名參與者取得對其他使用者之共用應用程式的控制權。</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若此設定設為 True，且 <strong>[允許參與者取得控制權]</strong> 設為 False，則會覆寫此設定。</td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 參與者原則設定

下表列出可套用至會議參與者的所有會議原則設定。

### 參與者原則設定

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>設定</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>啟用應用程式共用</p></td>
<td><p>允許使用者排程支援應用程式共用的會議。</p></td>
</tr>
<tr class="even">
<td><p>啟用應用程式和桌面共用</p></td>
<td><p>允許使用者參加支援應用程式共用與桌面共用的會議。在會議中，這個套用到會議召集人的設定值會套用到所有參與的匿名端點。</p></td>
</tr>
<tr class="odd">
<td><p>啟用點對點檔案傳輸</p></td>
<td><p>允許參與者在會議期間執行點對點檔案傳輸。點對點檔案傳輸不會涉及所有會議參與者。</p></td>
</tr>
<tr class="even">
<td><p>啟用點對點錄製</p></td>
<td><p>允許參與者錄製點對點會議工作階段。</p></td>
</tr>
</tbody>
</table>

