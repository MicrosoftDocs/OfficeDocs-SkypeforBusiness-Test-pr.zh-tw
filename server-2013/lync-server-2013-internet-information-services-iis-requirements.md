---
title: Lync Server 2013：Internet Information Services (IIS) 需求
TOCTitle: Internet Information Services (IIS) 需求
ms:assetid: 4f57a605-a8a9-4c5a-9a18-05ecb3d9ab6b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398321(v=OCS.15)
ms:contentKeyID: 49290892
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Internet Information Services (IIS) 需求

 

_**上次修改主題的時間：** 2015-03-09_

有數個 Lync Server 2013 元件需要 Internet Information Services (IIS)。本主題說明支援 Lync Server 所需的特定 IIS 功能。本節中的主題則說明 IIS 特定元件的需求。

當 Windows Server 2008 上啟用 Web 伺服器 (IIS) 角色時，預設會安裝各種角色服務。下表說明當 Windows Server 2008 上啟用 Web 伺服器 (IIS) 角色時，必須安裝的其他角色服務。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>角色服務</th>
<th>功能</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>一般 HTTP 功能</p></td>
<td><p>HTTP 重新導向</p></td>
</tr>
<tr class="even">
<td><p>應用程式開發</p></td>
<td><p>ASP.NET</p></td>
</tr>
<tr class="odd">
<td><p>應用程式開發</p></td>
<td><p>.NET 擴充性</p></td>
</tr>
<tr class="even">
<td><p>應用程式開發</p></td>
<td><p>ISAPI 擴充程式</p></td>
</tr>
<tr class="odd">
<td><p>應用程式開發</p></td>
<td><p>ISAPI 篩選器</p></td>
</tr>
<tr class="even">
<td><p>健康情況及診斷</p></td>
<td><p>記錄工具</p></td>
</tr>
<tr class="odd">
<td><p>健康情況及診斷</p></td>
<td><p>追蹤</p></td>
</tr>
<tr class="even">
<td><p>安全性</p></td>
<td><p>基本驗證</p></td>
</tr>
<tr class="odd">
<td><p>安全性</p></td>
<td><p>Windows 驗證</p></td>
</tr>
<tr class="even">
<td><p>管理工具</p></td>
<td><p>IIS 管理指令碼及工具</p></td>
</tr>
<tr class="odd">
<td><p>管理工具</p></td>
<td><p>IIS 6 管理相容性</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg398321.security(OCS.15).gif" title="security" alt="security" />安全性 附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您在 Windows Server 2008 作業系統上使用 IIS 7.0， Lync Server 安裝程式會停用 IIS 中的核心模式驗證。</td>
</tr>
</tbody>
</table>


## 本章節內容

  - [Lync Server 2013 中的前端集區與 Standard Edition Server 的 IIS 需求](lync-server-2013-iis-requirements-for-front-end-pools-and-standard-edition-servers.md)

