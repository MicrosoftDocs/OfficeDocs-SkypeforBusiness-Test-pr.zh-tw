---
title: DNS 摘要 - 可延伸的訊息和顯示狀態通訊協定 (XMPP) 同盟
TOCTitle: DNS 摘要 - 可延伸的訊息和顯示狀態通訊協定 (XMPP) 同盟
ms:assetid: 0f720a2a-8ab5-43cc-882a-ab595ed3cec7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ618368(v=OCS.15)
ms:contentKeyID: 49290104
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# DNS 摘要 - 可延伸的訊息和顯示狀態通訊協定 (XMPP) 同盟

 

_**上次修改主題的時間：** 2015-03-09_

若要為您的部署設定可延伸訊息和目前狀態通訊協定 (XMPP)，請在外部 DNS 伺服器中建立兩個網域名稱系統 (DNS) 記錄，該伺服器會將記錄解析至 Edge Server 或 Edge 集區的 Access Edge Service。

## 可延伸訊息和目前狀態通訊協定的 DNS 摘要


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>位置/類型/連接埠</th>
<th>FQDN</th>
<th>IP 位址/FQDN 主機記錄</th>
<th>對應至/註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>外部 DNS/SRV/5269</p></td>
<td><p>_xmpp-server._tcp.contoso.com</p></td>
<td><p>xmpp.contoso.com</p></td>
<td><p>Access Edge Service 或 Edge 集區上的 XMPP Proxy 外部介面。請針對具有啟用 Lync 之使用者的所有內部 SIP 網域，依需要重複，在該網域中，若要與 XMPP 連絡人聯繫，可以透過全域原則、使用者所在的網站原則，或套用至啟用 Lync 之使用者的使用者原則，來設定外部存取原則。XMPP 同盟協力廠商原則中也必須設定允許的 XMPP 網域。如需詳細資訊，請參閱＜<strong>請參閱</strong>＞中的主題。</p></td>
</tr>
<tr class="even">
<td><p>外部 DNS/A</p></td>
<td><p>xmpp.contoso.com (範例)</p></td>
<td><p>Edge Server 或裝載 XMPP Proxy 的 Edge 集區之 Access Edge Service 的 IP 位址</p></td>
<td><p>指向 Access Edge Service 或裝載 XMPP Proxy 服務的 Edge 集區。一般而言，您建立的 SRV 記錄會指向此主機 (A 或 AAAA) 記錄</p></td>
</tr>
</tbody>
</table>


## 請參閱

#### 工作

[在 Lync Server 2013 中設定 XMPP 同盟](lync-server-2013-setting-up-xmpp-federation.md)  

#### 概念

[針對 Lync Server 2013 判定 DNS 需求](lync-server-2013-determine-dns-requirements.md)

