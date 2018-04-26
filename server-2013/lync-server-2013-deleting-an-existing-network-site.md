---
title: 刪除現有的網站
TOCTitle: 刪除現有的網站
ms:assetid: 2762149b-3572-4513-b838-beda7fa9e81e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688001(v=OCS.15)
ms:contentKeyID: 49889986
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 刪除現有的網站

 

_**上次修改主題的時間：** 2012-11-01_

網路網站是設定在通話許可控制 (CAC) 或增強型 9-1-1 部署之每一個地區內部的辦公室或位置。您可以使用 Lync Server 2013 控制台來設定網站，並將網站關聯至區域。例如，北美洲的網路區域可能會和 Chicago、Redmond 及 Vancouver 等網路網站相關聯。您必須為組織內的每個網站建立 CAC 網路網站，即使該網站沒有頻寬限制。從 Lync Server 控制台，您可以建立、修改或刪除網路網站。使用下列程序刪除現有網路網站。如需建立或修改網路網站的詳細資訊，請參閱＜[建立或修改網站](lync-server-2013-creating-or-modifying-network-sites.md)＞

## 刪除網路網站

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 \[網路設定\] 和 \[網站\]。

4.  在 \[網站\] 頁面上，按一下您要刪除的網站。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您可以一次刪除多個網站。若要這樣做，請按 CTRL 並在按住 CTRL 鍵的同時選取多個網站。或者，若要選取所有網站，請按一下 [編輯] 功能表上的 [全選]。</td>
    </tr>
    </tbody>
    </table>


5.  在 \[編輯\] 功能表中，按一下 \[刪除\]。

6.  按一下 \[確定\]。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>但是如果網站與某個網路子網路相關聯時，則無法移除該網路網站。如果您嘗試移除與子網路相關聯的網站，則會收到錯誤訊息。若要查看網站是否與子網路相關聯，請按一下網站並按一下 [編輯] 功能表上的 [顯示詳細資料]。</td>
    </tr>
    </tbody>
    </table>

