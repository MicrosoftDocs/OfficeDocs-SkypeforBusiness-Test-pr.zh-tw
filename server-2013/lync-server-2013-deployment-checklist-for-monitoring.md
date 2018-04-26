---
title: Lync Server 2013：監控的部署檢查表
TOCTitle: 監控的部署檢查表
ms:assetid: 4e798370-277c-4391-84b4-13a972b45ca6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204874(v=OCS.15)
ms:contentKeyID: 49890060
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中監控的部署檢查表

 

_**上次修改主題的時間：** 2015-03-09_

雖然每一部前端伺服器上都已經安裝及啟動監控功能，您仍然必須先執行幾個步驟，才能夠實際開始收集 Microsoft Lync Server 2013 的監控資料。這些步驟如下面的檢查清單所述：


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>階段</p></td>
<td><p>步驟</p></td>
<td><p>角色與群組成員資格</p></td>
<td><p>文件</p></td>
</tr>
<tr class="even">
<td><p><strong>安裝先決條件硬體與軟體</strong></p></td>
<td><p>在要作為監控之用的後端資料存放區的電腦上，安裝支援的 Microsoft SQL Server 版本。</p></td>
<td><p>同時也是本機系統管理員群組成員的網域使用者。</p></td>
<td><p>《支援能力指南》中的 <a href="lync-server-2013-supported-hardware.md">Lync Server 2013 的受支援硬體</a></p>
<p>《支援能力指南》中的 <a href="lync-server-2013-server-software-and-infrastructure-support.md">Lync Server 2013 中的伺服器軟體和基礎結構支援</a></p></td>
</tr>
<tr class="odd">
<td><p><strong>[建立適當的內部拓撲以支援監控]</strong></p></td>
<td><p>使用 Lync Server 2013 拓樸產生器將監控資料庫新增至拓樸，然後發行更新的拓樸。</p></td>
<td><p>如果要定義拓樸，屬於本機使用者群組成員的使用者。</p>
<p>如果要發行拓樸，屬於網域管理員群組和 RTCUniversalServerAdmins 群組成員的使用者。</p></td>
<td><p>《部署指南》中的 <a href="lync-server-2013-associating-a-monitoring-store-with-a-front-end-pool.md">在 Lync Server 2013 中讓監控儲存區與前端集區產生關聯</a></p></td>
</tr>
<tr class="even">
<td><p><strong>啟用適當的監控設定</strong></p></td>
<td><p>啟用全域範圍和/或網站範圍的詳細通話記錄 (CDR) 和/或經驗品質 (QoE) 監控。</p></td>
<td><p>屬於 RTCUniversalServerAdmins 群組成員的使用者，或被指派提供 CsCdrConfiguration 和 CsQoEConfiguration Cmdlet 存取權的 RBAC 角色的使用者。</p></td>
<td><p>《作業指南》中的 <a href="lync-server-2013-configuring-call-detail-recording-and-quality-of-experience-settings.md">在 Lync Server 2013 中設定詳細通話記錄及經驗品質設定</a></p></td>
</tr>
</tbody>
</table>

