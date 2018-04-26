---
title: Lync Server 2013：Lync 用戶端軟體支援
TOCTitle: Lync 用戶端軟體支援
ms:assetid: a6851e38-ba9a-4f19-9aa7-d8accf4d62b3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412781(v=OCS.15)
ms:contentKeyID: 49291907
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Lync 用戶端軟體支援

 

_**上次修改主題的時間：** 2015-07-06_

本節摘要說明 Lync 2013 和 Lync 2013 的線上會議增益集的軟體支援。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lync 2013 的線上會議增益集會隨著 Lync 2013 自動安裝，支援在 Outlook 訊息和共同作業用戶端內管理會議。</td>
</tr>
</tbody>
</table>


### Lync 2013 和 Lync 2013 的線上會議增益集的軟體需求

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>系統元件</th>
<th>最低需求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows 作業系統</p></td>
<td><p>Windows 8.1</p>
<p>Windows 8</p>
<p>Windows 7 作業系統</p>
<p>具有最新 Service Pack 的 Windows Server 2008 R2</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Windows Vista 或 Windows XP (任何版本) 都不支援 Lync 2013 與 Lync 2013 的線上會議增益集。</td>
</tr>
</tbody>
</table>

</div></td>
</tr>
<tr class="even">
<td><p>安裝和更新</p></td>
<td><p>系統管理員權限</p></td>
</tr>
<tr class="odd">
<td><p>瀏覽器</p></td>
<td><p>Windows Internet Explorer 10 網際網路瀏覽器</p>
<p>Internet Explorer 9 網際網路瀏覽器</p>
<p>Internet Explorer 8 網際網路瀏覽器</p>
<p>Internet Explorer 7 網際網路瀏覽器</p>
<p>Mozilla Firefox 網頁瀏覽器</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您使用 Lync 搭配 Microsoft Exchange Online，而且您的組織已部署驗證的 HTTP Proxy，那麼需要使用 Internet Explorer 9 或 Internet Explorer 8。</td>
</tr>
</tbody>
</table>

</div></td>
</tr>
<tr class="even">
<td><p>Microsoft Office 整合</p></td>
<td><p>完整的整合功能：</p>
<ul>
<li><p>Outlook 2013 訊息和共同作業用戶端</p></li>
<li><p>Outlook 2010 訊息和共同作業用戶端</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange 整合</p></td>
<td><p>完整的整合功能：</p>
<ul>
<li><p>Microsoft Exchange Server 2013</p></li>
<li><p>Microsoft Exchange Server 2010</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Macintosh 作業系統

Lync 2013 僅適用於 Windows。但是， Lync Server 2013 在執行 Mac OS 10.5.8 或最新 Service Pack 或最新版 (採用 Intel) 作業系統的電腦上支援下列用戶端 (目前不支援 Mac OS 10.9 作業系統)。如需受支援功能的詳細資料，請參閱 [Lync Server 2013 的用戶端比較表](lync-server-2013-desktop-client-comparison-tables.md)。

  - Microsoft Lync for Mac 2011 (請參閱＜Lync for Mac 2011 部署指南＞，網址為： [http://go.microsoft.com/fwlink/?linkid=268786\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=268786%26clcid=0x404))

  - Microsoft Communicator for Mac 2011 (請參閱《Communicator for Mac 2011 部署指南》，網址為： [http://go.microsoft.com/fwlink/?linkid=268787\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=268787%26clcid=0x404))

## Lync Web App 瀏覽器

Lync Web App 支援特定的作業系統和瀏覽器組合。如需詳細資訊，請參閱規劃文件中的＜ [Lync Server 2013 的 Lync Web App 支援平台](lync-server-2013-lync-web-app-supported-platforms.md)＞。

## Microsoft Office 支援能力

如本節所述， Lync Server 2013 用戶端支援各種 Microsoft Office 版本的整合。

  - 在 Outlook 2013 和 Microsoft Outlook 2010 上支援 Lync 2013 整合功能。

  - 在 Microsoft Exchange Server 2013 和 Microsoft Exchange Server 2010 上支援 Lync 2013 整合功能。

  - Office 2013 和 Microsoft Office 2010 支援 Lync 2013 的線上會議增益集。

## 使用強制設定檔

如果使用者計劃要使用 Lync 2013 會議功能，則不應使用 Active Directory 網域服務 強制設定檔來登入 Lync 2013 用戶端。由於強制設定檔是唯讀的使用者設定檔，因此 Lync 2013 會議所需的公開金鑰基礎結構 (PKI) 金鑰無法儲存至設定檔。如需詳細資訊，請參閱 Microsoft 知識庫文章 2552221＜當使用者使用強制使用者設定檔來登入時，Lync 2010 會議功能失敗＞，網址為： [http://go.microsoft.com/fwlink/?linkid=3052\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=3052%26clcid=0x404)。

## 請參閱

#### 概念

[Lync Server 2013 中的 Lync 用戶端硬體支援](lync-server-2013-lync-client-hardware-support.md)  
[Lync Server 2013 的 Lync 用戶端視訊需求](lync-server-2013-lync-client-video-requirements.md)  
[Lync Server 2013 中舊部署支援的用戶端](lync-server-2013-supported-clients-from-previous-deployments.md)

