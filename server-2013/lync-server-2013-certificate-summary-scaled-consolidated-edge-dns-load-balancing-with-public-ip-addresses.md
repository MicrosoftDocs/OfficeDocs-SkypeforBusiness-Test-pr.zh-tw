﻿---
title: Lync Server 2013：憑證摘要 - 調整式合併 Edge (利用公用 IP 位址進行 DNS 負載平衡)
TOCTitle: 憑證摘要 - 調整式合併 Edge (利用公用 IP 位址進行 DNS 負載平衡)
ms:assetid: e87ac448-ee8f-477a-9f33-ce066c1bf093
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205399(v=OCS.15)
ms:contentKeyID: 49292668
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的憑證摘要 - 調整式合併 Edge (利用公用 IP 位址進行 DNS 負載平衡)

 

_**上次修改主題的時間：** 2015-03-09_

Microsoft Lync Server 2013 使用憑證來手動驗證其他伺服器，並加密伺服器到伺服器與伺服器到用戶端的資料。憑證必須有與伺服器建立關聯之網域名稱系統 (DNS) 記錄的名稱比對，以及憑證上的主體名稱 (SN) 與主體別名 (SAN)。為了成功對應伺服器、DNS 記錄與憑證項目，您必須在登錄於 DNS 時小心規劃所需的伺服器完整網域名稱，以及憑證上 SN 與 SAN 項目。

公用憑證授權單位 (CA) 會要求指派到 Edge Server 外部介面的憑證。下文列出已針對 整合通訊 目的成功供應憑證的公用 CA： <http://support.microsoft.com/kb/929395> 要求憑證時，您可使用 Lync Server 部署精靈產生的憑證要求，或是手動或依公用 CA 提供之程序建立要求。指派憑證時，憑證會指派到 Access Edge Service 介面、 Web Conferencing Edge Service 介面，以及音訊/視訊驗證服務。音訊/視訊驗證服務不應與 A/V Edge 服務 混淆，後者不使用憑證加密音訊與視訊串流。內部 Edge Server 介面可使用內部 (到貴公司) CA 的憑證，或是公用 CA 的憑證。內部介面憑證只使用 SN，不需要或使用 SAN 項目。

> [!NOTE]  
> 下表顯示主體替代名稱清單中的第二個 SIP (sip.fabrikam.com) 項目供您參考。您必須為組織中的每個 SIP 網域新增憑證主體替代名稱清單所列的對應 FQDN。



## 使用 DNS 負載平衡與公用 IP 位址的調整式合併 Edge


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
<td><p>調整式合併 Edge (外部 Edge)</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>webcon.contoso.com</p>
<p>sip.contoso.com</p>
<p>sip.fabrikam.com</p></td>
<td><p>若要部署與 AOL 的公用 IM 連線，憑證必須由公用 CA 發出，且必須要有伺服器 EKU 與用戶端 EKU。另外，若使用調整式 Edge Server，憑證私密金鑰必須要能匯出，且憑證與私密金鑰必須複製到每個 Edge Server。指派憑證到外部 Edge 介面的目的如下：</p>
<ul>
<li><p>Access Edge</p></li>
<li><p>Conferencing Edge</p></li>
<li><p>A/V Edge</p></li>
</ul>
<p>請注意，SAN 會自動根據您在拓撲產生器所下的定義新增到憑證。您可視需要為其他必須支援的 SIP 網域及其他項目新增 SAN 項目。主體名稱會複寫到 SAN 中，必須要出現才會正確運作。</p></td>
</tr>
<tr class="even">
<td><p>調整式合併 Edge (內部 Edge)</p></td>
<td><p>lsedge.contoso.net</p></td>
<td><p>不需要 SAN</p></td>
<td><p>憑證可用公用或私人 CA 發出，且必須包含伺服器 EKU。憑證會指派到內部 Edge 介面。</p></td>
</tr>
</tbody>
</table>


## 憑證摘要：Public Instant Messaging Connectivity


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
<td><p>外部/Access Edge</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>sip.contoso.com</p>
<p>webcon.contoso.com</p>
<p>sip.fabrikam.com</p></td>
<td><p>若要部署與 AOL 的公用 IM 連線，憑證必須由公用 CA 發出，且必須要有伺服器 EKU 與用戶端 EKU。指派憑證到外部 Edge 介面的目的如下：</p>
<ul>
<li><p>Access Edge</p></li>
<li><p>Conferencing Edge</p></li>
<li><p>A/V Edge</p></li>
</ul>
<p>請注意，SAN 會自動根據您在拓撲產生器所下的定義新增到憑證。您可視需要為其他必須支援的 SIP 網域及其他項目新增 SAN 項目。主體名稱會複寫到 SAN 中，必須要出現才會正確運作。</p></td>
</tr>
</tbody>
</table>


## 可延伸訊息與目前狀態通訊協定的憑證摘要


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
<td><p>指派到 Edge Server 的 Access Edge Service 或 Edge 集區</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>webcon.contoso.com</p>
<p>sip.contoso.com</p>
<p>sip.fabrikam.com</p>
<p>xmpp.contoso.com</p>
<p><strong>*.contoso.com</strong></p></td>
<td><p>頭三個 SAN 項目是完整 Edge Server 的一般 SAN 項目。contoso.com 是同盟與 XMPP 夥伴在根網域層級要求的項目。此項目允許所有尾碼為 *.contoso.com 的網域執行XMPP。</p></td>
</tr>
</tbody>
</table>

