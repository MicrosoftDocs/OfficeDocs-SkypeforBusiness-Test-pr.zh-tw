---
title: Lync Server 2013：常設聊天室伺服器的部署檢查清單
TOCTitle: 常設聊天室伺服器的部署檢查清單
ms:assetid: b1108f8f-88a2-4660-8086-d25ba76f7239
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412851(v=OCS.15)
ms:contentKeyID: 49292026
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的常設聊天室伺服器的部署檢查清單

 

_**上次修改主題的時間：** 2015-03-09_

Lync Server 2013常設聊天室伺服器 的部署必須依照正確的順序進行，並且完成所有必要的部署步驟。

## 部署順序

您可以在部署初始拓撲之後部署 常設聊天室伺服器，至少包括一個 Lync Server 2013前端集區，或一部 Lync Server 2013Standard Edition 伺服器。本主題描述如何藉由將 常設聊天室伺服器 加入至現有部署的方式進行部署。

## 部署程序

下表列出部署 常設聊天室伺服器 的基本步驟，並提供詳細資訊的連結。

### 常設聊天室伺服器 部署程序

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>工作</th>
<th>步驟</th>
<th>必要角色和群組成員資格</th>
<th>相關主題</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>安裝先決條件硬體與軟體</strong></p></td>
<td><p>在符合系統需求的硬體上，安裝下列各項：</p>
<ul>
<li><p>在 常設聊天室伺服器前端伺服器 上：</p></li>
</ul>
<ul>
<li><p>符合系統需求的作業系統</p></li>
<li><p>執行 Lync Server 2013 之電腦的軟體先決條件</p></li>
<li><p>將主控 常設聊天室伺服器 資料庫的伺服器上具有 SQL Server</p></li>
</ul>
<p>如果需要 常設聊天室伺服器 規範：</p>
<ul>
<li><p>將主控 常設聊天室伺服器 規範資料庫的伺服器上具有 SQL Server</p></li>
</ul></td>
<td><p>屬於本機 Administrators 群組成員的任何使用者。</p></td>
<td><p>支援文件中的 <a href="lync-server-2013-supported-hardware.md">Lync Server 2013 的受支援硬體</a>。</p>
<p>支援文件中的 <a href="lync-server-2013-server-software-and-infrastructure-support.md">Lync Server 2013 中的伺服器軟體和基礎結構支援</a>。</p>
<p><a href="lync-server-2013-determining-your-system-requirements.md">判定 Lync Server 2013 的系統需求</a></p>
<p><a href="lync-server-2013-technical-requirements-for-persistent-chat-server.md">Lync Server 2013 中常設聊天室伺服器的技術需求</a></p></td>
</tr>
<tr class="even">
<td><p><strong>建立適當的內部拓撲以支援 常設聊天室伺服器 (並選擇性支援 常設聊天室 規範)</strong></p></td>
<td><p>執行 拓撲產生器，將 Persistent Chat Server 集區新增至您的拓撲：</p>
<ul>
<li><p>將 常設聊天室伺服器 元件新增至拓撲</p></li>
<li><p>為 常設聊天室伺服器 存放區建立 SQL Server 資料庫 (並備份 SQL Server 供災害復原之用)</p></li>
<li><p>定義新 Lync 檔案存放區或使用現有 Lync File Store for 常設聊天室伺服器 檔案</p></li>
<li><p>將可路由要求的 Lync Server 2013 集區關聯至此 Persistent Chat Server 集區</p></li>
</ul>
<p>如果需要 常設聊天室 規範：</p>
<ul>
<li><p>新增 常設聊天室 規範存放區</p></li>
<li><p>按一下 Persistent Chat Server 集區 定義核取方塊來啟用規範</p></li>
<li><p>發行拓撲</p></li>
</ul>
<p>如果您在 Standard Edition 上安裝 常設聊天室伺服器， Persistent Chat Server 集區的完整網域名稱 (FQDN) 必須符合 Standard Edition 伺服器，且 SQL Server 資料庫會組合在 Standard Edition 伺服器上的 SQL Server Express 執行個體</p></td>
<td><p>若要定義拓撲，使用屬於本機 Users 群組成員的帳戶。</p>
<p>若要發行拓撲，則使用屬於 Domain Admins 群組和 RTCUniversalServerAdmins 群組成員的帳戶，且使用者應該也擁有在 Lync File Store for 常設聊天室伺服器 檔案上的完整控制權限 (讀取/寫入/修改) (讓拓撲產生器可以設定必要的 DACL)。</p></td>
<td><p>部署文件中的＜ <a href="lync-server-2013-adding-persistent-chat-server-to-your-deployment.md">在 Lync Server 2013 中將常設聊天室伺服器新增至您的部署</a>＞</p></td>
</tr>
<tr class="odd">
<td><p><strong>部署 常設聊天室伺服器</strong></p></td>
<td><p>在執行 常設聊天室伺服器 的所有電腦上執行 Lync Server 安裝。 常設聊天室伺服器 安裝已整合至 Lync Server 2013 部署精靈，精靈提供下列指示：</p>
<ul>
<li><p>部署本機管理存放區</p></li>
<li><p>安裝 常設聊天室伺服器 服務</p></li>
<li><p>要求並指派憑證</p></li>
<li><p>執行與啟動服務</p></li>
</ul></td>
<td><p>屬於本機 Administrators 群組成員的任何使用者。</p></td>
<td><p>部署文件中的＜ <a href="lync-server-2013-deploying-persistent-chat-server.md">在 Lync Server 2013 中部署常設聊天室伺服器</a>＞</p></td>
</tr>
<tr class="even">
<td><p><strong>建立 常設聊天室系統管理員</strong></p></td>
<td><p>將使用者新增至 CsPersistentChatAdministrator 安全性群組。</p></td>
<td><p>屬於網域 Administrators 成員的任何使用者。</p></td>
<td><p>部署文件中的＜ <a href="lync-server-2013-adding-a-persistent-chat-administrator.md">在 Lync Server 2013 中新增常設聊天室管理員</a>＞</p></td>
</tr>
<tr class="odd">
<td><p><strong>設定 常設聊天室伺服器</strong></p></td>
<td><p>設定使用者：</p>
<ul>
<li><p>必須使用原則存取 常設聊天室伺服器 以啟用使用者。依預設，所有使用者的原則為關閉，且可在全域/網站/集區/使用者範圍上定義原則。</p></li>
<li><p>進行設定</p></li>
</ul></td>
<td><p>使用者必須為 CsPersistentChatAdministrator 成員。若要變更原則，使用者至少必須為 CsUserAdministrator。</p></td>
<td><p>部署文件中的＜ <a href="lync-server-2013-configuring-persistent-chat-server.md">在 Lync Server 2013 中設定常設聊天室伺服器</a>＞</p></td>
</tr>
</tbody>
</table>


> [!IMPORTANT]  
> 您可以部署一或多個 Persistent Chat Server 集區。我們支援多個 Persistent Chat Server 集區，然而因法規的規範，指定區域產生的資料必須留在該區域中。例如，如果您在芝加哥部署一個 Persistent Chat Server 集區，在蘇黎世部署另一個以符合瑞士對資料的規範，使用者若有存取權，則可連線至這兩個 Persistent Chat Server 集區中的聊天室。


