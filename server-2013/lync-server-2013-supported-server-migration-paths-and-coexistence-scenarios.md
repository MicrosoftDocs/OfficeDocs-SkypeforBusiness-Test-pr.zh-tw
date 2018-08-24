---
title: Lync Server 2013：支援的伺服器轉移路徑和並存案例
TOCTitle: 支援的伺服器轉移路徑和並存案例
ms:assetid: 2a6a730f-7f80-45f9-9540-3edfdaa265fb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425764(v=OCS.15)
ms:contentKeyID: 49290402
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中支援的伺服器轉移路徑和並存案例

 

_**上次修改主題的時間：** 2012-10-16_

Lync Server 2013 支援從下列任一版本進行移轉：

  - Microsoft Lync Server 2010

  - Microsoft Office Communications Server 2007 R2

同時執行這兩個舊版的環境無法進行移轉。此外也不支援從 Microsoft Office Communications Server 2007 或 Live Communications Server 2005 等舊版本進行移轉。若您先前的部署中包含 群組聊天，就必須單獨進行移轉。

## 移轉方法

所有 Lync Server 拓撲與伺服器角色的移轉均受支援。您可以從某一種拓撲移轉至不同的拓撲，包括從 Standard Edition Server 移轉至 Enterprise Edition Server 在內。

Lync Server 2013 僅支援下列移轉方法：

   **並存移轉。**在並存移轉中， Lync Server 2013 會以現有的 Microsoft Lync Server 2010 或 Office Communications Server 2007 R2 部署為基礎進行部署，然後再將作業轉換到新伺服器，並將使用者移至 Lync Server 2013。此方法在移轉期間需要額外的伺服器平台 (包括軟硬體)，且新設定中的系統名稱和集區名稱會不相同。若有需要復原為先前的版本，您可以將作業切換回先前的伺服器。

Active Directory 網域服務 樹系間的移轉不受支援。

建議您採用分段執行的移轉路徑。如需從舊版進行移轉的詳細資訊 (包括將元件部署適當分段的方式)，請參閱下列移轉文件中的主題：

  - [從 Lync Server 2010 移轉到 Lync Server 2013](migration-from-lync-server-2010-to-lync-server-2013.md)

  - [從 Office Communications Server 2007 R2 移轉至 Lync Server 2013](migration-from-office-communications-server-2007-r2-to-lync-server-2013.md)

  - [從 Lync Server 2010 群組聊天或 Office Communications Server 2007 R2 群組聊天移轉至 Lync Server 2013 常設聊天室伺服器](migration-from-lync-server-2010-group-chat-or-office-communications-server-2007-r2-group-chat-to-lync-server-2013-persistent-chat-server.md)

## 並存案例

Lync Server 2013 可與 Lync Server 2010 部署或 Office Communications Server 2007 R2 部署的元件並存。 Lync Server 2013 無法與 Lync Server 2010 和 Office Communications Server 2007 R2 同時部署 (無法三種版本全部同時部署)。

在先前的 Lync Server 2013 或 Office Communications Server 2007 R2 部署會暫時與新 Lync Server 2010 部署並存的分段移轉期間，混合版本路由的支援性將有所限制。如需詳細資訊，請參閱移轉文件。

您必須分別使用不同的電腦為您的 Lync Server 2013 資料庫執行個體執行 Microsoft SQL Server 2008 R2 或 Microsoft SQL Server 2012。您無法為您針對 Lync Server 2010 或 Office Communications Server 2007 R2 前端集區所使用的 Lync Server 2013 前端集區，使用相同的 SQL Server 執行個體。若您在 拓撲產生器中，針對已部署 Lync Server 2010 或 Office Communications Server 2007 R2 的部署，定義及設定 Lync Server 2013，則 拓撲產生器將不會允許您定義拓撲中已使用的 Lync Server 2013 執行個體。

拓撲產生器將顯示下列訊息以通知您此問題：「SQL Server \[伺服器的 FQDN\] 已經包含裝載角色「使用者存放區」的 SQL 執行個體。」

> [!NOTE]  
> 若您想部署對 Lync Server 2013 而言為全新的伺服器角色，則應先依照＜移轉＞與部署文件中的說明將您現有的部署升級，然後再依照規劃與部署文件中的說明部署新的伺服器角色。若您要移轉舊版的群組聊天，請先完成將所有其他元件從 Lync Server 2010 移轉至 Office Communications Server 2007 R2 的程序，才能在最後移轉舊版的群組聊天。



如需特定共存需求，以及 Lync Server 2010 或 Office Communications Server 2007 R2 與 Lync Server 2013 元件之共存及移轉的其他詳細資訊，請參閱移轉文件中的＜ [從 Lync Server 2010 移轉到 Lync Server 2013](migration-from-lync-server-2010-to-lync-server-2013.md)＞及＜ [從 Office Communications Server 2007 R2 移轉至 Lync Server 2013](migration-from-office-communications-server-2007-r2-to-lync-server-2013.md)＞。如需用戶端的混合版本支援的詳細資訊，請參閱＜ [Lync Server 2013 中舊部署支援的用戶端](lync-server-2013-supported-clients-from-previous-deployments.md)＞。

