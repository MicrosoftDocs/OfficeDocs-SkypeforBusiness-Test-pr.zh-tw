---
title: 啟用或停用封存 IM 或會議工作階段
TOCTitle: 啟用或停用封存 IM 或會議工作階段
ms:assetid: aa4b5983-dbe1-4d64-8a18-fe2c33994e94
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182567(v=OCS.15)
ms:contentKeyID: 49291946
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 啟用或停用封存 IM 或會議工作階段

 

_**上次修改主題的時間：** 2012-10-10_

在 Lync Server 2013 控制台中，您可使用封存組態來啟用和停用 IM、會議工作階段或兩者的封存功能。這包括下列封存組態：

  - 部署 Lync Server 2013 時預設會建立的全域組態。

  - 您可建立並使用的選用網站層級與集區層級組態，以指定在特定網站或集區實作封存的方式。

您一開始在部署封存時設定封存組態，但可以在部署之後變更、新增和刪除組態。如需關於封存組態實作方式的詳細資訊，包括您可以指定的選項以及封存組態的階層，請參閱規劃文件、部署文件或作業文件中的[在 Lync Server 2013 中封存的運作方式](lync-server-2013-how-archiving-works.md)。

> [!NOTE]
> 若要使用封存，您必須設定封存原則，以指定是否針對位於 Lync Server 2013 的使用者啟用內部通訊、外部通訊或兩者的封存。預設不會啟用內部或外部通訊的封存。在任何原則中啟用封存前，應先如本節所述，為您的部署和 (選用的) 特定網站與集區指定適當的封存組態。如需關於啟用封存的詳細資訊，請參閱部署文件中的<a href="lync-server-2013-configuring-and-assigning-archiving-policies.md">設定和指派封存原則</a>。<br />
> 如果您在部署封存之後，決定要使用 Microsoft Exchange 整合在 Exchange 2013 伺服器上儲存封存資料和檔案，而且所有使用者都位於 Exchange 2013 伺服器上，您應從拓撲中移除 SQL Server 資料庫組態。如需詳細資訊，請參閱作業文件中的＜<a href="lync-server-2013-changing-archiving-database-options.md">在 Lync Server 2013 中變更封存資料庫選項</a>＞。


## 啟用或停用 IM 或會議工作階段的封存

1.  使用指派給 CsArchivingAdministrator 或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左側導覽列中，依序按一下 \[監控和封存\]及 \[封存組態\]。

4.  從封存組態清單中選取適當的全域、網站或集區組態，並依序按一下 \[編輯\] 和 \[顯示詳細資料\]，然後執行下列動作：
    
      - 若只要啟用立即訊息 (IM) 工作階段的封存，請按一下 \[封存 IM 工作階段\]。
    
      - 若要同時啟用 IM 工作階段和會議的封存，請按一下 \[封存 IM 和會議工作階段\]。
    
      - 若要停用原則的封存，請按一下 \[停用封存\]。

5.  按一下 \[認可\]。

## 請參閱

#### 其他資源

[在 Lync Server 2013 中管理組織、網站及集區的封存設定選項](lync-server-2013-managing-archiving-configuration-options-for-your-organization-sites-and-pools.md)  
[設定和指派封存原則](lync-server-2013-configuring-and-assigning-archiving-policies.md)

