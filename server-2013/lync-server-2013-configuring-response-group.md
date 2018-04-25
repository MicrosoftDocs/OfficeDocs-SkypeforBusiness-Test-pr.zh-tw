---
title: Lync Server 2013：設定回應群組
TOCTitle: 設定回應群組
ms:assetid: c56db929-cb21-4af0-be3f-c8f807b78a5a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205249(v=OCS.15)
ms:contentKeyID: 49292247
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定回應群組

 

_**上次修改主題的時間：** 2012-10-30_

回應群組是 企業語音的功能，可將來電路由傳送並排入佇列給一組人 (稱為「代理」 ，例如服務台人員或客戶服務人員)。

當您部署 企業語音時，前端伺服器或 Standard Edition Server 上會自動安裝並啟用 回應群組所需的元件。若要讓使用者能夠使用 回應群組，您必須依序設定代理群組、佇列以及工作流程。此外， 回應群組系統管理員可以將設定現有工作流程的工作委派給 回應群組管理員，後者可接著修改和重新設定工作流程及其相關的代理群組和佇列。

本節會引導您完成設定 Lync Server 2013回應群組的工作。文中假設您已閱讀 回應群組的相關規劃章節，且已部署具有 企業語音的 Enterprise Edition Server 或 Standard Edition Server。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如需關於使用 Lync Server 管理命令介面建立 回應群組的詳細資訊，包括範例指令碼，請參閱＜使用 Lync Server 管理命令介面建立您第一個回應群組＞，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=204108%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=204108&amp;clcid=0x404</a>。</td>
</tr>
</tbody>
</table>


## 本章節內容

  - [Lync Server 2013 中的回應群組設定權限和先決條件](lync-server-2013-response-group-configuration-permissions-and-prerequisites.md)

  - [Lync Server 2013 中的回應群組部署程序](lync-server-2013-deployment-process-for-response-group.md)

  - [在 Lync Server 2013 中建立工作流程的案例概觀](lync-server-2013-overview-of-workflow-creation-scenarios.md)

  - [在 Lync Server 2013 中建立回應群組代理群組](lync-server-2013-create-response-group-agent-groups.md)

  - [在 Lync Server 2013 中建立回應群組佇列](lync-server-2013-create-response-group-queues.md)

  - [(選用) 在 Lync Server 2013 中定義回應群組營業時間](lync-server-2013-optional-define-response-group-business-hours.md)

  - [(選用) 在 Lync Server 2013 中定義回應群組假日集](lync-server-2013-optional-define-response-group-holiday-sets.md)

  - [在 Lync Server 2013 中建立回應群組工作流程](lync-server-2013-create-response-group-workflows.md)

  - [(選用) 確認回應群組部署](lync-server-2013-optional-verify-response-group-deployment.md)

## 請參閱

#### 其他資源

[在 Lync Server 2013 中規劃通話管理功能](lync-server-2013-planning-for-call-management-features.md)

