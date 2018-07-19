---
title: 設定網路區域連結
TOCTitle: 設定網路區域連結
ms:assetid: 952bc93e-e6aa-4539-85c7-2b15f14eb382
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182551(v=OCS.15)
ms:contentKeyID: 49291716
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定網路區域連結

 

_**上次修改主題的時間：** 2012-11-01_

您可以將兩個網路地區間的連結設定為通話許可控制 (CAC) 的一部分。網路中的地區是透過實體廣域網路 (WAN) 連線相連結。您可以使用 Lync Server 控制台來定義兩個網路地區之間的連結，並設定這些地區之間音訊和視訊連線的頻寬限制。如需關於刪除現有網路地區連結的詳細資訊，請參閱＜[刪除網路地區連結](lync-server-2013-deleting-network-region-links.md)＞。

## 若要建立網路地區連結

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  按一下左導覽列中的 \[網路設定\]，然後按一下 \[地區連結\]。

4.  按一下 **\[地區連結\]** 頁面中的 **\[新增\]**。

5.  在 **\[新地區連結\]** 頁面的 **\[名稱\]** 欄位中輸入值。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>此值在您的 Lync Server 2013 部署中必須是唯一的。</td>
    </tr>
    </tbody>
    </table>


6.  在 **\[網路地區 \#1\]** 下拉式清單中選取一個或兩個要連結的地區。

7.  在 \[網路地區 \#2\] 下拉式清單中選取其他要連結的地區。此地區必須與選取為網路地區 \#1 的地區不同。

8.  (選用) 如果您想要限制這些地區的音訊或視訊通話頻寬，請在 **\[頻寬原則\]** 下拉式清單中選取頻寬原則設定檔。

9.  按一下 \[認可\]。

## 若要修改網路地區連結

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  按一下左導覽列中的 \[網路設定\]，然後按一下 \[地區連結\]。

4.  在 **\[地區連結\]** 頁面中按一下要修改的地區連結。

5.  在 \[編輯\] 功能表上，按一下 \[顯示詳細資料\]。

6.  在 **\[編輯地區連結\]** 中修改已連結的地區或此連結的頻寬原則設定檔。

7.  按一下 \[認可\]。

## 請參閱

#### 工作

[刪除網路地區連結](lync-server-2013-deleting-network-region-links.md)  

#### 其他資源

[New-CsNetworkRegionLink](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsNetworkRegionLink)  
[Set-CsNetworkRegionLink](href: https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsNetworkRegionLink)  
[Remove-CsNetworkRegionLink](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsNetworkRegionLink)  
[Get-CsNetworkRegionLink](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsNetworkRegionLink)

