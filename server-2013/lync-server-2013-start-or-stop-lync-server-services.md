---
title: 啟動或停止 Lync Server 2013 服務
TOCTitle: 啟動或停止 Lync Server 2013 服務
ms:assetid: 1c70b4ec-9de5-4f7a-a3c9-c0eb76710505
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg520958(v=OCS.15)
ms:contentKeyID: 49290262
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 啟動或停止 Lync Server 2013 服務

 

_**上次修改主題的時間：** 2014-02-05_

您可使用 Lync Server 控制台啟動或停止在特定電腦上執行的所有 Lync Server 2013 服務，或是啟動或停止特定的服務。

## 啟動或停止電腦上的所有 Lync Server 服務

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限) 或指派給 CsServerAdministrator 或 CsAdministrator 角色的使用者帳戶，登入部署 Lync Server 2013 之網路上的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[拓撲\]**，再按一下 **\[狀態\]**。

4.  在 **\[狀態\]** 頁面上，視需要排序或搜尋清單，找到正在執行您要啟動或停止之服務的電腦，然後按一下該電腦。

5.  按一下 **\[動作\]**。

6.  按一下 **\[啟動所有服務\]** 或 **\[停止所有服務\]**。

## 啟動或停止特定服務

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[拓撲\]**，再按一下 **\[狀態\]**。

4.  在 **\[狀態\]** 頁面上，視需要排序或搜尋清單，找到正在執行您要啟動或停止之服務的電腦，然後按一下該電腦。

5.  按一下 **\[內容\]**。

6.  視需要排序服務清單，然後按一下您要啟動或停止的服務。

7.  按一下 **\[動作\]**。

8.  按一下 **\[啟動服務\]** 或 **\[停止服務\]**。

9.  按一下 **\[關閉\]**。

## 請參閱

#### 工作

[Lync Server 2013 中不允許服務的工作階段](lync-server-2013-prevent-sessions-for-services.md)  

#### 其他資源

[管理 Lync Server 2013 拓撲](lync-server-2013-managing-the-lync-server-topology.md)

