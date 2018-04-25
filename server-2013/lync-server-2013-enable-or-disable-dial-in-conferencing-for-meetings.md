---
title: 針對會議啟用或停用電話撥入式會議
TOCTitle: 針對會議啟用或停用電話撥入式會議
ms:assetid: 418dcf2d-c8d6-4b2c-b1ab-8723c7ef53e0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688036(v=OCS.15)
ms:contentKeyID: 49890036
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 針對會議啟用或停用電話撥入式會議

 

_**上次修改主題的時間：** 2012-11-01_

下列程序描述如何使用撥入功能允許使用者加入會議。

## 啟用/停用電話撥入式會議

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[會議\]**，再按一下 **\[會議原則\]**。

4.  在會議原則清單中，選取要啟用電話撥入式會議的原則，然後按一下 **\[編輯\]**，再按一下 **\[顯示詳細資料\]**。

5.  若要允許使用者藉由撥入電話來加入會議，請勾選 **\[啟用 PSTN 電話撥入式會議\]** 核取方塊。根據預設，使用者可以使用公用交換電話網路 (PSTN) 來撥入會議。

6.  按一下 **\[認可\]**。

