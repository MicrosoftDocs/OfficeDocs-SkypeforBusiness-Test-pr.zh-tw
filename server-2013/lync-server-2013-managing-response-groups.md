---
title: 在 Lync Server 2013 中管理回應群組
TOCTitle: 在 Lync Server 2013 中管理回應群組
ms:assetid: 5a804d7d-3c1a-4647-a0e0-d5c4c8c23b73
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg520996(v=OCS.15)
ms:contentKeyID: 49291015
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中管理回應群組

 

_**上次修改主題的時間：** 2012-10-01_

回應群組是一種通話管理功能，可讓您保留對特定區域所撥出的通話 (例如客服中心)，然後將這些通話路由傳送至指定的人員群組 (稱為*「代理人」*)。

若要管理回應群組，請設定代理人群組、佇列及工作流程，藉以定義從通話保留至代理人應答這段期間對通話的處理方式。

> [!NOTE]  
> 若您的回應群組部署範圍中，單一集區的工作流程超過 300 個，最好使用 Lync Server 管理命令介面 Cmdlet 建立這些工作流程。如果您使用「回應群組設定工具」，為內含 300 多個工作流程的集區建立更多工作流程，該網頁需要一段時間載入。



本節中的主題會針對您可以在部署中執行來自訂和維護回應群組應用程式的工作提供逐步程序。

## 本章節內容

  - [管理回應群組代理程式群組](lync-server-2013-managing-response-group-agent-groups.md)

  - [管理回應群組佇列](lync-server-2013-managing-response-group-queues.md)

  - [管理回應群組工作流程](lync-server-2013-managing-response-group-workflows.md)

  - [在 Lync Server 2013 中管理應用程式層級回應群組設定](lync-server-2013-managing-application-level-response-group-settings.md)

  - [將回應群組移到新集區](lync-server-2013-moving-response-groups-to-a-new-pool.md)

  - [在災害期間使用 Lync Server 2013 管理回應群組](lync-server-2013-managing-response-groups-during-a-disaster.md)

