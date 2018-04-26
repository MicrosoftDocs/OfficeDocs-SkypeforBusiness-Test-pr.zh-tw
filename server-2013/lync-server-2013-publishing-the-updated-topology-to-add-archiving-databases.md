---
title: 發佈已更新的拓撲以新增封存資料庫
TOCTitle: 發佈已更新的拓撲以新增封存資料庫
ms:assetid: 454c68df-2ef5-4b5f-a44c-4eee02635d45
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204860(v=OCS.15)
ms:contentKeyID: 49290771
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 發佈已更新的拓撲以新增封存資料庫

 

_**上次修改主題的時間：** 2012-10-01_

您在拓撲產生器中更新拓樸之後，必須先將拓樸發行至中央管理存放區，才能設定和使用封存。資料的唯讀複本會複製到拓撲中的所有伺服器，讓所有伺服器與拓撲和其他設定變更保持同步。

## 發行更新的拓樸

1.  在執行 Lync Server 2013 的電腦上，或安裝 Lync Server 系統管理工具的電腦上，使用本機 Users 群組成員的帳戶 (或具有相等使用者權限的帳戶) 登入。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您可以使用屬於本機 Users 群組成員的帳戶來定義拓撲，但是若要發行拓撲 (新增伺服器至拓樸的必要作業)，則使用的帳戶必須是 <strong>[Domain Admins]</strong> 群組及 <strong>[RTCUniversalServerAdmins]</strong> 群組的成員，而且具有檔案共用的完全控制權限 (即讀取、寫入及修改)，而此檔案共用是用於 Lync Server 2013 檔案存放區，(亦即，讓拓撲產生器可以設定必要的判別存取控制清單 (DACL)，或者，使用的帳戶必須具有相等的權限。</td>
    </tr>
    </tbody>
    </table>


2.  使用拓撲產生器開啟您在上一節中建立的拓樸。

3.  在主控台樹狀目錄中，以滑鼠右鍵按一下 **\[Lync Server 2013\]**，然後按一下 **\[發行拓樸\]**。

4.  在 **\[發行拓樸\]** 頁面上，按一下 **\[下一步\]**。

5.  在 **\[建立資料庫\]** 頁面上，確認已選取資料庫，然後按一下 **\[下一步\]**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您未具備建立資料庫的適當權限，可以取消選取資料庫，讓具備適當權限的人能夠建立資料庫。如需有關所需系統管理員權限的詳細資訊，請參閱部署移轉文件<a href="lync-server-2013-deployment-permissions-for-sql-server.md">Lync Server 2013 中 SQL Server 的部署權限</a>＞。<br />
    只有專用 SQL Server 伺服器上的資料庫可以使用拓撲產生器安裝。SQL Server 伺服器上與其他伺服器元件配置在一起的資料庫必須藉由在該電腦上執行本機安裝程式的方式進行安裝。</td>
    </tr>
    </tbody>
    </table>


6.  在 **\[發行精靈完成\]** 頁面上，確認拓撲已成功發行，然後按一下 **\[完成\]**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>發行拓樸之後，您必須先為封存設定選項和原則，才能封存內容。如需詳細資訊，請參閱部署移轉文件<a href="lync-server-2013-configuring-support-for-archiving.md">在 Lync Server 2013 中設定封存支援</a>＞。</td>
    </tr>
    </tbody>
    </table>

