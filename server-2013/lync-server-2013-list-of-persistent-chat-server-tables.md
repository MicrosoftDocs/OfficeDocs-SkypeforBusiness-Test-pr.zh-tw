---
title: Lync Server 2013：常設聊天室伺服器清單表格
TOCTitle: 常設聊天室伺服器清單表格
ms:assetid: 26c9e271-3516-4d90-b930-70fec4e359ea
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg558628(v=OCS.15)
ms:contentKeyID: 49290381
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的常設聊天室伺服器清單表格

 

_**上次修改主題的時間：** 2015-03-09_

常設聊天室資料庫結構描述由下列表格所組成。

## Active Directory 同步處理


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>表格</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="lync-server-2013-tbladcookie.md">Lync Server 2013 中的 tblADCookie</a></p></td>
<td><p>包含目前輕量型目錄存取協定 (LDAP) 同步處理 Cookie。每一列都對應於 常設聊天室伺服器 正主動監控變更的 Active Directory 網域服務 網域。(本表格僅呈現和 常設聊天室伺服器 相關的 Active Directory 網域。)</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-tblprincipalmemberdifference.md">Lync Server 2013 中的 tblPrincipalMemberDifference</a></p></td>
<td><p>包含後續 Active Directory 同步處理步驟尚未處理的群組成員資格變更 (已新增及已移除的成員)，且其為第一個 Active Directory 同步處理步驟中所使用的暫時表格 (搭配 tblADUpdates 表格)。</p>
<p>僅針對 tblPrincipal 表格中所列或具有已提列成員的群組，存放及/或處理其成員資格變更。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-tbladupdates.md">Lync Server 2013 中的 tblADUpdates</a></p></td>
<td><p>包含後續 Active Directory 同步處理步驟尚未處理的 Active Directory 網域服務 變更，且其為第一個 Active Directory 同步處理步驟中所使用的暫時表格 (搭配 tblPrincipalMemberDifference 表格)。</p>
<p>僅針對 tblPrincipal 表格中已提列的主體，存放及/或處理其 Active Directory 變更。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-tblprincipalmembers.md">Lync Server 2013 中的 tblPrincipalMembers</a></p></td>
<td><p>包含主體成員資格。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-tblprincipalmeta.md">Lync Server 2013 中的 tblPrincipalMeta</a></p></td>
<td><p>包含必須從 Active Directory 重新整理的主體。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-tblskippedaffiliations.md">Lync Server 2013 中的 tblSkippedAffiliations</a></p></td>
<td><p>包含因某個原因而無法重新整理的關係 (通常原因是 Active Directory 存取錯誤)。</p>
<p>本表格之用途僅為提供資訊參考用。其內容無法使用。</p>
<p>tblPrincipalMeta 表格中會存放具有無法正確重新整理之關係的主體，並給予其另一次重新整理的機會。</p></td>
</tr>
</tbody>
</table>


## 主體、關係、節點、範圍與角色


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>表格</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="lync-server-2013-tblprincipaltype.md">Lync Server 2013 中的 tblPrincipalType</a></p></td>
<td><p>含有主體類型以分類 tblPrincipal 表格中的項目。此表格是靜態的，其會在資料庫建立期間設定，且不會變更。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-tblprincipal.md">Lync Server 2013 中的 tblPrincipal</a></p></td>
<td><p>內含所有主體，包括使用者、資料夾及群組等。 常設聊天室伺服器會將其視為一般異質清單來處理。各欄位會依據每個主體的類型而定。</p>
<p>大多數這些主體都是儲存在 Active Directory 中的物件快取複本。在這些 Active Directory 物件的 Principal 表格中建立快取複本就稱為「佈建」 。</p>
<p>部分主體是刻意建立的，而部分 Active Directory 物件則會被共同忽略。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-tblprincipalaffiliations.md">Lync Server 2013 中的 tblPrincipalAffiliations</a></p></td>
<td><p>包含主體關係，可描述 Active Directory 安全性群組、 Active Directory 容器等成員資格。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-tblnode.md">Lync Server 2013 中的 tblNode</a></p></td>
<td><p>包含類別節點，並在 Lync Server 控制台中進行管理。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-tblroletype.md">Lync Server 2013 中的 tblRoleType</a></p></td>
<td><p>是一種靜態查閱表格，含有角色類型與其相關的權限組。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-tblscopeprincipal.md">Lync Server 2013 中的 tblScopePrincipal</a></p></td>
<td><p>包含指派給節點的範圍。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-tblprincipalrole.md">Lync Server 2013 中的 tblPrincipalRole</a></p></td>
<td><p>包含指派給節點的角色。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-tblsiopwhitelist.md">Lync Server 2013 中的 tblSiopWhiteList</a></p></td>
<td><p>包含可與節點相關聯的已註冊增益集。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-tblenumattribute.md">Lync Server 2013 中的 tblEnumAttribute</a></p></td>
<td><p>僅包含 tblNode 表格中所用之「可見度」和「行為」硬式編碼屬性。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-tblenumvalue.md">Lync Server 2013 中的 tblEnumValue</a></p></td>
<td><p>僅包含 tblNode 表格中所用之「可見度」和「行為」屬性的硬式編碼值。</p></td>
</tr>
</tbody>
</table>


## 邀請、聊天以及其他用戶端支援


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>表格</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="lync-server-2013-tblprincipalinvites.md">Lync Server 2013 中的 tblPrincipalInvites</a></p></td>
<td><p>包含系統中所有啟用自動邀請的節點之所有已佈建使用者的邀請。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-tblchat.md">Lync Server 2013 中的 tblChat</a></p></td>
<td><p>包含所有聊天訊息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-tbllastinviteid.md">Lync Server 2013 中的 tblLastInviteId</a></p></td>
<td><p>含有為每個使用者產生 (也用於 tblPrincipalInvites 表格) 的最後一個邀請 ID。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-tbllastchatid.md">Lync Server 2013 中的 tblLastChatId</a></p></td>
<td><p>含有為每個使用者產生 (也用於 tblChat 表格) 的最後一個聊天 ID。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-tblpreference.md">Lync Server 2013 中的 tblPreference</a></p></td>
<td><p>包含使用者用戶端喜好設定 (僅限舊版用戶端使用)。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-tblfiletoken.md">Lync Server 2013 中的 tblFileToken</a></p></td>
<td><p>包含用於檔案傳輸的臨時權杖。每當上傳或下載檔案時， 常設聊天室服務會產生一個權杖，其可讓用戶端用來存取 Web 服務檔案存放區。</p></td>
</tr>
</tbody>
</table>


## 伺服器支援


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>表格</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="lync-server-2013-tblserveridentity.md">Lync Server 2013 中的 tblServerIdentity</a></p></td>
<td><p>包含 Persistent Chat Server 集區中的伺服器。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-tbladminlock.md">Lync Server 2013 中的 tblAdminLock</a></p></td>
<td><p>包含執行某些管理員命令所需的管理員鎖定。tblSystemRevision 表格中的系統修訂項目會在每次解除鎖定後遞增。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-tblsystemrevision.md">Lync Server 2013 中的 tblSystemRevision</a></p></td>
<td><p>包含所用的修訂編號項目 (搭配 tblAdminLock 表格) 以用於封存多部伺服器間的一致性。</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-tblactivepeers.md">Lync Server 2013 中的 tblActivePeers</a></p></td>
<td><p>包含 常設聊天室服務之間的目前對等連線。</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-tblconfig.md">Lync Server 2013 中的 tblConfig</a></p></td>
<td><p>包含 常設聊天室伺服器 不支援的設定。</p></td>
</tr>
</tbody>
</table>

