---
title: Lync Server 2013：Enterprise Voice 的軟體先決條件
TOCTitle: Enterprise Voice 的軟體先決條件
ms:assetid: 41172119-9631-46c7-9d9f-386d951c650b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425916(v=OCS.15)
ms:contentKeyID: 49290712
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中 Enterprise Voice 的軟體先決條件

 

_**上次修改主題的時間：** 2012-10-03_

確認您想要部署 Enterprise Voice 的基礎結構符合下列軟體先決條件：

  - 網路上已安裝 Lync Server 2013 Standard Edition 或 Enterprise Edition，而且運作正常。

  - 所有的 Edge Server (包括執行 Access Edge Service、 A/V Edge 服務、 Web Conferencing Edge Service 的 Edge Server 和反向 Proxy) 都已部署在周邊網路中，而且運作正常。

  - 需要 Microsoft Exchange Server 2007 Service Pack 3 (SP3)、Microsoft Exchange Server 2010 或 Microsoft Exchange Server 2013，才能將 Exchange Unified Messaging 和 Lync Server 整合，為 Lync 端點提供豐富的通知及通話記錄資訊。

  - 已為 Lync Server 建立並啟用一個或多個使用者。

  - 已成功部署 Lync 用戶端和裝置。

  - 拓撲產生器已安裝在您網路的某個伺服器上。

## 後續步驟：確認安全性和設定先決條件

確認 Enterprise Voice 的軟體先決條件後，您可以參考文件說明，繼續準備部署 Enterprise Voice：

1.  依照＜ [Lync Server 2013 中 Enterprise Voice 的安全性和組態先決條件](lync-server-2013-security-and-configuration-prerequisites-for-enterprise-voice.md)＞所述，確認安全性、使用者設定和硬體先決條件。

2.  依照＜[在 Lync Server 2013 中安裝中繼伺服器的檔案](lync-server-2013-install-the-files-for-mediation-server.md)＞的說明安裝中繼伺服器，但*僅*限於您在組合時的前端集區或 Standard Edition 伺服器 部署程序中安裝中繼伺服器，以致於想要部署獨立中繼伺服器或集區時。

3.  依照＜[在 Lync Server 2013 中設定主幹](lync-server-2013-configuring-trunks.md)＞的說明設定主幹連線，為使用者提供 PSTN 連線。

