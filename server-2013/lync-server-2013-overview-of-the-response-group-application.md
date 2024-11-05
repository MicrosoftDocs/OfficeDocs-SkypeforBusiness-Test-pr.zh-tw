﻿---
title: Lync Server 2013：回應群組應用程式概觀
TOCTitle: 回應群組應用程式概觀
ms:assetid: 6cc333e7-4029-4372-86b2-016040c415fb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398513(v=OCS.15)
ms:contentKeyID: 49291245
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的回應群組應用程式概觀

 

_**上次修改主題的時間：** 2015-03-09_

來電者與回應群組通話時，該通話會根據群組搜尋或來電者對互動語音回應 (IVR) 問題的回答，路由傳送給代理人。 回應群組應用程式使用標準回應群組路由方法，將通話路由傳送給下一個有空的代理人。通話路由方法包括序列、最長閒置時間、平行、循環配置資源及應答路由 (也就是說，所有代理人都會同時接獲每一通來電，不論他們目前是否有空)。如果沒有代理人有空，則會將通話保留在佇列中，直到某位代理人有空。通話保留在佇列時，來電者會聽到音樂，直到某位有空的代理人受理該通話。如果佇列已滿，或通話在佇列中逾時，則來電者可能會聽到訊息，然後便中斷通話或將通話轉接至不同的目的地。依系統管理員設定回應群組的方式不同，代理人受理通話時，來電者不一定會看到代理人的身分識別。代理人得以正式方式受理通話 (表示他們必須先登入群組，才能受理路由傳送給群組的通話)，或以非正式方式受理通話 (表示他們未登入及登出群組就受理通話)。

> [!NOTE]  
> 代理人只能為內部部署使用者。若代理人從內部部署移至線上， 回應群組通話將不會路由傳送至該代理人。



> [!NOTE]  
> 回應群組應用程式使用內部服務 (稱為「配對」) 將通話置入佇列，並尋找有空的代理人。每部執行 回應群組應用程式的電腦都會執行配對服務，但是一個 Lync Server 集區一次只會有一個主動配對服務，其他則是被動配對服務。如果主動配對服務在意外中斷服務期間無法使用，則被動配對服務其中之一會變成主動配對服務。 回應群組應用程式會盡全力確保通話路由及佇列持續不中斷。但是在轉換配對服務時，所有轉接中的通話都會中斷。例如，如果轉換是因 前端伺服器當機所導致，則該 前端伺服器上主動配對服務目前所處理的任何通話也會中斷。



在 Lync Server 2013 中，可使用兩個管理角色來管理回應群組： 回應群組管理員以及 回應群組系統管理員。 回應群組系統管理員可管理任何回應群組的所有層面； 回應群組管理員僅可以管理某些層面，而且只能管理其所擁有的回應群組。新的管理員角色有助於降低管理成本，因為您可以將特定回應群組的有限職責委派給任何已啟用 企業語音的使用者。

因應新的管理員角色， Lync Server 2013回應群組應用程式採用「受管理」或「未受管理」 **\[工作流程類型\]** 。下表描述「已受管理」與「未受管理」回應群組內容。

### 受管理與未受管理回應群組

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>回應群組類型</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>未受管理</p></td>
<td><ul>
<li><p>未受管理的回應群組沒有指定的管理員。只有 回應群組系統管理員能夠設定這些回應群組。</p></li>
<li><p>多個未受管理回應群組可共用一個佇列或代理人群組。</p></li>
<li><p>當您將回應群組從舊版本移轉至 Lync Server 2013 的時候，會設定為「未受管理」類型。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>受管理</p></td>
<td><ul>
<li><p>回應群組系統管理員可設定受管理之回應群組的任何層面。</p></li>
<li><p>回應群組管理員無法對未明確指派給他們的回應群組進行檢視或修改。</p></li>
<li><p>回應群組管理員只能對明確指派給他們的回應群組進行部分的設定。</p></li>
<li><p>受管理的回應群組無法與其他任何受管理或未受管理的回應群組共用任何佇列或代理人群組。</p></li>
</ul></td>
</tr>
</tbody>
</table>


下表描述 回應群組管理員對於受到指派的回應群組，可以執行以及無法執行的動作。

### 回應群組管理員功能

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>可設定：</th>
<th>可建立、刪除或設定：</th>
<th>無法：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>代理人</p></li>
<li><p>歡迎訊息</p></li>
<li><p>回應群組名稱</p></li>
<li><p>說明</p></li>
<li><p>顯示號碼</p></li>
<li><p>營業時間</p></li>
<li><p>保留音樂</p></li>
<li><p>狀態 (使用中/非使用中)</p></li>
<li><p>群組搜尋工作流程或互動語音回應 (IVR) 工作流程</p></li>
</ul></td>
<td><ul>
<li><p>代理人群組</p></li>
<li><p>佇列</p></li>
<li><p>假日集</p></li>
</ul></td>
<td><ul>
<li><p>建立或刪除任何工作流程類型</p></li>
<li><p>修改核心回應群組設定，例如： <strong>[SIP URI]</strong> 、 <strong>[電話號碼]</strong> 或 <strong>[工作流程類型]</strong> 。</p></li>
</ul></td>
</tr>
</tbody>
</table>


回應群組管理員可使用下列工具以管理其指定的回應群組。

  - Lync Server 控制台
    
    > [!NOTE]  
    > 回應群組管理員只能藉由此工具管理 回應群組設定，無法使用其他 Lync Server 設定。
    


  - 回應群組設定工具

  - Lync Server 管理命令介面

回應群組可針對部門或工作群組環境進行適當調整 (如需詳細資訊，請參閱＜ [Lync Server 2013 中的回應群組的容量規劃](lync-server-2013-capacity-planning-for-response-group.md)＞)，而且可以部署在全新的電話語音安裝中；並支援 企業語音部署及本地電信業者網路的來電。代理人可以使用 Lync 2013、 Lync 2010、 Lync 2010 Attendant 或 Lync Phone Edition 來接聽路由傳送給他們的通話。

回應群組應用程式是 企業語音的元件。當您部署 企業語音時，會自動安裝及啟動 回應群組應用程式。
