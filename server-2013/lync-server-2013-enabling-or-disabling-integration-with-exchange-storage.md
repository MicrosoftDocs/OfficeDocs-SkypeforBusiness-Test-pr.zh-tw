---
title: 啟用或停用 Exchange 儲存整合
TOCTitle: 啟用或停用 Exchange 儲存整合
ms:assetid: c08b9ba5-04f6-452a-b44c-c130f1564a34
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205228(v=OCS.15)
ms:contentKeyID: 49292205
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 啟用或停用 Exchange 儲存整合

 

_**上次修改主題的時間：** 2012-10-09_

在 Lync Server 2013 控制台中，您可以使用封存組態來啟用及停用與 Exchange 儲存區的整合。這包括下列封存組態：

  - 部署 Lync Server 2013 時預設會建立的全域組態。

  - 您可建立並使用的選用網站層級與集區層級組態，以指定在特定網站或集區實作封存的方式。

如需關於封存組態實作方式的詳細資訊，包括您可以指定的選項以及封存組態的階層，請參閱規劃文件、部署文件或作業文件中的[在 Lync Server 2013 中封存的運作方式](lync-server-2013-how-archiving-works.md)。

## 若要啟用或停用與 Microsoft Exchange 儲存區的整合

1.  使用指派給 CsArchivingAdministrator 或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左側導覽列中，依序按一下 \[監控和封存\]及 \[封存組態\]。

4.  在封存組態清單中，按一下適當的全域、網站或集區組態名稱，再依序按一下 \[編輯\]、\[顯示詳細資料\]，然後執行下列動作：
    
      - 若要啟用與 Exchange 2013 儲存區的整合，請選取 \[Microsoft Exchange 整合\] 核取方塊。
    
      - 若要停用與 Exchange 2013 儲存區的整合，請清除 \[Microsoft Exchange 整合\] 核取方塊。

5.  按一下 \[認可\]。

## 請參閱

#### 概念

[在 Lync Server 2013 中封存的運作方式](lync-server-2013-how-archiving-works.md)  

#### 其他資源

[在 Lync Server 2013 中管理組織、網站及集區的封存設定選項](lync-server-2013-managing-archiving-configuration-options-for-your-organization-sites-and-pools.md)

