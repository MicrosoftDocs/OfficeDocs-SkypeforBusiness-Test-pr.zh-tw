---
title: Lync Server 2013 IPv6 的技術需求
TOCTitle: IPv6 的技術需求
ms:assetid: caff0123-ce41-4a62-87a0-00b1d118b72b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205278(v=OCS.15)
ms:contentKeyID: 49292312
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中 IPv6 的技術需求

 

_**上次修改主題的時間：** 2012-10-30_

如果您打算針對 IPv6 設定 Lync Server 2013，請注意下列需求：

  - 若要在 Lync Server 使用 IPv6 位址，您需要針對必須被探索到並解析成 IPv6 位址的記錄，建立網域名稱系統 (DNS) 記錄。IPv6 DNS 使用主機 AAAA (四個 A) 記錄。如果您的部署中同時使用 IPv4 和 IPv6，最好同時設定及維護 IPv4 的主機 A 記錄和 IPv6 的主機 AAAA 記錄。即使您完全將部署轉換成 IPv6，您可能仍需要有 IPv4 DNS 主機記錄以供仍在使用 IPv4 的外部使用者使用。
    
    在開始使用 IPv6 前，您可以先部署 IPv6 DNS 主機記錄。用戶端或伺服器如果不使用 IPv6，便不會參考該記錄。過渡性技術會根據過渡性技術的組態與原則，決定要使用哪筆記錄。

  - 每個 IPv6 位址都有範圍。有三個範圍可以用於 IPv6 定址：IPv6 全域位址 (類似公用 IPv4 位址)、IPv6 唯一本機位址 (類似私人 IPv4 位址範圍)，以及 IPv6 連結本機位址 (類似 Windows Server 中 IPv4 的自動私人 IP 位址)。集區內的所有伺服器都應該具有相同範圍的 IPv6 位址。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>IPv6 是個複雜的主題，需要與您的網路團隊及網際網路提供者一起小心規劃，以確保您在 Windows Server 層級和 Lync Server 2013 層級指派的位址將會如預期般運作。如需 IPv6 定址和規劃的其他資源，請參閱本主題結尾的連結。</td>
</tr>
</tbody>
</table>


## 請參閱

#### 其他資源

[IP 版本 6 定址結構](http://tools.ietf.org/html/rfc4291)  
[IPv6 全域單點傳播位址格式](http://tools.ietf.org/html/rfc3587)  
[唯一本機 IPv6 單一位址](http://tools.ietf.org/html/rfc4193)

