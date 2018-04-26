---
title: 確認已完成使用者複製
TOCTitle: 確認已完成使用者複製
ms:assetid: 199dc9de-b555-468f-a42a-9e92ea6c9053
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204712(v=OCS.15)
ms:contentKeyID: 49290238
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 確認已完成使用者複製

 

_**上次修改主題的時間：** 2012-09-28_

執行 **Move-CsLegacyUser** Cmdlet 時，可能會因為資料庫一開始的複寫不完整，導致 Active Directory 網域服務 (AD DS) 與 Lync Server 2013 資料庫之間的使用者資訊不同步，而發生失敗的情況。成功完成 Lync Server 2013 使用者複寫器服務的初始同步化所需花費的時間，取決於主控 Lync Server 2013 集區的 Active Directory 樹系所主控的網域控制站數量。 Lync Server 2013 前端伺服器第一次啟動時，會開始進行 Lync Server 2013 使用者複寫器服務的初始同步處理程序。完成後，則是根據使用者複寫器間隔來進行同步化。在執行 **Move-CsLegacyUser** Cmdlet 之前，請完成下列步驟來確認已完成使用者複寫。

## 確認使用者複寫已完成

1.  從 Lync Server 2013 前端伺服器按一下 \[開始\] 功能表，然後按一下 \[執行\] 。

2.  輸入 **eventvwr.exe** ，然後按一下 \[確定\] 。

3.  在事件檢視器中，按一下 \[應用程式及服務記錄檔\] 予以展開，然後選取 Lync Server。

4.  在 \[動作\] 窗格中，按一下 \[篩選目前的記錄\] 。

5.  在 \[事件來源\] 清單中，按一下 \[LS 使用者複寫器\] 。

6.  在 \[\<所有事件識別碼\>\] 中輸入 **30024** ，然後按一下 \[確定\] 。

7.  在篩選後事件清單的 \[一般\] 索引標籤上，尋找有無任何項目指出使用者複寫成功的項目。

