---
title: Lync Server 2013：設定通話許可控制
TOCTitle: 設定通話許可控制
ms:assetid: ce3e6e71-1e33-4cff-849a-c0468e61fef6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398870(v=OCS.15)
ms:contentKeyID: 49292352
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定通話許可控制

 

_**上次修改主題的時間：** 2012-09-21_

通話許可控制 (CAC) 是一種根據可用頻寬，可根據可用的頻寬來決定是否可以建立即時工作階段，防止提供很差的音訊/視訊品質給壅塞網路上的使用者。CAC 只能控制音訊和視訊的即時流量而不會影響資料流量。CAC 可在預設的 WAN 路徑沒有所需的頻寬時，透過網路網路路徑路由傳送通話。如需詳細資訊，請參閱規劃文件中的 [在 Lync Server 2013 中規劃通話許可控制](lync-server-2013-planning-for-call-admission-control.md)。

本節提供一組範例程序，說明如何在您的網路中部署及管理 CAC。

> [!IMPORTANT]  
> 在您部署 CAC 之前，必須收集企業網路拓撲的所有必要資訊，如規劃文件中的 <a href="lync-server-2013-example-of-gathering-your-requirements-for-call-admission-control.md">範例：在 Lync Server 2013 中收集通話許可控制服務需求</a>所述。另外也請確定已安裝並啟動 CAC 元件，如部署文件中的 <a href="lync-server-2013-define-and-configure-a-front-end-pool-or-standard-edition-server.md">在 Lync Server 2013 中定義和設定前端集區或 Standard Edition Server</a>所述。



> [!NOTE]  
> 本節中的所有 CAC 部署和管理範例都是使用 Lync Server 管理命令介面執行。或者，您也可以使用 Lync Server 控制台的 <strong>[網路設定]</strong> 區段來管理 CAC。



## 本章節內容

  - [在 Lync Server 2013 中設定 CAC 的網路區域](lync-server-2013-configure-network-regions-for-cac.md)

  - [在 Lync Server 2013 中建立頻寬原則設定檔](lync-server-2013-create-bandwidth-policy-profiles.md)

  - [在 Lync Server 2013 中設定 CAC 的網站](lync-server-2013-configure-network-sites-for-cac.md)

  - [在 Lync Server 2013 中將子網路與 CAC 上的網站關聯](lync-server-2013-associate-subnets-with-network-sites-for-cac.md)

  - [在 Lync Server 2013 中建立網路區域連結](lync-server-2013-create-network-region-links.md)

  - [在 Lync Server 2013 中建立網路區間路由](lync-server-2013;-create-network-interregion-routes.md)

  - [在 Lync Server 2013 中建立網路站間原則](lync-server-2013-create-network-intersite-policies.md)

  - [在 Lync Server 2013 中啟用通話許可控制](lync-server-2013-enable-call-admission-control.md)

  - [Lync Server 2013 中的通話許可控制部署檢查清單](lync-server-2013-call-admission-control-deployment-checklist.md)

