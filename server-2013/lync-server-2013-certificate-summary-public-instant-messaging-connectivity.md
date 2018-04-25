---
title: 憑證摘要 - Public Instant Messaging 連線
TOCTitle: 憑證摘要 - Public Instant Messaging 連線
ms:assetid: 2b3687ee-50c2-4c1c-880e-8dcf8bd4f309
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ618370(v=OCS.15)
ms:contentKeyID: 49290411
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 憑證摘要 - Public Instant Messaging 連線

 

_**上次修改主題的時間：** 2015-03-09_

若要設定公用立即訊息連線的憑證，您應先知道除了 America Online (AOL) 需要專屬憑證設定之外，與其他 SIP 同盟類型，甚至與標準 Edge Server 憑證均無不同。America Online 不但需要一般伺服器增強金鑰使用方法 (EKU)，還需要憑證也包含用戶端 EKU (若為 Edge 集區時，則為多個憑證)。用戶端 EKU 是憑證的附加部分，並且是指派給 Edge Server 之外部公用憑證的一部分。

## 憑證摘要 - 公用立即訊息連線


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
<td><p>若要部署與 AOL 的公用 IM 連線，憑證必須來自公用 CA，且必須具有伺服器 EKU 和用戶端 EKU。憑證會指派給下列項目的外部 Edge Server 介面：</p>
<ul>
<li><p>Access Edge Service</p></li>
<li><p>Web Conferencing Edge Service</p></li>
<li><p>A/V Edge 服務</p></li>
</ul>
<p>請注意，系統會根據您在拓撲產生器中的定義，將 SAN 自動新增至憑證。您可以視需要為其他 SIP 網域新增 SAN 項目，或新增其他必須支援的項目。SAN 中的主體名稱會複寫，且必須存在才能正常運作。</p></td>
</tr>
</tbody>
</table>


## 請參閱

#### 概念

[Lync Server 2013 中的外部使用者存取案例](lync-server-2013-scenarios-for-external-user-access.md)

