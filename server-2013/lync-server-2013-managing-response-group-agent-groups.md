---
title: 管理回應群組代理程式群組
TOCTitle: 管理回應群組代理程式群組
ms:assetid: 36084cdc-38f1-4c45-922f-f81c7e86210c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg520976(v=OCS.15)
ms:contentKeyID: 49290567
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 管理回應群組代理程式群組

 

_**上次修改主題的時間：** 2012-10-01_

代理人群組是由一組指定用來接聽打給回應群組之電話的人員所組成。當您建立代理人群組時，需要選取指派給該群組的代理人，並指定其他群組設定，例如，路由方法，以及代理人是否可以登入和登出群組。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用者必須能使用企業語音，您才能將他們新增至代理人群組。如需有關為使用者啟用企業語音的詳細資訊，請參閱＜<a href="lync-server-2013-enable-users-for-enterprise-voice.md">在 Lync Server 2013 中為使用者啟用企業語音</a>＞。</td>
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
<td>只有內部部署的使用者可以成為代理人。如果將代理人從內部部署移至線上，回應群組電話將無法路由傳送給該代理人。</td>
</tr>
</tbody>
</table>


必須登入和登出群組 (與登入或登出 Lync Server 不同) 的代理人稱為*「正式代理人」*。正式代理人必須先登入此群組，才可以接聽路由傳送到此群組的電話。對於以兼職身分接聽群組來電的代理人而言，這可能相當實用。正式代理人可按一下 Lync 2013 中的功能表項目，開啟 Windows Internet Explorer 網際網路瀏覽器並顯示網頁主控台，以登入和登出其群組。

未登入或登出群組的代理人稱為*「非正式代理人」*。非正式代理人會在登入 Lync Server 時自動登入群組，但無法登出群組。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您將使用者指派為回應群組代理人時，如果他們已啟用隱私權模式，請通知他們需要搜尋 &quot;RGS Presence Watcher&quot; 連絡人並將他們新增到其連絡人清單。已啟用隱私權模式但其連絡人清單中沒有 &quot;RGS Presence Watcher&quot; 的代理人，無法接收到打給回應群組的電話。未啟用隱私權模式的代理人則不受影響。</td>
</tr>
</tbody>
</table>


## 本章節內容

  - [在 Lync Server 2013 中建立或修改代理人群組](lync-server-2013-create-or-modify-an-agent-group.md)

  - [刪除專員群組](lync-server-2013-delete-an-agent-group.md)

