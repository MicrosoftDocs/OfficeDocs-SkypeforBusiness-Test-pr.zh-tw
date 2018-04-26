---
title: Lync Server 2013：封存概觀
TOCTitle: 封存概觀
ms:assetid: 1e3c2ef1-f561-4f57-8b6a-7d78addc1ed1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204729(v=OCS.15)
ms:contentKeyID: 49290281
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的封存概觀

 

_**上次修改主題的時間：** 2013-09-30_

Lync Server 2013 中的封存功能可讓您封存透過 Lync Server 2013 傳送的通訊。

您可在初始的 Lync Server 2013 部署中同時實作封存，或可將其新增至現有的部署。若要使用 Lync Server 2013 封存資料庫 ( SQL Server 資料庫) 來儲存封存資料，您可以使用 拓撲產生器，將資料庫新增至拓撲中，然後再次發行拓撲。若您的所有使用者都位於 Exchange 2013 且其信箱都是就地保留狀態，您就不需更新拓撲，只需啟用 Microsoft Exchange 整合，即可在 Exchange 2013 中儲存已封存資料。

實作封存時，您要設定好欲進行封存的項目 (預設是不會封存任何項目)。您可使用 Lync Server 2013 控制台 來設定和管理封存。您可針對內部通訊及/或外部通訊實作封存，也可設定封存整個組織的設定，或是特定網站、特定集區和特定使用者和使用者群組的設定。如需判斷組織之適當選項的詳細資訊，請參閱規劃文件中的＜[在 Lync Server 2013 中定義封存需求](lync-server-2013-defining-your-requirements-for-archiving.md)＞。如需如何實作封存原則和設定的詳細資訊，以及可以及不可封存之資訊的詳細資訊，請參閱規劃文件、部署文件或作業文件中的＜[在 Lync Server 2013 中封存的運作方式](lync-server-2013-how-archiving-works.md)＞。

