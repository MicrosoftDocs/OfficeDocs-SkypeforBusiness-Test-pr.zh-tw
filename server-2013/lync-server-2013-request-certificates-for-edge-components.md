---
title: Lync Server 2013：要求 Edge 元件的憑證
TOCTitle: 要求 Edge 元件的憑證
ms:assetid: 8c72b877-febc-428f-89dc-389e7a7ac849
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398708(v=OCS.15)
ms:contentKeyID: 49291600
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中要求 Edge 元件的憑證

 

_**上次修改主題的時間：** 2013-11-07_

支援外部使用者存取所需的憑證包括公用憑證授權單位 (CA) 所發出的憑證以及內部企業 CA 所發出的憑證：

  - Edge Server 的外部介面及反向 Proxy 所需的憑證必須由公用 CA 所發出。

  - 內部介面所需的憑證可以由公用 CA 或內部企業 CA 發出。建議使用內部 Windows Server 2008 CA、 Windows Server 2008 R2 CA、 Windows Server 2012 CA 或 Windows Server 2012 R2 CA 來建立這些憑證，以節省使用公用憑證的費用。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>處理憑證要求 (特別是公用 CA 的要求) 需要一些時間，因此應該及早要求 Edge Server 的憑證，以確保在您啟動 Edge Server 元件的部署時有憑證可用。如需 Edge Server 的憑證需求摘要，請參閱＜ <a href="lync-server-2013-certificate-requirements-for-external-user-access.md">Lync Server 2013 中的外部使用者存取的憑證需求</a>＞。</td>
</tr>
</tbody>
</table>


儘管您可以選擇將公用 CA 用於內部邊緣介面，不過我們還是建議您改將內部企業 CA 用於其他憑證，以將憑證的成本降到最低。如需 Edge Server 的憑證需求摘要，請參閱＜ [Lync Server 2013 中的外部使用者存取的憑證需求](lync-server-2013-certificate-requirements-for-external-user-access.md)＞。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在安裝 Edge Server 時，安裝程式包含的憑證精靈可簡化要求、指派及安裝憑證等工作，如 <a href="lync-server-2013-set-up-edge-certificates.md">針對 Lync Server 2013 設定 Edge 憑證</a>一節所述。如果您想要在安裝 Edge Server 之前要求憑證 (以便節省實際部署 Edge Server 元件的時間)，只要確定憑證可匯出且含有所有必要的主體別名，即可使用內部伺服器要求憑證。本文件未提供使用內部伺服器要求憑證的程序。</td>
</tr>
</tbody>
</table>


## 從公用 CA 要求憑證

您的 Edge Server 部署會要求單一可供 Edge Server 外部介面使用的公用憑證，這個公用憑證適用於 Access Edge Service、 Web Conferencing Edge Service 及 A/V 驗證服務。這個憑證必須要有可匯出的私密金鑰，才能確保 A/V 驗證服務會在集區的所有 Edge Server 上使用相同的金鑰。搭配 Microsoft Internet Security and Acceleration (ISA) Server 2006 或 Microsoft Forefront Threat Management Gateway 2010 的反向 Proxy 亦需要公用憑證。

## 從內部企業 CA 請求憑證

內部邊緣介面所需的憑證，可由公用憑證授權單位 (CA) 或內部 CA 核發。使用內部企業 CA 有助於降低憑證成本。如果您的組織已部署內部 CA，內部邊緣的憑證即應由內部 CA 核發。以內部企業 CA 核發內部憑證，可降低憑證成本。

如需 Edge 元件的憑證需求摘要，請參閱＜ [Lync Server 2013 中的外部使用者存取的憑證需求](lync-server-2013-certificate-requirements-for-external-user-access.md)＞。如需關於使用公用 CA 取得憑證的詳細資訊，請參閱＜ [在 Lync Server 2013 中要求 Edge 元件的憑證](lync-server-2013-request-certificates-for-edge-components.md)＞。如需關於要求、安裝及指派憑證的詳細資訊，請參閱＜ [針對 Lync Server 2013 設定 Edge 憑證](lync-server-2013-set-up-edge-certificates.md)＞。

