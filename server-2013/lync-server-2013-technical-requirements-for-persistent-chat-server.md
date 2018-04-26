---
title: Lync Server 2013：常設聊天室伺服器的技術需求
TOCTitle: 常設聊天室伺服器的技術需求
ms:assetid: 692b7d99-1bc9-4c99-a050-2bc2be8688b2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398495(v=OCS.15)
ms:contentKeyID: 49291195
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中常設聊天室伺服器的技術需求

 

_**上次修改主題的時間：** 2015-03-09_

將裝載 常設聊天室伺服器 的每部電腦都必須能夠存取具有下列元件的現有 Lync Server 2013 拓撲：

  - **Lync Server 2013， 前端伺服器。**前端伺服器是工作階段初始通訊協定 (SIP) 路由的基礎，可讓通訊在執行 常設聊天室伺服器 和 常設聊天室功能的電腦之間得以進行。在您開始部署 常設聊天室伺服器 之前，請驗證 Lync Server 2013、Standard Edition 或 Lync Server前端集區和執行 Lync Server 之任何其他內部電腦的部署是否適合您的組織。

下列各節說明 常設聊天室伺服器 以及儲存 常設聊天室資料之資料庫的特定需求。

## 常設聊天室伺服器需求

如需部署 Lync Server 及最新版 常設聊天室伺服器 之建議硬體的詳細資訊，請參閱支援文件中的 [Lync Server 2013 的伺服器硬體平台](lync-server-2013-server-hardware-platforms.md)。

如需 Lync Server 及 常設聊天室伺服器 之伺服器及工具作業系統支援的詳細資訊，請參閱支援文件中的 [Lync Server 2013 中的伺服器及工具作業系統支援](lync-server-2013-server-and-tools-operating-system-support.md)。

如需部署 常設聊天室伺服器 所需其他軟體的詳細資訊，請參閱下表。

### 常設聊天室伺服器 軟體先決條件

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>軟體</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>訊息佇列</p></td>
<td><p>供 常設聊天室伺服器 和 常設聊天室 Compliance Service 使用 (若已部署)。</p></td>
</tr>
</tbody>
</table>


## 常設聊天室伺服器 資料庫需求

常設聊天室伺服器 使用 常設聊天室資料庫來儲存交談記錄、設定和使用者佈建資料。該伺服器也可選擇使用 常設聊天室規範資料庫來儲存規範資料。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>常設聊天室資料庫 (MGC) 和規範資料庫 (Mgccomp) 可位於相同的 SQL Server 執行個體或不同的 SQL Server 上。</td>
</tr>
</tbody>
</table>


若要準備資料庫伺服器平台，請確定每部電腦都符合硬體需求，然後安裝必要軟體。

常設聊天室資料庫伺服器的伺服器平台所需的硬體與 Lync Server 後端資料庫伺服器相同。如需詳細資訊，請參閱支援文件中的 [Lync Server 2013 的伺服器硬體平台](lync-server-2013-server-hardware-platforms.md)。

在資料庫伺服器上，確定已安裝下列其中一個軟體應用程式：

  - Microsoft SQL Server 2012。如需如何安裝 Microsoft SQL Server 2012 的詳細資訊，請參閱＜安裝 SQL Server 2012＞，網址為 <http://go.microsoft.com/fwlink/?linkid=248559>。

  - Microsoft SQL Server 2008 R2。如需如何安裝 Microsoft SQL Server 2008 R2 的詳細資訊，請參閱＜SQL Server 安裝 (SQL Server 2008 R2)＞，網址為 <http://go.microsoft.com/fwlink/?linkid=275702>。

## 常設聊天室伺服器 憑證需求

如需了解取得憑證、建立 SQL Server 資料庫與建立檔案存放區的詳細資訊，請參閱部署文件中的 [部署 Lync Server 2013](lync-server-2013-deploying-lync-server.md)。

