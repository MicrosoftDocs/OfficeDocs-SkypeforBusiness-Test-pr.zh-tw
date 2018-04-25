---
title: IP 電話的拓撲
TOCTitle: IP 電話的拓撲
ms:assetid: 26ebffcf-43ff-4e70-847d-0fbc90e94e57
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425740(v=OCS.15)
ms:contentKeyID: 49290385
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# IP 電話的拓撲

 

_**上次修改主題的時間：** 2012-06-21_

本節提供連線程序的概觀，並會說明 IP 電話連線至內部與外部網路的差異。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lync Server 可支援下列 IP 電話：Aastra 6721ip 公用區電話、Aastra 6725ip 電話機、HP 4110 IP 電話 (公用區電話)、HP 4120 IP 電話 (電話機)、Polycom CX600 IP 電話機、Polycom CX700 IP 電話機、Polycom CX500 IP 公用區電話以及 Polycom CX3000 IP 會議電話。這些電話中，除了 Polycom CX700 之外，所有電話皆可執行 Lync Phone Edition。</td>
</tr>
</tbody>
</table>


下圖說明公司環境中與裝置連線功能相關的所有元件。

**內部拓撲**

![網路內部裝置](images/Gg425740.3d88893e-df57-46e3-855a-a1d24589030a(OCS.15).jpg "網路內部裝置")

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>上圖所呈現的是邏輯性代表，而不是實際的概觀。例如，Active Directory 網域服務 (AD DS) 很少會與任何 Lync Server 元件位於相同的機器上。使用者存放區只能位於後端伺服器或是封存與監控伺服器之上。Lync Server 管理命令介面、Web 伺服器和升級服務都是前端伺服器角色的一部分。</td>
</tr>
</tbody>
</table>


下圖說明當裝置位於公司網路外時相關的元件概觀。

**外部拓撲**

![網路外部裝置](images/Gg425740.8ce6bb8e-b89c-4c4e-ac6d-41ac6c68f6f3(OCS.15).jpg "網路外部裝置")

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>裝置更新 Web 服務會提供一個外部與內部網站，但此處僅顯示外部網站。<br />
當啟用外部存取時，組織的登錄器位置與裝置更新 Web 服務的 URL 都必須發佈至 DNS。此外，您必須部署並正確設定 Edge Server，以讓裝置和公司環境之間的外部通訊可順利進行。上圖省略了這個部分，因為 Edge 部署並不是專用於裝置連線此部分。</td>
</tr>
</tbody>
</table>

