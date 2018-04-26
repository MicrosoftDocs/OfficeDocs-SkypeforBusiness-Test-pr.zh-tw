---
title: Lync Server 2013：準備鎖定的 Active Directory 網域服務
TOCTitle: 準備鎖定的 Active Directory 網域服務
ms:assetid: 68bde963-3fa3-4102-88d6-ac931c1dd2d7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398492(v=OCS.15)
ms:contentKeyID: 49291191
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中準備鎖定的 Active Directory 網域服務

 

_**上次修改主題的時間：** 2012-05-14_

組織通常會鎖定 Active Directory 網域服務，協助減少安全性風險。不過，鎖定的 Active Directory 環境可能會限制 Lync Server 2013 所需要的權限。針對 Lync Server 2013 正確準備鎖定的 Active Directory 環境時，需要考量額外事項和進行額外步驟。

鎖定的 Active Directory 環境是以下列兩種常見方式來限制權限：

  - 已驗證的使用者存取控制項目 (ACE) 已從容器中移除。

  - User、Contact、InetOrgPerson 或 Computer 物件的容器已停用權限繼承。

## 本節內容

  - [Lync Server 2013 中已移除已驗證使用者權限](lync-server-2013-authenticated-user-permissions-are-removed.md)

  - [Lync Server 2013 中的 Computers、Users 或 InetOrgPerson 容器已停用權限繼承](lync-server-2013-permissions-inheritance-is-disabled-on-computers-users-or-inetorgperson-containers.md)

