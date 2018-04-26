---
title: 憑證摘要 - 可延伸的訊息和顯示狀態通訊協定 (XMPP) 同盟
TOCTitle: 憑證摘要 - 可延伸的訊息和顯示狀態通訊協定 (XMPP) 同盟
ms:assetid: b059a34e-99df-40af-91fe-fe2aa52841f6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ618374(v=OCS.15)
ms:contentKeyID: 49292010
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 憑證摘要 - 可延伸的訊息和顯示狀態通訊協定 (XMPP) 同盟

 

_**上次修改主題的時間：** 2015-03-09_

啟用與建立與可延伸傳訊和顯示狀態通訊協定 (XMPP) 合作夥伴的的憑證要求需要額外記錄您的 XMPP 網域。包含在憑證作為主體替代名稱 (SAN) 的記錄會是可以參與 XMPP 通訊的網域。如果您想要對整個網域啟用 XMPP，則網域可以是根層級網域 (例如，contoso.com)，或如果您想要對使用者子集啟用 XMPP，可以是選取的子網域 (例如，corp.contoso.com、finance.contoso.com)。

## 可延伸傳訊和顯示狀態通訊協定的憑證摘要


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>元件</th>
<th>主體名稱</th>
<th>主體替代名稱 (SAN)/順序</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>指派給 Edge Server 的 Access Edge Service 或 Edge 集區</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>webcon.contoso.com</p>
<p>sip.contoso.com</p>
<p>sip.fabrikam.com</p>
<p>contoso.com</p></td>
<td><p>前三個 SAN 項目是完整 Edge Server 的一般 SAN 項目。contoso.com 是與根網域層級之 XMPP 協力廠商同盟所需的項目。此項目會允許擁有尾碼 contoso.com 之所有網域的 XMPP。</p></td>
</tr>
</tbody>
</table>


## 請參閱

#### 工作

[Lync Server 2013 中的範例 XMPP 設定 – XMPP 與 Google Talk 的同盟](lync-server-2013-example-xmpp-configuration-–-xmpp-federation-with-google-talk.md)  

#### 概念

[在 Lync Server 2013 中規劃 Edge Server 憑證](lync-server-2013-plan-for-edge-server-certificates.md)  

#### 其他資源

[針對 Lync Server 2013 設定 Edge 憑證](lync-server-2013-set-up-edge-certificates.md)  
[Request-CsCertificate](request-cscertificate.md)  
[Set-CsCertificate](set-cscertificate.md)

