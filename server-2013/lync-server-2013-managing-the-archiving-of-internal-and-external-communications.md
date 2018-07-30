---
title: 在 Lync Server 2013 中管理內部與外部通訊的封存
TOCTitle: 在 Lync Server 2013 中管理內部與外部通訊的封存
ms:assetid: 6c2cf941-3204-4f1a-a7e0-416c828056d9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204977(v=OCS.15)
ms:contentKeyID: 49291228
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中管理內部與外部通訊的封存

 

_**上次修改主題的時間：** 2012-10-09_

在 Lync Server 2013 中，如果您不使用 Microsoft Exchange 整合，或如果您的使用者不是位於 Exchange 2013 且將其信箱設為 \[就地保留\]，則您會使用封存原則來啟用和停用內部通訊和外部通訊的封存。其中包括下列封存原則：

  - 當您部署 Lync Server 2013 時會建立全域原則。

  - 您可建立並使用選擇的網站層級和使用者層級原則，以針對特定網站或使用者指定封存的實作方式。

當您部署封存時，會初步設定封存原則，但是您可在部署後變更、新增和刪除原則。在 Lync Server 2013 控制台 中，您可以使用 **\[封存和監控\]** 群組的 **\[封存原則\]** 頁面管理全域層級、網站層級和使用者層級的原則。如果您將 Lync Server 儲存與 Exchange 2013 儲存整合在一起，Exchange 使用者原則的優先順序會高於 Lync Server 2013 封存原則。

如需原則實作方式，包括原則階層的詳細資訊，請參閱規劃文件、部署文件或作業文件中的[在 Lync Server 2013 中封存的運作方式](lync-server-2013-how-archiving-works.md)。

> [!NOTE]
> 若要控制封存的實作，您必須在封存組態設定中指定選項，例如是否要封存 IM 或會議、關鍵模式的使用和清除選項。根據預設，全域封存組態或是任何網站或即區封存組態中，不會啟用任何選項。您應當在啟用封存原則中的內部或外部通訊前，先在封存組態中指定所有合適的選項。如需詳細資訊，請參閱作業文件中的<a href="lync-server-2013-managing-archiving-configuration-options-for-your-organization-sites-and-pools.md">在 Lync Server 2013 中管理組織、網站及集區的封存設定選項</a>。<br />
> 如果您針對部署作業啟用 Microsoft Exchange 整合，Exchange 原則會控制是否要啟用位於 Exchange 2013 之使用者的封存，並將其信箱設為 [就地保留]。如需詳細資訊，請參閱部署文件中的<a href="lync-server-2013-setting-up-policies-for-archiving-when-using-exchange-server-integration.md">設定使用 Exchange Server 整合時的封存原則</a>。


## 本章節內容

  - [建立封存原則以針對特定網站或使用者啟用或停用封存內部或外部通訊](lync-server-2013-creating-an-archiving-policy-to-enable-or-disable-archiving-of-internal-or-external-communications-for-specific-sites-or-users.md)

  - [變更封存原則以啟用或停用封存組織、網站或使用者的內部或外部通訊](lync-server-2013-changing-an-archiving-policy-to-enable-or-disable-archiving-of-internal-or-external-communications-for-your-organization-sites-or-us.md)

  - [將封存原則套用到使用者](lync-server-2013-applying-an-archiving-policy-to-users.md)

  - [設定使用 Exchange Server 整合時的封存原則](lync-server-2013-setting-up-policies-for-archiving-when-using-exchange-server-integration.md)

  - [刪除封存原則](lync-server-2013-deleting-an-archiving-policy.md)

