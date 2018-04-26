---
title: 網域名稱系統 (DNS) 需求
TOCTitle: 網域名稱系統 (DNS) 需求
ms:assetid: 586cf18e-0080-4eb1-aee5-56843277fdfc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398386(v=OCS.15)
ms:contentKeyID: 49290991
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 網域名稱系統 (DNS) 需求

 

_**上次修改主題的時間：** 2012-06-18_

若要部署 Lync Server，您必須建立網域名稱系統 (DNS) 記錄，以啟用用戶端和伺服器探索，與 (選用) 自動用戶端登入支援 (如果您的組織想要支援的話)。

Lync Server 以下列方式使用 DNS：

  - 探索內部伺服器或集區以進行伺服器對伺服器的通訊。

  - 允許用戶端探索用於各種 SIP 交易的前端集區或 Standard Edition 伺服器。

  - 允許未登入的整合通訊 (UC) 裝置，探索執行裝置更新 Web 服務的 前端集區 或 Standard Edition 伺服器、取得更新以及傳送記錄檔。

  - 允許外部伺服器與用戶端連線至 Edge Server 或 HTTP 反向 Proxy，以進行立即訊息 (IM) 或會議。

  - 允許外部 UC 裝置透過 Edge Server 或 HTTP 反向 Proxy 連線至裝置更新 Web 服務，並取得更新。

  - 讓行動用戶端能夠自動探索 Web 服務資源，而不需使用者手動在裝置設定中輸入 URL。

## 本章節內容

  - [針對 Lync Server 2013 判定 DNS 需求](lync-server-2013-determine-dns-requirements.md)

  - [前端集區的 DNS 需求](lync-server-2013-dns-requirements-for-front-end-pools.md)

  - [Standard Edition Server 的 DNS 需求](lync-server-2013-dns-requirements-for-standard-edition-servers.md)

  - [Lync Server 2013 中簡單 URL 的 DNS 需求](lync-server-2013-dns-requirements-for-simple-urls.md)

  - [Lync Server 2013 中的自動用戶端登入的 DNS 需求](lync-server-2013-dns-requirements-for-automatic-client-sign-in.md)

  - [行動的 DNS 需求](lync-server-2013-dns-requirements-for-mobility.md)

  - [Lync Server 2013 中的 DNS 負載平衡](lync-server-2013-dns-load-balancing.md)

