---
title: 停用網路媒體旁路
TOCTitle: 停用網路媒體旁路
ms:assetid: 936d2678-d712-4589-b172-b5793013652f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688141(v=OCS.15)
ms:contentKeyID: 49890211
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 停用網路媒體旁路

 

_**上次修改主題的時間：** 2012-10-15_

媒體旁路設定會在 Microsoft Lync Server 2013 部署中全域套用。媒體旁路允許通話略過中繼伺服器。如需關於媒體旁路使用時機的詳細資訊，請參閱＜規劃＞一節中的[在 Lync Server 2013 中規劃媒體旁路](lync-server-2013-planning-for-media-bypass.md)。您可以從 Lync Server 控制台停用媒體旁路。如需關於啟用和設定媒體旁路的詳細資訊，請參閱＜[啟用網路媒體旁路](lync-server-2013-enabling-network-media-bypass.md)＞。

## 停用媒體旁路

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[網路設定\]，然後按一下 \[通用\]。

4.  在 \[通用\] 頁面上，按一下 \[通用\] 設定。其中一律只有一項設定，且一律稱為「通用」。

5.  在 \[編輯\] 功能表中，按一下 \[檢視詳細資料\]。

6.  在 \[編輯通用設定\] 頁面上，清除 \[啟用媒體旁路\] 核取方塊。

7.  按一下 \[認可\] 以儲存變更。

## 請參閱

#### 工作

[啟用網路媒體旁路](lync-server-2013-enabling-network-media-bypass.md)

