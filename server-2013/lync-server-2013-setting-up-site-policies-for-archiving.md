---
title: 設定封存的網站原則
TOCTitle: 設定封存的網站原則
ms:assetid: dc2ea206-8b9c-44dd-a479-efb217593c89
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205325(v=OCS.15)
ms:contentKeyID: 49292528
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定封存的網站原則

 

_**上次修改主題的時間：** 2012-10-09_

您可以為每個特定網站建立和設定封存原則，來啟用或停用那些網站的封存功能。網站原則優先於全域原則，但使用者原則優先於網站原則。只有在您不使用 Microsoft Exchange 整合，或是確實使用 Microsoft Exchange 整合，但有一些使用者未裝載在 Exchange 2013 而就地保留其信箱時，才適用封存原則。

如需封存原則如何運作，包括全域、網站及使用者原則階層的詳細資訊，請參閱規劃文件、部署文件或作業文件中的＜[在 Lync Server 2013 中封存的運作方式](lync-server-2013-how-archiving-works.md)＞。

> [!NOTE]
> 如果您啟用 Microsoft Exchange 整合以供部署使用，Exchange 就地保留原則可控制是否要為 Exchange 2013 上所裝載且就地保留其信箱的使用者，啟用封存原則。如需詳細資訊，請參閱部署文件中的＜<a href="lync-server-2013-setting-up-policies-for-archiving-when-using-exchange-server-integration.md">設定使用 Exchange Server 整合時的封存原則</a>＞。<br />
> 您應該在封存設定中先指定所有適當選項，再於封存原則中啟用內部或外部通訊的封存功能。如需詳細資訊，請參閱部署文件中的＜<a href="lync-server-2013-configuring-archiving-options.md">設定封存選項</a>＞。


## 建立網站的封存原則

1.  使用指派為 CsArchivingAdministrator 或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 2013 控制台。

3.  在左側導覽列中，依序按一下 \[監控和封存\]及 \[封存原則\]。
    
    如需封存原則如何運作，包括全域、網站及使用者原則階層的詳細資訊，請參閱規劃文件、部署文件或＜運作＞文件中的＜[在 Lync Server 2013 中封存的運作方式](lync-server-2013-how-archiving-works.md)＞。

4.  按一下 \[新增\]，然後按一下 \[站台原則\]。

5.  在 \[選取站台\] 中，按一下要套用該原則的網站。

6.  在 \[新增封存原則\] 中，執行下列動作：
    
      - 在 \[名稱\] 中，指定網站原則的名稱。
    
      - 在 \[描述\] 中，提供該網站原則的相關詳細資訊 (例如，Redmond 的網站原則)。
    
      - 若要控制指定網站的內部通訊封存功能，請選取或清除 \[封存內部通訊\] 核取方塊。
    
      - 若要控制指定網站的外部通訊封存功能，請選取或清除 \[封存外部通訊\] 核取方塊。

7.  按一下 \[認可\]。

