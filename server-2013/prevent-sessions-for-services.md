---
title: 防止服務的工作階段
TOCTitle: 防止服務的工作階段
ms:assetid: 4b541c72-cdc1-4f86-a5a8-c43c24f41d8b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688049(v=OCS.15)
ms:contentKeyID: 49890052
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 防止服務的工作階段

 

_**上次修改主題的時間：** 2012-10-04_

您可以使用 Microsoft Lync Server 2010 控制台來阻止所有 Lync Server 2010 服務的新工作階段於特定電腦上執行，或阻止特定 Lync Server 2010 服務的新工作階段。

## 若要阻止所有 Lync Server 服務的新工作階段於電腦上執行

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限) 或指派給 CsServerAdministrator 或 CsAdministrator 角色的使用者帳戶，登入部署 Lync Server 2013 之網路上的任何電腦。

2.  開啟 Lync Server 控制台。

3.  在左導覽列中，按一下 \[拓撲\] ，然後按一下 \[狀態\] 。

4.  在 **\[狀態\]** 頁面中視需要排序或搜尋整個清單，以尋找目前正在執行您要阻止新工作階段之服務的電腦，然後按一下該電腦。

5.  按一下 **\[動作\]** 。

6.  按一下 **\[阻止對所有服務的新工作階段\]** 。

## 若要阻止特定服務的新工作階段

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限) 或指派給 CsServerAdministrator 或 CsAdministrator 角色的使用者帳戶，登入部署 Lync Server 2013 之網路上的任何電腦。

2.  開啟 Lync Server 控制台。

3.  在左導覽列中，按一下 \[拓撲\] ，然後按一下 \[狀態\] 。

4.  在 **\[狀態\]** 頁面上，視需要排序或搜尋清單，找到正在執行您要啟動或停止之服務的電腦，然後按一下該電腦。

5.  按一下 \[內容\] 。

6.  視需要排序服務清單，然後按一下要阻止新工作階段的服務。

7.  按一下 **\[動作\]** 。

8.  按一下 **\[阻止對服務的新工作階段\]** 。

9.  按一下 \[關閉\] 。

