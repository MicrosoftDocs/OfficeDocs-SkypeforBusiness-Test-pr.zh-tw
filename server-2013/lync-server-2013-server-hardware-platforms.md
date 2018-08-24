---
title: Lync Server 2013 伺服器硬體平台
TOCTitle: 伺服器硬體平台
ms:assetid: c964c1c0-0153-472b-88ad-a38866e0df0c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398835(v=OCS.15)
ms:contentKeyID: 49292307
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 的伺服器硬體平台

 

_**上次修改主題的時間：** 2015-03-09_

Lync Server 2013 伺服器角色和執行 Lync Server 系統管理工具的電腦需要 64 位元硬體。

Lync Server 2013 部署所用的特定硬體可能因大小和使用需求而異。本節描述建議的硬體。雖然這些只是建議而非必要需求，但使用不符合這些建議的硬體可能會產生重大的效能影響和其他問題。

## 建議的硬體平台

為達最佳效能，建議您在符合下表所列硬體需求的伺服器上執行 Lync Server。如果您使用功能性較低的硬體，可能會遇到功能性問題或效能不佳。請注意，這些硬體需求比舊版 Lync Server 的需求高，主要是因為在 Lync Server 2013 中，所有前端伺服器都會執行 SQL Server。

> [!NOTE]  
> NIC 小組受支援且應在 Lync Server 中顯示。若需詳細資料，請參閱 <a href="http://go.microsoft.com/fwlink/p/?linkid=389910">通訊伺服器或 Lync 伺服器與網路介面卡協力作業</a>。



### 前端伺服器、後端伺服器、Standard Edition Server、常設聊天室伺服器，以及常設聊天室儲存區與常設聊天室規範儲存區 (常設聊天室伺服器的後端伺服器角色) 的建議硬體

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>硬體元件</th>
<th>建議</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CPU</p></td>
<td><p>64 位元雙處理器、六核心、2.26 GHz 或更高</p>
<p>Lync Server 伺服器角色不支援 Intel Itanium 處理器。</p></td>
</tr>
<tr class="even">
<td><p>記憶體</p></td>
<td><p>32 GB</p></td>
</tr>
<tr class="odd">
<td><p>磁碟</p></td>
<td><ul>
<li><p>8 個 (含) 以上 10,000 RPM 硬碟機，每個至少有 72 GB 可用磁碟空間。</p>
<p>其中應有兩個磁碟使用 RAID 1，並有六個磁碟使用 RAID 10。</p>
<p>- 或者 -</p></li>
<li><p>固態硬碟 (SSD)，其提供類似 8 個 10,000 RPM 機械式磁碟機的效能。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>網路</p></td>
<td><ul>
<li><p>1 張 1 Gbps 或更高速度的雙連接埠網路卡 (建議使用 2 張，需要和單一 MAC 位址和單一 IP 位址搭配使用)</p></li>
</ul></td>
</tr>
</tbody>
</table>


### Edge Server、獨立中繼伺服器和 Director 的建議硬體

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>硬體元件</th>
<th>建議</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CPU</p></td>
<td><ul>
<li><p>64 位元雙處理器、四核心、2.0 GHz 或更高</p>
<p>- 或者 -</p></li>
<li><p>64 位元 4 向處理器、雙核心、2.0 GHz 或更高</p></li>
</ul>
<p>Lync Server 伺服器角色不支援 Intel Itanium 處理器。</p></td>
</tr>
<tr class="even">
<td><p>記憶體</p></td>
<td><p>16 GB</p></td>
</tr>
<tr class="odd">
<td><p>磁碟</p></td>
<td><ul>
<li><p>4 個 (含) 以上 10,000 RPM 磁碟機，每個至少有 72 GB 可用磁碟空間。</p>
<p>磁碟應使用 2x RAID 1 設定。</p>
<p>- 或者 -</p></li>
<li><p>固態硬碟 (SSD)，其提供類似 4 個 10,000 RPM 機械式磁碟機的效能。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>網路</p></td>
<td><ul>
<li><p>1 張 1 Gbps 或更高速度的雙連接埠網路卡 (建議使用 2 張，需要和單一 MAC 位址和單一 IP 位址搭配使用)。Edge Server 需要 2 個網路介面。</p></li>
</ul></td>
</tr>
</tbody>
</table>

