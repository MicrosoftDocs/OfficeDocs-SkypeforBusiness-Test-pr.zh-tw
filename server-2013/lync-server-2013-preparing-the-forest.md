---
title: Lync Server 2013：準備樹系
TOCTitle: 準備樹系
ms:assetid: 3d188fcb-c64e-46cf-a3a7-9e3ebefed7fd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425898(v=OCS.15)
ms:contentKeyID: 49290669
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 為 Lync Server 2013 準備樹系

 

_**上次修改主題的時間：** 2013-02-21_

樹系準備會建立 Active Directory 全域設定和物件以及 Active Directory 萬用群組，以供 Lync Server 2013 使用，並在 Active Directory 物件上授與適當的存取權限。如需萬用群組以及樹系準備所建立之全域設定和物件的說明，請參閱＜ [Lync Server 2013 中的樹系準備所進行的變更](lync-server-2013-changes-made-by-forest-preparation.md)＞。

樹系準備也會建立物件，這些物件將包含 Lync Server 2013 所使用的屬性集與顯示規範，並會將其儲存在組態容器中。

> [!IMPORTANT]  
> 在執行樹系準備程序前，請確定架構準備變更已複寫至所有網域控制站。如果複寫未完成，則會發生錯誤。



如果您執行的是全新 Lync Server 部署，則必須將全域設定儲存在組態容器中。如果您是從舊版進行升級，且仍將全域設定儲存在系統容器中，則可以繼續使用系統容器。

您必須是樹系根網域 Enterprise Admins 或 Domain Admins 群組的成員，才能執行這項程序。

## 本章節內容

  - [針對 Lync Server 2013 執行樹系準備](lync-server-2013-running-forest-preparation.md)

  - [使用 Cmdlet 進行 Lync Server 2013 的反向樹系準備](lync-server-2013-using-cmdlets-to-reverse-forest-preparation.md)

