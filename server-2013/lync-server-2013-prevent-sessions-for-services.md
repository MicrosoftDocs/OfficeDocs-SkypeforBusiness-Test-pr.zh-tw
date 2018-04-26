---
title: Lync Server 2013 中不允許服務的工作階段
TOCTitle: Lync Server 2013 中不允許服務的工作階段
ms:assetid: 977dcc5c-2aac-48ef-86a1-a8d47b4d9e74
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182553(v=OCS.15)
ms:contentKeyID: 49291761
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中不允許服務的工作階段

 

_**上次修改主題的時間：** 2012-11-01_

您可以使用 Lync Server 控制台來阻止所有 Lync Server 2013 服務的新工作階段於特定電腦上執行，或阻止特定 Lync Server 2013 服務的新工作階段。

## 若要阻止所有 Lync Server 服務的新工作階段於電腦上執行

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限) 或指派給 CsServerAdministrator 或 CsAdministrator 角色的使用者帳戶，登入部署 Lync Server 2013 之網路上的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[拓撲\]，然後按一下 \[狀態\]。

4.  在 **\[狀態\]** 頁面中視需要排序或搜尋整個清單，以尋找目前正在執行您要阻止新工作階段之服務的電腦，然後按一下該電腦。

5.  按一下 \[動作\]。

6.  按一下 **\[阻止對所有服務的新工作階段\]**。

## 若要阻止特定服務的新工作階段

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限) 或指派給 CsServerAdministrator 或 CsAdministrator 角色的使用者帳戶，登入部署 Lync Server 2013 之網路上的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[拓撲\]，然後按一下 \[狀態\]。

4.  在 **\[狀態\]** 頁面上，視需要排序或搜尋清單，找到正在執行您要啟動或停止之服務的電腦，然後按一下該電腦。

5.  按一下 \[內容\]。

6.  視需要排序服務清單，然後按一下要阻止新工作階段的服務。

7.  按一下 \[動作\]。

8.  按一下 **\[阻止對服務的新工作階段\]**。

9.  按一下 \[關閉\]。

## 請參閱

#### 其他資源

[管理 Lync Server 2013 拓撲](lync-server-2013-managing-the-lync-server-topology.md)

