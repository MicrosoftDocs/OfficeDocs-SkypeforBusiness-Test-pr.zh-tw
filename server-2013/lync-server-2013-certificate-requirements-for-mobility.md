---
title: Lync Server 2013：行動憑證需求
TOCTitle: 行動憑證需求
ms:assetid: bb0e97af-cf60-4271-a0ab-654429d884ea
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690044(v=OCS.15)
ms:contentKeyID: 49292128
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的行動憑證需求

 

_**上次修改主題的時間：** 2015-03-09_

如果您部署行動功能並支援行動用戶端自動探索，您必須在憑證上包含特定主體替代名稱項目，以支援來自行動用戶端的安全連線。

您必須在下列憑證上包含主體替代名稱項目，以進行自動探索：

  - Director 集區

  - 前端集區

  - 反向 Proxy

本節說明憑證上所需的主體替代名稱項目，以進行自動探索。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用內部憑證授權單位重新發行憑證通常是很簡單的程序，但是將多個主體替代名稱項目新增至反向 Proxy 所使用的公開憑證可能很昂貴。如果您具有許多 SIP 網域，使得新增主體別名很昂貴，您可以設定反向 Proxy 讓初始自動探索服務要求使用 HTTP，而不是使用 HTTPS (預設設定)。如需詳細資訊，請參閱 <a href="lync-server-2013-technical-requirements-for-mobility.md">Lync Server 2013 行動技術需求</a>。</td>
</tr>
</tbody>
</table>


### Director 集區憑證需求

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>說明</th>
<th>主體替代名稱項目</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>內部自動探索服務 URL</p></td>
<td><p>SAN=lyncdiscoverinternal.&lt;SIP 網域&gt;</p></td>
</tr>
<tr class="even">
<td><p>外部自動探索服務 URL</p></td>
<td><p>SAN=lyncdiscover.&lt;SIP 網域&gt;</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>或者，您可以使用 SAN=*.&lt;SIP 網域&gt;</td>
</tr>
</tbody>
</table>


### 前端集區憑證需求

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>說明</th>
<th>主體替代名稱項目</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>內部自動探索服務 URL</p></td>
<td><p>SAN=lyncdiscoverinternal.&lt;SIP 網域&gt;</p></td>
</tr>
<tr class="even">
<td><p>外部自動探索服務 URL</p></td>
<td><p>SAN=lyncdiscover.&lt;SIP 網域&gt;</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>或者，您可以使用 SAN=*.&lt;SIP 網域&gt;</td>
</tr>
</tbody>
</table>


### 反向 Proxy (公用 CA) 憑證需求

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>說明</th>
<th>主體替代名稱項目</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>外部自動探索服務 URL</p></td>
<td><p>SAN=lyncdiscover.&lt;SIP 網域&gt;</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您將此 SAN 指派給反向 Proxy 上的 SSL 接聽程式的憑證。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>反向 Proxy 接聽程式有外部 Web 服務 URL 的主體替代名稱 (例如 SAN=lyncwebextpool01.contoso.com 以及 dirwebexternal.contoso.com - 如果您已部署選用的 Director)。</td>
</tr>
</tbody>
</table>

