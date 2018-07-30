---
title: 第 10 階段：解除委任舊版網站
TOCTitle: 第 10 階段：解除委任舊版網站
ms:assetid: d591a310-3b5c-4092-b19e-0349616e40df
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205300(v=OCS.15)
ms:contentKeyID: 49292460
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 第 10 階段：解除委任舊版網站

 

_**上次修改主題的時間：** 2012-10-16_

下列主題會指引您解除委任集區和從舊版的 Office Communications Server 2007 R2 部署停用和移除伺服器與集區。本節所列的程序並非全為必要程序。請閱讀各主題中的資訊，來判斷適用的解除委任程序。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ205186.Caution(OCS.15).gif" title="Caution" alt="Caution" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若您原先已將撥入會議的會議目錄匯入 Lync Server 2013，在開始解除委任集區之前，先將會議目錄所有權轉換至 Lync Server 2013 是相當重要的一件事。如果您解除委任集區時沒有先轉換會議目錄所有權，所有移轉會議的撥入功能都將無效。您必須先為舊集區中的每一個會議目錄，執行一次轉換所有權的步驟。</td>
</tr>
</tbody>
</table>


> [!IMPORTANT]  
> 如需在解除委任舊版環境之前移轉和升級 Microsoft Unified Communications Managed API (UCMA) 應用程式的詳細資訊，請參閱 <a href="http://go.microsoft.com/fwlink/p/?linkid=269555">http://go.microsoft.com/fwlink/p/?LinkId=269555</a>



## 本節內容

  - [移動會議目錄](move-conference-directories.md)

  - [更新 DNS SRV 記錄](update-dns-srv-records_1.md)

  - [解除委任伺服器與集區](decommissioning-servers-and-pools.md)

  - [移除 BackCompatSite](remove-backcompatsite.md)

