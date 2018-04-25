---
title: Lync Server 2013：Director 的軟硬體需求
TOCTitle: Director 的軟硬體需求
ms:assetid: 747b701e-7f97-46fe-91c5-1e8d9addf9f7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398560(v=OCS.15)
ms:contentKeyID: 49291316
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中 Director 的軟硬體需求

 

_**上次修改主題的時間：** 2015-03-09_

本節詳述 Director 的硬體及軟體需求，以及支援的 Director 組合案例。

## Director 的硬體需求

下表列出 Director 的硬體需求：

### Director 的硬體需求

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>硬體元件</th>
<th>最低需求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CPU</p></td>
<td><ul>
<li><p>64 位元處理器、四核心、2.0 GHz 或更快速度</p></li>
<li><p>64 位元雙處理器、四核心、2.0 GHz 或更快速度</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>記憶體</p></td>
<td><p>4 GB</p></td>
</tr>
<tr class="odd">
<td><p>磁碟</p></td>
<td><ul>
<li><p>10K RPM 硬碟 (HDD)</p></li>
<li><p>高效能固態硬碟 (SSD)，效能等於或優於 10K RPM HDD</p></li>
<li><p>2x RAID 10 (等量和鏡像)，15K RPM 磁碟用於資料庫資料檔</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>網路</p></td>
<td><ul>
<li><p>雙埠 1 Gbps 的網路介面卡 (建議)</p></li>
<li><p>單一 1 Gbps 網路介面卡 (支援)</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Director 的軟體需求

Director 角色只能部署在執行 Lync Server 2013 Enterprise Edition 的伺服器上。

Director 需要下列其中一種 64 位元作業系統：

  - Windows Server 2008 R2 Standard Service Pack 1 作業系統

  - Windows Server 2008 R2 Enterprise Service Pack 1 作業系統

  - Windows Server 2008 R2 Datacenter Service Pack 1 作業系統

  - Windows Server 2012 Standard 作業系統

  - Windows Server 2012 Datacenter 作業系統

Lync Server 2013 亦需要安裝下列 [Lync Server 2013 中的其他伺服器支援和需求](lync-server-2013-additional-server-support-and-requirements.md)主題中所詳述的程式及更新。

## 支援的組合

Director 伺服器角色無法與 Lync Server 2013 中的任何其他伺服器角色組合，然而，如果您並未部署 Director，則 前端伺服器會假定角色。

