---
title: 移除前端集區或 Standard Edition Server
TOCTitle: 移除前端集區或 Standard Edition Server
ms:assetid: 83c39a36-49a1-4ac6-9cc5-b0e441b1fdec
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688115(v=OCS.15)
ms:contentKeyID: 49890147
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移除前端集區或 Standard Edition Server

 

_**上次修改主題的時間：** 2012-10-04_

本主題引導您進行移除 前端集區或 Standard Edition 前端伺服器的程序。在集區移除程序中，移除 前端集區時，將移除屬於集區的 前端伺服器。移除 Standard Edition 前端伺服器 時，必須從 拓撲產生器移除 SQL 存放區定義。

## 移除前端伺服器集區

1.  開啟 拓撲產生器。

2.  瀏覽至 Lync Server 2010 節點。

3.  依序展開 \[Enterprise Edition 前端集區\] 和 前端集區，以滑鼠右鍵按一下您想移除的 前端集區，再按一下 \[刪除\] 。

4.  發行拓撲，並檢查複寫狀態，然後視需要執行 Lync Server 部署精靈。

## 移除 Standard Edition 前端伺服器

1.  開啟 拓撲產生器。

2.  瀏覽至 Lync Server 2010 節點。

3.  展開 \[Standard Edition 前端伺服器\] ，以滑鼠右鍵按一下您想移除的 前端伺服器，再按一下 \[刪除\] 。

4.  展開 \[SQL 存放區\] ，以滑鼠右鍵按一下與 Standard Edition 前端伺服器相關聯的 SQL Server 資料庫，再按一下 \[刪除\] 。
    
    > [!IMPORTANT]  
    > 您必須將組合的 SQL Server 資料庫定義從 Standard Edition 前端伺服器中移除。
    


5.  發行拓撲，並檢查複寫狀態，然後視需要執行 Lync Server 部署精靈。

