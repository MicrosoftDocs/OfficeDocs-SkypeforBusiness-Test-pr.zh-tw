---
title: 建立或修改網路地區路由
TOCTitle: 建立或修改網路地區路由
ms:assetid: 76993daa-76c2-4cec-8363-de8aebef0145
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg521016(v=OCS.15)
ms:contentKeyID: 49291359
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 建立或修改網路地區路由

 

_**上次修改主題的時間：** 2012-10-08_

通話許可控制服務 (CAC) 組態內的每個地區，都必須要有辦法存取其他每個地區。地區連結會設定地區間連線的頻寬限制，也代表實體連結，而路由會決定從甲地連線到乙地時要採取的連結路徑。您可以使用 Lync Server 控制台來設定網路地區路由。您可以從 Lync Server 控制台建立、修改或刪除網路地區路由。若要建立或修改網路地區路由，請利用本節主題。如需有關刪除現有網路地區路由的詳細資訊，請參閱＜[刪除現有的網路地區路由](lync-server-2013-deleting-existing-network-region-routes.md)＞。

## 若要建立網路地區路由

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 **\[網路設定\]** 和 **\[地區路由\]**。

4.  在 **\[地區路由\]** 頁面上，按一下 **\[新增\]**。

5.  在 **\[新的地區路由\]** 的 **\[名稱\]** 欄位中，輸入一個值。
    
    > [!NOTE]  
    > 此值在您的 Microsoft Lync Server 2013 部署中必須是唯一的。
    


6.  從 **\[網路地區 \#1\]** 下拉式清單中，選取要以此路由相連的兩個地區中的其中一個地區。

7.  從 \[網路地區 \#2\] 下拉式清單中，選取此路由的另一個地區。此地區必須與選取為網路地區 \#1 的地區不同。

8.  使用 **\[網路地區連結\]** 清單方塊，將地區連結新增至路由。按一下 **\[新增\]** 按鈕以顯示 **\[地區連結\]** 頁面。按一下要新增至此路由的地區連結，然後按一下 **\[確定\]**。
    
    > [!NOTE]  
    > 若要新增更多連結，請繼續按 <strong>[新增]</strong> 按鈕；若要移除連結，請選取連結，然後按一下 <strong>[移除]</strong>。
    


9.  按一下 **\[認可\]**。

## 若要修改網路地區路由

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 **\[網路設定\]** 和 **\[地區路由\]**。

4.  在 **\[地區路由\]** 頁面上，按一下您要修改的地區路由。

5.  在 **\[編輯\]** 功能表上，按一下 **\[顯示詳細資料\]**。

6.  在 **\[編輯地區路由\]** 中，您可以修改此路由所聯結的地區，以及與路由相關聯的地區連結。

7.  按一下 **\[認可\]**。

## 請參閱

#### 工作

[刪除現有的網路地區路由](lync-server-2013-deleting-existing-network-region-routes.md)

