---
title: 驗證試驗集區與舊版集區共存
TOCTitle: 驗證試驗集區與舊版集區共存
ms:assetid: fe7e14bb-c7eb-4719-b154-009e99360520
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205420(v=OCS.15)
ms:contentKeyID: 49292922
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 驗證試驗集區與舊版集區共存

 

_**上次修改主題的時間：** 2012-09-29_

部署前導集區後，必須使用系統管理工具檢視集區資訊，以驗證兩個集區是否共存。在 Lync Server 2013 集區與舊版集區中，您必須使用 Lync Server 2013 控制台 與「拓撲產生器」工具。

## 驗證是否已啟動該 Lync Server 2013 服務

1.  從 Lync Server 2013 前端伺服器中瀏覽至：系統管理工具\\Services applet。

2.  驗證下列服務是否在前端伺服器中執行:

**Lync Server 2013 服務**

![已啟動的 Lync Server 服務清單](images/JJ205420.cfff9385-6bf6-461c-982c-e727c9f20b70(OCS.15).png "已啟動的 Lync Server 服務清單")

## 開啟 Lync Server 2013 控制台

從 Lync Server 2013 部署中的前端伺服器，開啟 Lync Server 2013 控制台 並選取 Lync Server 2010 集區。重複此程序以開啟 Lync Server 2013 集區。

**開啟 Lync Server 2013 控制台**

![\[選取 URL\] 對話方塊](images/JJ205420.b1f8e650-9c3c-4563-a403-5069f198342f(OCS.15).png "[選取 URL] 對話方塊")

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Lync Server 2013 上，您必須先將 Silverlight 升級為 Silverlight 版本 5 才能使用 Lync Server 控制台。</td>
</tr>
</tbody>
</table>


現在此拓撲包含 Lync Server 2010 與 Lync Server 2013 伺服器角色。

**Lync Server 2013 控制台拓撲頁面**

![\[Lync Server 控制台 - 拓撲\] 頁面](images/JJ205420.4ed1cc7a-cb3e-42f6-82e2-6d4d71d19352(OCS.15).jpg "[Lync Server 控制台 - 拓撲] 頁面")

## 請勿嘗試在 Lync Server 2010 拓撲產生器中開啟拓撲

如果您嘗試使用 Lync Server 2010 拓撲產生器開啟拓撲，就會遭遇以下問題。您僅可使用 Lync Server 2013 拓撲產生器檢視拓撲。 Lync Server 2013 拓撲產生器必須皆用於建立 Lync Server 2013 與 Lync Server 2010 的集區。

**Lync Server 2010 拓撲產生器錯誤訊息**

![Lync Server 拓撲產生器 MMC 貼齊錯誤](images/JJ205420.f6666343-c348-4d81-ae0e-6ba5a44e16c4(OCS.15).png "Lync Server 拓撲產生器 MMC 貼齊錯誤")

