---
title: 刪除位置原則
TOCTitle: 刪除位置原則
ms:assetid: 8ca9ba10-f45f-435a-b39c-519d251e9085
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688125(v=OCS.15)
ms:contentKeyID: 49890197
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 刪除位置原則

 

_**上次修改主題的時間：** 2012-10-10_

在 Lync Server 2013 中，您可以使用位置原則，來套用與增強型 9-1-1 (E9-1-1) 功能和使用者或連絡人的位置設定相關的設定。位置原則會判斷使用者是否已啟用 E9-1-1，如果是，則會決定緊急電話的行為。例如，您可以使用位置原則來定義組成緊急電話的數字 (在美國為 911)、是否應自動告知公司的安全部門，以及應如何路由傳送來電。

您可以在 Lync Server 2013 控制台的 \[網路設定\] 群組中設定位置原則。從 Lync Server 控制台，您可以檢視、建立、修改或刪除位置原則。請使用下列程序來刪除位置原則。如需關於建立或修改位置原則的詳細資訊，請參閱＜[建立或修改位置原則](lync-server-2013-creating-or-modifying-a-location-policy.md)＞。

## 刪除位置原則

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[網路設定\]，然後按一下 \[位置原則\]。

4.  在 \[位置原則\] 頁面上，選取要刪除的位置原則。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您可以同時刪除一個以上的位置原則。若要這麼做，請按住 CTRL 鍵，然後選取一個以上的原則。或者，若要選取所有原則，請在 [編輯] 功能表上按一下 [全選]。</td>
    </tr>
    </tbody>
    </table>


5.  在 \[編輯\] 功能表中，按一下 \[刪除\]。

6.  按一下 \[確定\]。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您無法刪除全域位置原則。如果您嘗試刪除全域原則，則會出現警告訊息，且該原則將重設為預設值。</td>
    </tr>
    </tbody>
    </table>


## 請參閱

#### 工作

[建立或修改位置原則](lync-server-2013-creating-or-modifying-a-location-policy.md)  
[檢視位置原則資訊](lync-server-2013-viewing-location-policy-information.md)

