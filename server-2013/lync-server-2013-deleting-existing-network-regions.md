---
title: 刪除現有網路地區
TOCTitle: 刪除現有網路地區
ms:assetid: c7293a2f-2b49-4c4a-903f-f7edcea2bc5f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721882(v=OCS.15)
ms:contentKeyID: 49890305
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 刪除現有網路地區

 

_**上次修改主題的時間：** 2013-02-21_

網路地區可將網路的不同部分跨多個地理區域互連。每個網路地區都必須與中央網站產生關聯。中央網站是資料中心網站，通話許可控制 (CAC) 頻寬原則服務會在其上執行。您可以使用 Lync Server 控制台來設定網路地區。網路地區包含的設定可判斷是否允許透過網際網路的替代路徑用於音訊和視訊連線。您可以從 Lync Server 控制台建立、修改或刪除網路地區。請使用本主題刪除現有的網路地區。如需關於建立或修改現有網路地區的詳細資訊，請參閱[建立或修改網路地區](lync-server-2013-creating-or-modifying-network-regions.md)

## 刪除網路地區

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[網路設定\]，然後按一下 \[地區\]。

4.  在 \[地區\] 頁面上，按一下您要刪除的地區。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您一次可以刪除一個以上的地區。若要這樣做，請按 CTRL，並在按住 CTRL 鍵時選取一個以上的地區。或者，若要選取所有地區，請在 [編輯] 功能表上按一下 [全選]。</td>
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
    <td>如果網路地區與某個網站相關聯，則無法移除該地區。如果您嘗試移除與網站相關聯的地區，則會收到錯誤訊息。若要查看某個地區是否與任何網站相關聯，請選取該地區，然後在 [編輯] 功能表上，按一下 [顯示詳細資料]。</td>
    </tr>
    </tbody>
    </table>


## 請參閱

#### 工作

[建立或修改網路地區](lync-server-2013-creating-or-modifying-network-regions.md)

