---
title: 建立或修改網站
TOCTitle: 建立或修改網站
ms:assetid: 358aa08a-c5bc-45fc-8017-19e6202f88c5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg520975(v=OCS.15)
ms:contentKeyID: 49290559
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 建立或修改網站

 

_**上次修改主題的時間：** 2012-10-08_

網站是設定在通話許可控制 (CAC) 或增強型 9-1-1 部署之每一個地區內部的辦公室或位置。您可以使用 Microsoft Lync Server 2013 控制台來設定網站，並將網站關聯至地區。例如，北美洲的網路地區可能會和 Chicago、Redmond 及 Vancouver 等網站相關聯。您必須為組織內的每個網站建立 CAC 網站，即使該網站沒有頻寬限制。從 Lync Server 控制台，您可以建立、修改及刪除網站。請使用下列程序來建立或修改網站。如需有關刪除現有網站的詳細資訊，請參閱＜[刪除現有的網站](lync-server-2013-deleting-an-existing-network-site.md)＞。

## 若要建立網路網站

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 **\[網路設定\]** 和 **\[網站\]**。

4.  在 **\[網站\]** 頁面上，按 **\[新增\]**。

5.  在 **\[新增網站\]** 的 **\[名稱\]** 欄位中，輸入網站的名稱。
    
    > [!NOTE]  
    > 網站名稱在 Lync Server 2013 部署中必須是唯一的。
    


6.  在 **\[地區\]** 下拉式清單中，選取要與此網站產生關聯的網域地區。

7.  (選用) 如果您要對此網站的音訊或視訊通話限制頻寬，請從 **\[頻寬原則\]** 下拉式清單中選取含有適當設定的頻寬原則設定檔。
    
    > [!NOTE]  
    > 您可以在 <strong>[網路設定]</strong> 群組的 <strong>[原則設定檔]</strong> 頁面上，檢視可用頻寬原則設定檔的詳細資訊，或是建立新的頻寬原則設定檔。如需詳細資訊，請參閱＜<a href="lync-server-2013-creating-or-modifying-bandwidth-policy-profiles.md">建立或修改頻寬原則設定檔</a>＞。
    


8.  (選用) 如果您要提供此網站的位置設定，請從 **\[位置原則\]** 下拉式清單中選取位置原則。
    
    > [!NOTE]  
    > 此位置原則將特定的增強型 9-1-1 (E9-1-1) 功能和用戶端位置設定指派給網站。您可以在 <strong>[網路設定]</strong> 群組的 <strong>[位置原則]</strong> 頁面上，檢視可用位置原則的詳細資訊，或是建立新的位置原則。如需詳細資訊，請參閱＜<a href="lync-server-2013-viewing-location-policy-information.md">檢視位置原則資訊</a>＞。
    


9.  (選用) 在 **\[描述\]** 欄位中輸入值，提供無法用名稱完整表達的網站的其他資訊。

10. 按一下 **\[認可\]**。
    
    > [!NOTE]  
    > 建立新的網路網站時不會使用 <strong>[關聯的子網路]</strong> 表格。建立或修改子網路時才會讓子網路與網站相關聯。如需詳細資訊，請參閱＜<a href="lync-server-2013-create-or-modify-network-subnets.md">建立或修改網路子網路</a>＞。
    


## 修改網路網站

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 **\[網路設定\]** 和 **\[網站\]**。

4.  在 **\[網站\]** 頁面中，按一下您要修改的網站。

5.  在 **\[編輯\]** 功能表上，按一下 **\[顯示詳細資料\]**。

6.  在 **\[編輯網站\]** 頁面上，您可以修改與網站相關聯的描述、地區、頻寬原則設定檔和位置原則。如需詳細資訊，請參閱本主題稍早的＜若要建立網路網站＞一節。

7.  按一下 **\[認可\]**。

您無法修改此頁面上的 **\[關聯的子網路\]** 表格。關聯的子網路清單僅供參考，讓您知道修改網站設定會影響哪些子網路。

## 若要刪除網路網站

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 **\[網路設定\]** 和 **\[網站\]**。

4.  在 **\[網站\]** 頁面上，按一下您要刪除的網站。
    
    > [!NOTE]  
    > 您可以一次刪除多個網站。若要這樣做，請按 CTRL 並在按住 CTRL 鍵的同時選取多個網站。或者，若要選取所有網站，請按一下 <strong>[編輯]</strong> 功能表上的 <strong>[全選]</strong>。
    


5.  在 **\[編輯\]** 功能表中，按一下 **\[刪除\]**。

6.  按一下 **\[確定\]**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>但是如果網站與某個網路子網路相關聯時，則無法移除該網路網站。如果您嘗試移除與子網路相關聯的網站，則會收到錯誤訊息。若要查看網站是否與子網路相關聯，請按一下網站並按一下 <strong>[編輯]</strong> 功能表上的 <strong>[顯示詳細資料]</strong>。</td>
    </tr>
    </tbody>
    </table>


## 請參閱

#### 工作

[刪除現有的網站](lync-server-2013-deleting-an-existing-network-site.md)  

#### 其他資源

[New-CsNetworkSite](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsNetworkSite)  
[Set-CsNetworkSite](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsNetworkSite)  
[Remove-CsNetworkSite](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsNetworkSite)  
[Get-CsNetworkSite](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsNetworkSite)

