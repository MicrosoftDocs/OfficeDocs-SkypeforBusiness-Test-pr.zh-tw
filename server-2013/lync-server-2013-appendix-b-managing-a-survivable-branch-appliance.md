---
title: Lync Server 2013：附錄 B：管理 Survivable Branch Appliance
TOCTitle: 附錄 B：管理 Survivable Branch Appliance
ms:assetid: 2ec9d505-6d39-491c-9524-8cf36866b855
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425797(v=OCS.15)
ms:contentKeyID: 49290472
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的附錄 B：管理 Survivable Branch Appliance

 

_**上次修改主題的時間：** 2012-10-18_

本主題說明管理 Survivable Branch Appliance 的程序。尤其會說明如何取代及重新命名 Survivable Branch Appliance，以及如何變更與 Survivable Branch Appliance 相關聯的 Lync Server 2013 前端集區。

## 取代 Survivable Branch Appliance

1.  停止 Survivable Branch Appliance 上的所有 Lync Server 2013 服務。(請參閱 Survivable Branch Appliance 廠商文件。)

2.  (建議執行) 從網域中移除 Survivable Branch Appliance。

3.  依照下列步驟，刪除 Active Directory 網域服務 中的 Survivable Branch Appliance 電腦物件：
    
      - 以 Enterprise Admins 群組成員的身分，登入成員伺服器。
    
      - 依序按一下 **\[開始\]** 、 **\[系統管理工具\]** 和 **\[Active Directory 使用者和電腦\]** 。
    
      - 以滑鼠右鍵按一下 Survivable Branch Appliance 物件，然後按一下 **\[刪除\]** 。

4.  重新新增 Survivable Branch Appliance 電腦物件 (請參閱＜ [在 Lync Server 2013 中將 Survivable Branch Appliance 新增到 Active Directory](lync-server-2013-add-a-survivable-branch-appliance-to-active-directory.md)＞)。

5.  等待 Active Directory 複寫執行。

6.  開啟 Lync Server 管理命令介面，然後輸入 **Enable-CSTopology** 。

7.  將新的 Survivable Branch Appliance 連線至網路，並依照＜[使用 Lync Server 2013 部署 Survivable Branch Appliance 或 Survivable Branch Server - 中央網站工作](lync-server-2013-deploying-a-survivable-branch-appliance-or-server-central-site-tasks.md)＞和＜[使用 Lync Server 2013 部署 Survivable Branch Appliance 或 Server - 分支網站工作](lync-server-2013-deploy-a-survivable-branch-appliance-or-server-branch-site-task.md)＞的步驟執行。

## 重新命名 Survivable Branch Appliance

1.  將使用者移至中央網站。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中將使用者移動到其他集區](lync-server-2013-move-users-to-another-pool.md)＞。

2.  停止 Survivable Branch Appliance 上的所有 Lync Server 2013 服務。(請參閱 Survivable Branch Appliance 廠商文件。)

3.  依照下列步驟，從拓撲中移除 Survivable Branch Appliance：
    
      - 依序按一下 \[開始\] 、\[程式集\] 、\[Microsoft Lync Server\] 及 \[Lync Server 拓撲建置器\] 。
    
      - 在主控台樹狀目錄中展開 \[分支網站\] ，按一下 Survivable Branch Appliance，然後在 \[動作\] 窗格上按一下 \[刪除\] 。

4.  從網域中移除 Survivable Branch Appliance。

5.  依照下列步驟，刪除 Active Directory 中的 Survivable Branch Appliance 電腦物件：
    
      - 以 Enterprise Admins 群組成員的身分，登入網域控制站。
    
      - 依序按一下 **\[開始\]** 、 **\[系統管理工具\]** 和 **\[Active Directory 使用者和電腦\]** 。
    
      - 以滑鼠右鍵按一下 Survivable Branch Appliance 物件，然後按一下 **\[刪除\]** 。

6.  將 Survivable Branch Appliance 還原為原廠預設值 (請參閱 Survivable Branch Appliance 廠商的文件)。

7.  依照＜[使用 Lync Server 2013 部署 Survivable Branch Appliance 或 Survivable Branch Server - 中央網站工作](lync-server-2013-deploying-a-survivable-branch-appliance-or-server-central-site-tasks.md)＞和＜[使用 Lync Server 2013 部署 Survivable Branch Appliance 或 Server - 分支網站工作](lync-server-2013-deploy-a-survivable-branch-appliance-or-server-branch-site-task.md)＞的步驟執行。

8.  將使用者移至重新命名的 Survivable Branch Appliance。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中將使用者移動到其他集區](lync-server-2013-move-users-to-another-pool.md)＞。

## 變更與 Survivable Branch Appliance 相關聯的 Lync Server 前端集區

1.  將使用者從 Survivable Branch Appliance 移至中央網站上的 Lync Server 前端集區。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中將使用者移動到其他集區](lync-server-2013-move-users-to-another-pool.md)＞。

2.  停止 Survivable Branch Appliance 上的所有 Lync Server 服務。(請參閱 Survivable Branch Appliance 廠商文件。)

3.  依照下列步驟，更新與 Survivable Branch Appliance 相關聯的 Lync Server 前端集區：
    
      - 依序按一下 \[開始\] 、\[程式集\] 、\[Microsoft Lync Server\] 及 \[Lync Server 拓撲建置器\] 。
    
      - 展開 \[分支網站\] 。
    
      - 在 Survivable Branch Appliance 物件上按一下滑鼠右鍵以進行修改，然後按一下 \[編輯內容\]
    
      - 在 \[恢復\] 中選取要與 Survivable Branch Appliance 關聯的新 前端集區，然後按 \[下一步\] 。
    
      - 在主控台樹狀目錄中，以滑鼠右鍵按一下新的 Survivable Branch Appliance，然後依序按一下 **\[拓撲\]** 和 **\[發行\]** 。

4.  重新啟動 Survivable Branch Appliance 上的所有 Lync Server 服務。

5.  測試 Survivable Branch Appliance。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中將使用者隸屬於 Survivable Branch Appliance 或 Survivable Branch Server](lync-server-2013-home-users-on-a-survivable-branch-appliance-or-server.md)＞。

6.  將使用者從中央網站上的 Lync Server 前端集區移至 Survivable Branch Appliance。

