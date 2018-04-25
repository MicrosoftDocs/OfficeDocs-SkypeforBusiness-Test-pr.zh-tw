---
title: Lync Server 2013：啟用 Kerberos 驗證的先決條件
TOCTitle: 啟用 Kerberos 驗證的先決條件
ms:assetid: 3f276a21-7476-4bc0-9fd1-59e844d2e9c1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425909(v=OCS.15)
ms:contentKeyID: 49290697
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中啟用 Kerberos 驗證的先決條件

 

_**上次修改主題的時間：** 2013-02-21_

啟用 Kerberos 驗證之前，請確定所有先決條件組態和基礎結構準備作業都已完成：

  - 已擴充 Lync Server 2013 的 Active Directory 架構。

  - 已完成 Lync Server 2013 的 Active Directory 樹系準備。

  - 已完成 Lync Server 2013 的 Active Directory 網域準備。

  - 中央管理存放區已成功安裝，且可供使用。

  - 已使用 拓撲產生器建立並發行拓撲。

  - 已定義和部署需要 Web 服務的伺服器和角色，包括前端伺服器、Standard Edition Server 和 Director。

  - 已使用建議的角色服務來設定和部署 Internet Information Services (IIS)，以支援 Lync Server 2013 中的 Web 服務。

先決條件都符合後，您就可以為您的部署建立一個或多個帳戶，供 Web 服務用於 Kerberos 驗證。每個部署應至少建立一個 Kerberos 驗證帳戶。不過，您可以為每個網站各建立一個帳戶，以在該網站提供本機 Kerberos 驗證。每個網站只能指定一個 Kerberos 驗證帳戶。

