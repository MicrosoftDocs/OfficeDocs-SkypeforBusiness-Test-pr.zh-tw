---
title: Lync Server 2013：通話許可控制的部署檢查清單
TOCTitle: 通話許可控制的部署檢查清單
ms:assetid: 7e56a169-3e63-44ab-bf28-1fdeb52381c8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398631(v=OCS.15)
ms:contentKeyID: 49291461
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的通話許可控制的部署檢查清單

 

_**上次修改主題的時間：** 2015-03-09_

若要有效規劃通話許可控制 (CAC)，您必須考量下列事項：

  - 部署 CAC 的先決條件

  - 部署 CAC 所需的資訊，以及您必須做出的組態決策，以便在開始部署時就有完整的必要資訊可供使用。

## 部署通話許可控制的先決條件

在部署通話許可控制之前，您必須已部署 Lync Server 2013 內部伺服器，包括 前端集區或 Standard Edition 伺服器。

## 通話許可控制的資訊需求

下表摘要說明部署通話許可控制所需的資訊。

### 部署通話許可控制的資訊需求

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>資訊</th>
<th>必要資訊的摘要</th>
<th>文件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>您組織所需的 Lync Server 功能</p></td>
<td><ul>
<li><p>您組織要支援的功能</p></li>
<li><p>要為個別使用者啟用的功能</p></li>
</ul></td>
<td><p><a href="lync-server-2013-defining-your-requirements-for-call-admission-control.md">在 Lync Server 2013 中定義通話許可控制需求</a></p></td>
</tr>
<tr class="even">
<td><p>要部署的拓撲和元件</p></td>
<td><ul>
<li><p>CAC 相關元件將自動連同 Lync Server 2013 一併安裝</p></li>
</ul>
<p></p></td>
<td><p><a href="lync-server-2013-defining-your-requirements-for-call-admission-control.md">在 Lync Server 2013 中定義通話許可控制需求</a></p></td>
</tr>
<tr class="odd">
<td><p>系統需求</p></td>
<td><ul>
<li><p>硬體需求</p></li>
<li><p>軟體需求</p></li>
<li><p>組合需求</p></li>
</ul>
<p></p></td>
<td><p><a href="lync-server-2013-determining-your-system-requirements.md">判定 Lync Server 2013 的系統需求</a></p></td>
</tr>
<tr class="even">
<td><p>基礎結構需求</p></td>
<td><ul>
<li><p>CAC 不需要特定的基礎結構需求</p></li>
</ul></td>
<td><p><a href="lync-server-2013-infrastructure-requirements-for-call-admission-control.md">Lync Server 2013 中的通話許可控制的基礎結構需求</a></p></td>
</tr>
<tr class="odd">
<td><p>網路介面需求</p></td>
<td><ul>
<li><p>內部與外部介面資訊</p></li>
<li><p>路由資訊 (包括 <a href="http://go.microsoft.com/fwlink/?linkid=203149%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=203149&amp;clcid=0x404</a> (Microsoft Lync Server 團隊的客戶回應管道) 的 NextHop 部落格上的資訊)</p></li>
</ul></td>
<td><p><a href="lync-server-2013-deploying-external-user-access.md">在 Lync Server 2013 中部署外部使用者存取</a></p></td>
</tr>
<tr class="even">
<td><p>部署策略</p></td>
<td><ul>
<li><p>部署順序</p></li>
<li><p>工作群組或網域</p></li>
<li><p>安全性</p></li>
<li><p>監控和稽核</p></li>
<li><p>硬體考量</p></li>
</ul></td>
<td><p><a href="lync-server-2013-best-practices-for-call-admission-control.md">Lync Server 2013 中通話許可控制的最佳做法</a></p></td>
</tr>
<tr class="odd">
<td><p>部署程序</p></td>
<td><ul>
<li><p>先決條件</p></li>
<li><p>資訊需求</p></li>
<li><p>處理和程序</p></li>
</ul></td>
<td><p><a href="lync-server-2013-configure-call-admission-control.md">在 Lync Server 2013 中設定通話許可控制</a></p></td>
</tr>
</tbody>
</table>

