---
title: 在 Lync Server 中建立和設定封存的使用者原則
TOCTitle: 在 Lync Server 中建立和設定封存的使用者原則
ms:assetid: 5af0e605-3563-4d6f-a3c6-511d204a3165
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204923(v=OCS.15)
ms:contentKeyID: 49291027
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 中建立和設定封存的使用者原則

 

_**上次修改主題的時間：** 2012-10-09_

若要為位於 Lync Server 的特定使用者啟用或停用封存，您必須先建立使用者原則，然後將原則套用至一或多個使用者或使用者群組。如需有關將使用者原則套用至特定使用者和使用者群組的詳細資訊，請參閱部署文件中的[將 Lync Server 封存原則套用至使用者](lync-server-2013-applying-a-lync-server-archiving-policy-to-a-user.md)。

如需有關封存原則如何運作 (包含全域、網站及使用者原則的階層) 的詳細資訊，請參閱規劃文件、部署文件或作業文件中的[在 Lync Server 2013 中封存的運作方式](lync-server-2013-how-archiving-works.md)。

> [!NOTE]
> 如果您已針對部署啟用 Microsoft Exchange 整合，Exchange 就地保留原則便會控制是否要針對位於 Exchange 2013 且其信箱狀態為 [就地保留] 的使用者啟用封存。如需詳細資訊，請參閱部署文件中的<a href="lync-server-2013-setting-up-policies-for-archiving-when-using-exchange-server-integration.md">設定使用 Exchange Server 整合時的封存原則</a>。<br />
> 啟用封存之前，您應該先在封存組態中指定所有適當的選項。如需詳細資訊，請參閱部署文件中的<a href="lync-server-2013-configuring-archiving-options.md">設定封存選項</a>。


## 為位於 Lync Server 上的使用者設定封存原則

1.  使用指派到 CsArchivingAdministrator 或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 2013 控制台。如需各種 Lync Server 2013 控制台啟動方法的詳細資訊，請參閱＜[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)＞。

3.  在左側導覽列中，依序按一下 \[監控和封存\]及 \[封存原則\]。

4.  依序按一下 \[新增\] 和 \[使用者原則\]。

5.  在 \[新增封存原則\] 中，執行下列動作：
    
      - 在 \[名稱\] 中，指定使用者原則的名稱。
    
      - 在 \[描述\] 中，提供何謂使用者原則的相關資訊 (例如，適用於法務部門的使用者原則)。
    
      - 若要控制使用者原則的內部通訊封存，請選取或清除 \[封存內部通訊\] 核取方塊。
    
      - 若要控制使用者原則的外部通訊封存，請選取或清除 \[封存外部通訊\] 核取方塊。

6.  按一下 \[認可\]。

使用者原則僅會套用至您指派該原則的使用者。如需有關將使用者原則套用至特定使用者的詳細資訊，請參閱部署文件中的[將 Lync Server 封存原則套用至使用者](lync-server-2013-applying-a-lync-server-archiving-policy-to-a-user.md)。

