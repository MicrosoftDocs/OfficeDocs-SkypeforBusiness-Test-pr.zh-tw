---
title: Lync Server 2013：DNS 基礎結構支援
TOCTitle: 網域名稱系統 (DNS) 基礎結構支援
ms:assetid: 37777c16-94ce-436d-b517-bcf53a564513
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425850(v=OCS.15)
ms:contentKeyID: 49290590
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 DNS 基礎結構支援

 

_**上次修改主題的時間：** 2013-03-08_

Lync Server 2013 需要網域名稱系統 (DNS)，並用於下列目的：

  - 探索內部伺服器或集區以進行伺服器對伺服器的通訊。

  - 讓用戶端可探索用於各種 SIP 交易的前端集區或 Standard Edition Server。

  - 將會議的簡單 URL 與裝載這些會議的伺服器產生關聯。

  - 讓外部伺服器與用戶端可連線至 Edge Server 或 HTTP 反向 Proxy 以進行立即訊息 (IM) 或會議。

  - 讓未登入的整合通訊 (UC) 裝置可探索執行裝置更新 Web 服務的前端集區或 Standard Edition Server 以取得更新以及傳送記錄檔。

  - 讓行動用戶端能自動探索 Web 服務資源，而不需使用者手動在裝置設定中輸入 URL。

  - 進行 DNS 負載平衡。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lync Server 2013 不支援國際化網域名稱 (IDN)。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您指定的名稱必須與伺服器上設定的電腦名稱相同。根據預設，電腦如未加入網域，則其電腦名稱屬於簡短名稱，而不是完整網域名稱 (FQDN)。拓撲產生器使用的是 FQDN，而非簡短名稱，因此，若是要將未加入網域的電腦部署為 Edge Server，您必須在其名稱中設定 DNS 尾碼。指派 Lync Server、Edge Server 和集區的 FQDN 時，「僅限使用標準字元」 (包括 A–Z、a–z、0–9 及連字號)。請勿使用 Unicode 字元或底線。外部 DNS 與公用 CA 通常不支援在 FQDN 中使用非標準字元 (也就是 FQDN 必須指派給憑證中 SN 時)。</td>
</tr>
</tbody>
</table>

