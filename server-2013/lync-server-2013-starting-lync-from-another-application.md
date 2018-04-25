---
title: 從其他應用程式啟動 Lync
TOCTitle: 從其他應用程式啟動 Lync
ms:assetid: 573b30b1-6590-4b24-8e96-a41be57cb0ef
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398376(v=OCS.15)
ms:contentKeyID: 52056111
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 從其他應用程式啟動 Lync

 

_**上次修改主題的時間：** 2015-03-09_

您可以使用命令列參數，快速啟動 Lync 2013。例如，當使用者按一下另一個應用程式中的電話號碼，該應用程式便會啟動 Lync 2013 執行個體並開始撥出該號碼。

Lync 2013 還能辨識分號分隔的連絡人名稱清單以便進行多方會議。

如果 Lync 2013 設為啟動時自動登入，則使用命令列參數啟用 Lync 2013 會開啟 Lync 主視窗。如果 Lync 並未設為啟動時自動登入，會開啟登入視窗。

下表顯示可用的參數。

### Lync 2013 命令列參數

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>延伸</th>
<th>資料格式</th>
<th>動作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>tel:</p></td>
<td><p>tel URI</p></td>
<td><p>開啟音訊通話的「交談」視窗，但不會撥打指定號碼。</p></td>
</tr>
<tr class="even">
<td><p>callto:</p></td>
<td><p>tel:、sip: 或可輸入的 tel URI</p></td>
<td><p>開啟音訊通話的「交談」視窗，但不會撥打指定號碼。</p></td>
</tr>
<tr class="odd">
<td><p>sip:</p></td>
<td><p>SIP URI</p></td>
<td><p>會開啟「交談」視窗，並在參與者清單中列出指定的 SIP 統一資源識別元 (URI)。</p></td>
</tr>
<tr class="even">
<td><p>Sips:</p></td>
<td><p>SIP URI</p></td>
<td><p>如果 Lync 2013 設為使用傳輸層安全性 (TLS) 通訊協定，則其功能將等同於 sip:。如果並未使用 TLS 功能，會顯示一個對話方塊，告知使用者需要啟用較高層級的安全性。</p></td>
</tr>
<tr class="odd">
<td><p>conf:</p></td>
<td><p>要加入的會議 SIP URI</p></td>
<td><p>如果 URI 為自行作用參數，會啟動焦點並帶出僅限會議名冊的檢視。否則，會帶出會議名冊檢視，但不會傳送 INVITE。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p>im:</p></td>
<td><p>SIP URI</p></td>
<td><p>顯示內含 SIP URI 的僅限立即訊息 (IM)「交談」視窗。接受在角括號 (&lt;&gt;) 裡面不使用任何分隔符號指定多個 SIP URI。</p>
<pre><code>im:&lt;sip:user1@host&gt;&lt;sip:user2@host&gt;</code></pre></td>
</tr>
</tbody>
</table>


下表提供上述命令列參數範例。

### 命令列參數範例

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>執行個體</th>
<th>結果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Tel:+14255550101</p></td>
<td><p>會開啟內含 +14255550101 的僅限電話檢視。</p></td>
</tr>
<tr class="even">
<td><p>Callto:tel:+ 14255550101</p></td>
<td><p>會開啟內含 +14255550101 的僅限電話檢視。</p></td>
</tr>
<tr class="odd">
<td><p>Callto:sip:kazuto@litwareinc.com</p></td>
<td><p>會開啟內含 kazuto@litwareinc.com 的僅限電話檢視。</p></td>
</tr>
<tr class="even">
<td><p>sip:kazuto@litwareinc.com</p></td>
<td><p>會開啟內含 kazuto@litwareinc.com 的交談視窗。</p></td>
</tr>
<tr class="odd">
<td><p>conf:sip:https://meet.contoso.com/kazuto/7322994</p></td>
<td><p>會開啟交談視窗並顯示會議音訊加入選項。</p></td>
</tr>
</tbody>
</table>

