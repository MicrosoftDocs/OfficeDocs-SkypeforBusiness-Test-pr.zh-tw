---
title: Lync Server 2013：會議規劃
TOCTitle: 會議規劃
ms:assetid: 983a272a-e1b3-4d70-8f84-836b092fe526
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398781(v=OCS.15)
ms:contentKeyID: 49291741
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的會議規劃

 

_**上次修改主題的時間：** 2013-01-29_

Lync Server 2013 提供一組豐富的會議功能：

  - Web 會議 (包括文件共同作業、應用程式共用及桌面共用)。 Lync Server 2013 使用 Office Web Apps 和 Office Web Apps Server 來處理 PowerPoint 簡報的共用和轉譯。如需關於安裝及設定 Office Web Apps Server 的詳細資訊，請參閱＜ [設定 Office Web Apps Server 與 Lync Server 2013 的整合](lync-server-2013-enabling-office-web-apps-server-and-lync-server-2013.md)＞。

  - 音訊/視訊 (A/V) 會議 - 讓使用者在不需要 Microsoft Live Meeting 服務等外部服務或是協力廠商音訊橋接器的情況下，舉行即時的音訊或視訊會議。

  - 電話撥入式會議 - 讓使用者在不需要協力廠商音訊會議提供者的情況下，使用公用交換電話網路 (PSTN) 電話加入 Lync Server 2013 會議的音訊部分。

  - 立即訊息 (IM) 會議 - 讓多方人員在單一 IM 工作階段中進行溝通。如需關於 IM 會議的詳細資訊，請參閱＜ [在 Lync Server 2013 中規劃前端伺服器、立即訊息及顯示狀態](lync-server-2013-planning-for-front-end-servers-instant-messaging-and-presence.md)＞。

Lync Server 2013 同時支援排程的會議和即席的會議。

在部署 Lync Server 2013前端伺服器時，您可以選擇是否要一同部署 Web 會議、A/V 會議及電話撥入式會議功能。IM 會議功能一律會隨著 Lync Server 2013  前端伺服器上的 IM 交談功能自動部署。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果部署包含利用 Office Communicator 2007 R2 用戶端 (包含 Live Meeting 主控台或 Microsoft Office Outlook 會議增益集) 召集的會議，則在移轉至 Lync Server 2013 之後，會議將會有以下限制：
<ul>
<li><p>會議中的使用者將無法使用資料共同作業功能，包含文件共同作業、應用程式共用，以及桌面共用。</p></li>
<li><p>由於 Office Communicator 2007 R2 用戶端未受 Lync Server 2013 支援，可能會出現穩定性問題。</p></li>
</ul>
為了避免這些問題，請透過使用 Outlook 2010 的 Office Communicator 2007 R2 用戶端，或使用 Lync 2010 的線上會議增益集或 Lync 2013 的線上會議增益集的 Outlook 2013 來重新排程召集的會議。</td>
</tr>
</tbody>
</table>


以下小節說明各種類型之會議功能的部署需求，包括規劃程序、元件、硬體和軟體需求及部署程序。

## 本章節內容

  - [Lync Server 2013 中的會議概觀](lync-server-2013-overview-of-conferencing.md)

  - [在 Lync Server 2013 中定義會議需求](lync-server-2013-defining-your-requirements-for-conferencing.md)

  - [Lync Server 2013 中的會議元件與拓撲](lync-server-2013-components-and-topologies-for-conferencing.md)

  - [Lync Server 2013 中會議的技術需求](lync-server-2013-technical-requirements-for-conferencing.md)

  - [Lync Server 2013 中的會議部署檢查清單](lync-server-2013-deployment-checklist-for-conferencing.md)

  - [Lync Server 2013 中的大型會議支援](lync-server-2013-support-for-large-meetings.md)

