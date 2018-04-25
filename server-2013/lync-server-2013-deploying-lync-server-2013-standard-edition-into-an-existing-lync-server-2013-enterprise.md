---
title: Lync Server 2013：將 Lync Server 2013 Standard Edition 部署到現有 Lync Server 2013 Enterprise 中
TOCTitle: 將 Lync Server 2013 Standard Edition 部署到現有 Lync Server 2013 Enterprise 中
ms:assetid: 05ea128d-6c94-49b3-b28b-477367196425
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398112(v=OCS.15)
ms:contentKeyID: 49289967
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 將 Lync Server 2013 Standard Edition 部署到現有 Lync Server 2013 Enterprise 中

 

_**上次修改主題的時間：** 2012-10-01_

將 Standard Edition 伺服器 部署至現有 Enterprise Edition 部署，與部署其他伺服器角色類似。 Standard Edition 伺服器 可部署至另一個網站，允許該網站中的使用者位於 Standard Edition 伺服器，而不是跨廣域網路 (WAN) 的 前端集區。在該網站中安裝新網站及伺服器的程序已定義於＜ [部署 Lync Server 2013](lync-server-2013-deploying-lync-server.md)＞文件的其他小節中。

**若要定義新網站**

1.  啟動拓撲產生器：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 拓撲產生器\]。

2.  在主控台樹狀目錄中，以滑鼠右鍵按一下 \[ Lync Server 2013\] ，然後按一下 \[新增中央網站\] 。

3.  在 **\[識別網站\]** 頁面上，提供網站的名稱並選擇性輸入描述。

4.  遵循用於定義網站拓撲其餘部分的程序。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中定義和設定拓撲](lync-server-2013-defining-and-configuring-the-topology.md)＞。

5.  發行更新後的拓撲。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中發行拓撲](lync-server-2013-publish-the-topology.md)＞。

6.  設定及安裝 Standard Edition 伺服器。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ205186.Caution(OCS.15).gif" title="Caution" alt="Caution" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您已部署僅具有 Standard Edition 伺服器 的環境，則您可能已透過下列動作從 [ Lync Server 部署精靈] 開始進行設定程序：使用 [準備第一個 Standard Edition Server] 連結將初始資料庫檔案安裝至新的 Standard Edition 伺服器。將 Standard Edition 伺服器 安裝到現有 Lync Server 2013 部署時， <strong>請勿</strong>遵循該程序。</td>
    </tr>
    </tbody>
    </table>

