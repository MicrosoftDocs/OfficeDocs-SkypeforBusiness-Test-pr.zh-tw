---
title: 使用使用者模型規劃 Lync Server 2013 容量
TOCTitle: 使用使用者模型規劃容量
ms:assetid: 902ab23e-94d6-482a-9d6e-c0b28dc3e03d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg615015(v=OCS.15)
ms:contentKeyID: 49890207
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 使用使用者模型針對 Lync Server 2013 規劃容量

 

_**上次修改主題的時間：** 2015-03-09_

本節提供指引，根據 [Lync Server 2013 中的使用者模型](lync-server-2013-user-models.md)中描述的使用方式，說明針對網站的使用者數目，該網站上需要多少部伺服器。

## 經過測試的硬體平台

本節中的所有效能結果與部署建議都是根據在執行下表所述之硬體的伺服器上進行測試所得到的效能。建議您使用類似的硬體。如果您使用功能性較低的硬體，可能會遇到功能性問題或效能不佳。請注意，這些硬體建議都會比舊版 Lync Server 的硬體建議還要高階。

### 效能測試中使用的硬體

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
<li><p>8 個 (含) 以上的 10,000 RPM 硬碟且至少 72 GB 的可用磁碟空間。</p>
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


## 結果摘要

下表彙總這些建議。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>伺服器角色</th>
<th>支援的使用者數目上限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>含 12 部 前端伺服器和一部 後端伺服器或一對鏡像的 後端伺服器的 前端集區。</p></td>
<td><p>同時登入 80,000 位唯一使用者，加上 50% 的多點出席 (MPOP) (代表非行動執行個體)，加上 40% 之已針對「行動性」啟用的使用者，總共 152,000 個端點。</p></td>
</tr>
<tr class="even">
<td><p>A/V 會議</p></td>
<td><p>前端集區提供的 A/V 會議服務支援集區的會議，但前提假設會議大小上限為 250 位使用者，而且一次只會舉行一個這類大型會議。</p>
<div>

> [!NOTE]  
> 此外，您可以部署含有兩部 前端伺服器的個別 前端集區來舉行大型會議，藉以支援使用者介於 250 位和 1000 位之間的大型會議。如需詳細資訊，請參閱＜ <a href="lync-server-2013-supporting-large-meetings.md">使用 Lync Server 2013 支援大型會議</a>＞。


</div></td>
</tr>
<tr class="odd">
<td><p>一個 Edge Server</p></td>
<td><p>12,000 位同時使用的遠端使用者</p></td>
</tr>
<tr class="even">
<td><p>一個 Director</p></td>
<td><p>12,000 位同時使用的遠端使用者</p></td>
</tr>
<tr class="odd">
<td><p>監控和封存</p></td>
<td><p>在 Lync Server 2013 中，[監控和封存] 前端服務現在會在每部 前端伺服器上執行，而不是在個別的伺服器角色上執行。</p>
<p>[監控和封存] 仍然各自需要它們自己的資料庫存放區。如果您同時執行 Exchange 2013，則可將封存資料保留於 Exchange 中，而不是在專屬的 SQL 資料庫中。</p></td>
</tr>
<tr class="even">
<td><p>一部 中繼伺服器</p></td>
<td><p>與 前端伺服器組合的 中繼伺服器會在集區中的每部 前端伺服器上執行，而且應該為集區中的使用者提供足夠的容量。針對獨立 中繼伺服器，請參閱本主題後續的＜ 中繼伺服器＞一節。</p></td>
</tr>
<tr class="odd">
<td><p>一部 Standard Edition 伺服器</p></td>
<td><p>我們極力建議，如果您使用 Standard Edition 伺服器為使用者提供主機服務，務必以兩部伺服器配對使用，並採用＜ <a href="lync-server-2013-planning-for-high-availability-and-disaster-recovery.md">在 Lync Server 2013 中規劃高可用性和災害復原</a>＞中的建議。其中每部伺服器可以為多達 2,500 位使用者提供主機服務，而在容錯移轉案例中，如果其中一部伺服器故障，剩下的伺服器可以支援 5,000 位使用者。</p>
<p>如果您的部署包含大量音訊或視訊流量，則每一伺服器上有 2,500 位以上的使用者時，伺服器效能可能會受到影響。在這種情況下，您應該考慮增加更多部 Standard Edition 伺服器或移至 Lync ServerEnterprise Edition。</p></td>
</tr>
</tbody>
</table>


## 前端伺服器

> [!NOTE]  
> 這個伺服器角色不支援延伸的集區。



在 前端集區中，集區中每 6,660 位使用者就應該有一部 前端伺服器，前提假設已在集區中的所有伺服器上啟用超執行緒功能，而且伺服器硬體符合 [Lync Server 2013 的伺服器硬體平台](lync-server-2013-server-hardware-platforms.md)中的建議。一個 前端集區中的最大使用者數目是 80,000，前提假設已在集區中的所有伺服器上啟用超執行緒功能。如果網站中有 80,000 位以上的使用者，則可以部署一個以上的 前端集區。

當您考量 前端集區中的使用者數目時，請納入位於與此 前端集區相關聯的分公司的 Survivable Branch Appliance 和 Survivable Branch 伺服器上的使用者。

當動態伺服器無法使用時，會將其連線自動轉接至集區中的其他伺服器。例如，如果您有 30,000 位使用者和五部 前端伺服器，當其中一部伺服器無法使用時，6000 位使用者的連線需要轉接至其餘四部伺服器。其餘四部伺服器將各有 7500 位使用者，大於建議的數目。

如果您在一開始為 30,000 位使用者使用六部 前端伺服器，但後續有一部變成無法使用，則所有的 5000 位使用者全都將移至其餘的五部伺服器上。這五部伺服器將各自裝載 6000 位使用者，這在建議範圍內。

前端集區中的使用者數目上限為 80,000。集區中的 前端伺服器數目上限為 12。

針對含有 80,000 位使用者的 前端集區，在遵循 [Lync Server 2013 中的使用者模型](lync-server-2013-user-models.md)的標準部署中，12 部 前端伺服器對效能而言就已足夠。設計來支援災害復原容錯移轉的部署假設最多可在兩對 前端集區中的每一對上裝載 40,000 位使用者，其中的每個集區都具有足夠的 前端伺服器，讓這兩個集區中的使用者應該能夠在需要時彼此進行容錯移轉。

特定的 前端集區為取得良好效能而支援的使用者數目，會基於下列因素而與這些數目不同：

  - 前端伺服器的硬體不符合 [Lync Server 2013 的伺服器硬體平台](lync-server-2013-server-hardware-platforms.md)中的建議。

  - 組織的使用方式與使用者模型差異極大，例如大量的會議流量。

> [!IMPORTANT]  
> 在 Lync Server 2013 中，狀態資料庫現在裝載於 前端伺服器上，不同於 Lync Server 2010，它們是裝載於 後端伺服器。這表示 前端伺服器的磁碟效能與容量應該會受到本節先前所列和 <a href="lync-server-2013-server-hardware-platforms.md">Lync Server 2013 的伺服器硬體平台</a>中的建議所影響，而不論您的 前端伺服器中裝載了多少位使用者。



下表根據 [Lync Server 2013 中的使用者模型](lync-server-2013-user-models.md)中定義的使用者模型，顯示 IM 和目前狀態的平均頻寬。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>每位使用者的平均頻寬</th>
<th>每個含有 6,660 位使用者的 前端伺服器的頻寬需求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1.3 Kpbs</p></td>
<td><p>13 Mbps</p></td>
</tr>
</tbody>
</table>


> [!NOTE]  
> 若要提升 前端伺服器上並存之 A/V 會議與 中繼伺服器功能的媒體效能，您應該在 前端伺服器的介面卡上啟用接收端調整 (RSS)。RSS 可讓伺服器上的多個處理器平行處理連入封包。如需詳細資訊，請參閱 <a href="http://go.microsoft.com/fwlink/?linkid=268731" class="uri">http://go.microsoft.com/fwlink/?linkid=268731</a> 上的＜Windows Server 2008 中的接收端調整增強功能＞。如需如何啟用 RSS 的詳細資訊，請參閱網路介面卡文件。



## 會議最大值

假設集區中的使用者隨時有 5% 在參加會議，根據這樣一個使用者模型，含有 80,000 位使用者的集區隨時大約有 4,000 位使用者在參加會議。這些會議通常有各種形式的媒體 (例如，部分為僅有 IM、部分為有語音的 IM、部分為音訊/視訊) 和各種數目的參與者。實際允許的會議數目並沒有強制限制，而實際使用量會決定實際效能。例如，如果您的組織擁有比使用者模型假設還要更多的混合模式會議，則您可能需要部署比本文件建議還要更多的 前端伺服器或 A/V 會議伺服器。如需關於使用者模型中各種假設的詳細資訊，請參閱 [Lync Server 2013 中的使用者模型](lync-server-2013-user-models.md)。

標準 Lync Server 2013前端集區支援的最大會議規模為 250 位參與者。當有一個 250 位使用者的會議正在進行時，集區仍然可以支援其他會議，如此，總共可支援 5% 的集區使用者同時進行會議。例如，在含有 12 部 前端伺服器和 80,000 位使用者的集區中，當有一個 250 位使用者的會議進行時， Lync Server 可支援其他 3,750 位使用者參與小型會議。

不論有多少使用者位於 前端集區或 Standard Edition Server，當集區或伺服器上有一個 250 位使用者的會議正在進行時， Lync Server 至少可支援其他 125 位使用者參與相同集區或伺服器上的小型會議。

若要舉行使用者人數介於 250 位和 1000 位之間的會議，您可以將個別的 前端集區設定為僅舉行這些會議。此 前端集區將不會裝載任何使用者。如需詳細資訊，請參閱＜ [使用 Lync Server 2013 支援大型會議](lync-server-2013-supporting-large-meetings.md)＞。

如果您的組織擁有比使用者模型假設還要更多的混合模式會議，則您可能需要部署比本文件建議還要更多的 前端伺服器 (上限為 12 FE)。如需關於使用者模型中各種假設的詳細資訊，請參閱 [Lync Server 2013 中的使用者模型](lync-server-2013-user-models.md)。

## Edge Server

> [!NOTE]  
> 這個伺服器角色不支援延伸的集區。



針對同時存取網站的每 12,000 位遠端使用者，您應該部署一部 Edge Server。建議最少使用兩部 Edge Server ，以獲得高可用性。這些建議假設您的 Edge Server 硬體符合 [Lync Server 2013 的伺服器硬體平台](lync-server-2013-server-hardware-platforms.md)中的建議。

當您考量 Edge Server 的使用者數目時，請納入位於與此網站的 前端集區相關聯的分公司的 Survivable Branch Appliance 和 Survivable Branch 伺服器上的使用者。

> [!NOTE]  
> 若要提升 Edge Server上 A/V Conferencing Edge service 的效能，您應該在 Edge Server 的介面卡上啟用接收端調整 (RSS)。RSS 可讓伺服器上的多個處理器平行處理連入封包。如需詳細資訊，請參閱 <a href="http://go.microsoft.com/fwlink/?linkid=268731" class="uri">http://go.microsoft.com/fwlink/?linkid=268731</a> 上的＜Windows Server 2008 中的接收端調整增強功能＞。如需如何啟用 RSS 的詳細資訊，請參閱網路介面卡文件。



## Director

> [!NOTE]  
> 這個伺服器角色不支援延伸的集區。



如果您部署 Director 伺服器角色，建議您針對同時存取網站的每 12,000 位遠端使用者部署一部 Director。建議最少使用兩個 Director，以獲得高可用性。這些建議假設您的 Edge Server 硬體符合 [Lync Server 2013 的伺服器硬體平台](lync-server-2013-server-hardware-platforms.md)中的建議。

當您考量 Director 的使用者數目時，請納入位於與此網站的 前端集區相關聯的分公司的 Survivable Branch Appliance 和 Survivable Branch 伺服器上的使用者。

## 中繼伺服器

> [!NOTE]  
> 這個伺服器角色不支援延伸的集區。



如果您將 中繼伺服器與 前端伺服器組合， 中繼伺服器便會在集區中的每部 前端伺服器上執行，而且應該為集區中的使用者提供足夠的容量。

如果您部署獨立 中繼伺服器集區，則要部署多少部 中繼伺服器取決於許多因素，包括 中繼伺服器使用的硬體、VoIP 使用者數目、每個 中繼伺服器集區所控制的閘道對等數目、通過這些閘道的尖峰時段流量，以及略過 中繼伺服器的通話百分比。

下表提供指引，說明 中繼伺服器可處理多少同時進行的通話，但前提假設 中繼伺服器的硬體符合 [Lync Server 2013 的伺服器硬體平台](lync-server-2013-server-hardware-platforms.md)中的建議，並且已啟用超執行緒功能。如需關於 中繼伺服器延展性的詳細資訊，請參閱＜ [針對 Lync Server 2013 評估語音使用方式和流量](lync-server-2013-estimating-voice-usage-and-traffic.md)＞及＜ [Lync Server 2013 中的中繼伺服器的部署指導方針](lync-server-2013-deployment-guidelines-for-mediation-server.md)＞。

下列所有表格均根據 [Lync Server 2013 中的使用者模型](lync-server-2013-user-models.md)中的摘要來假設使用量。

### 獨立 中繼伺服器容量：70% 內部使用者，30% 不含非旁路通話容量的外部使用者 (透過 中繼伺服器執行媒體轉碼)

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>伺服器硬體</th>
<th>通話數目上限</th>
<th>T1 線路數目上限</th>
<th>E1 線路數目上限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>雙處理器、六核心的 2.26 GHz 超執行緒 CPU ( <strong>已停用超執行緒</strong>)，搭載 32 GB 記憶體和一張雙埠網路介面卡。</p></td>
<td><p>1100</p></td>
<td><p>46</p></td>
<td><p>35</p></td>
</tr>
<tr class="even">
<td><p>雙處理器、六核心的 2.26 GHz 超執行緒 CPU，搭載 32 GB 記憶體和一張雙埠網路介面卡。</p></td>
<td><p>1500</p></td>
<td><p>63</p></td>
<td><p>47</p></td>
</tr>
</tbody>
</table>


> [!NOTE]  
> 雖然在效能測試時使用含 32 GB 記憶體的伺服器，但獨立 中繼伺服器支援含 16 GB 記憶體的伺服器，而且足以提供本表格中顯示的效能。



### 中繼伺服器容量 (已與 前端伺服器組合的 中繼伺服器) 70% 內部使用者、30% 外部使用者、非旁路通話容量 (透過 中繼伺服器執行媒體處理)

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>伺服器硬體</th>
<th>通話數目上限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>雙處理器、六核心的 2.26 GHz 超執行緒 CPU，搭載 32 GB 記憶體和 2 張 1GB 網路介面卡。</p></td>
<td><p>150</p></td>
</tr>
</tbody>
</table>


> [!NOTE]  
> 此數字小於獨立 中繼伺服器的數目，因為除了需要為語音通話進行轉碼之外， 前端伺服器還必須為其上的 6600 位使用者處理其他特性與功能。



> [!NOTE]  
> 若要提升 中繼伺服器的效能，您應該在 中繼伺服器 的介面卡上啟用接收端調整 (RSS)。RSS 可讓伺服器上的多個處理器平行處理連入封包。如需詳細資訊，請參閱 <a href="http://go.microsoft.com/fwlink/?linkid=268731" class="uri">http://go.microsoft.com/fwlink/?linkid=268731</a> 上的＜Windows Server 2008 中的接收端調整增強功能＞。如需如何啟用 RSS 的詳細資訊，請參閱網路介面卡文件。



## 後端伺服器

在 Lync Server 2013 中，狀態資料庫位於 前端伺服器上，而不是 後端伺服器上。這會針對 Lync Server 2013 中的每部 後端伺服器產生更簡單的需求，相當於 前端伺服器的硬體需求。相較於 Lync Server 2010，其中需要 後端伺服器來做為含有 25 個磁碟且等級更高的伺服器。但是， 後端伺服器的工作負載仍然要求您應該符合本節先前所列和 [Lync Server 2013 的伺服器硬體平台](lync-server-2013-server-hardware-platforms.md)中的硬體建議。

若要為 後端伺服器提供高可用性，建議部署伺服器鏡像。如需詳細資訊，請參閱＜ [Lync Server 2013 中的後端伺服器高可用性](lync-server-2013-back-end-server-high-availability.md)＞。

## 監控和封存

在 Lync Server 2013 中，如果您部署 \[監控或封存\]，這些服務的前端功能便會在 前端伺服器上執行，而不是在個別的伺服器角色上執行。\[監控和封存\] 仍然會各自使用它們自己的資料庫存放區 (與後端存放區不同)。如果您已部署 Exchange 2013，就可以在 Exchange 中而不是在專屬的 SQL 存放區中儲存立即訊息封存資料。

下表說明針對監控與封存資料，每位使用者每天大約需要多少資料庫儲存空間。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p><strong>CDR (監控)</strong></p></td>
<td><p><strong>QoE (監控)</strong></p></td>
<td><p><strong>封存</strong></p></td>
</tr>
<tr class="even">
<td><p>每位使用者每天所需的磁碟空間</p></td>
<td><p>49 KB</p></td>
<td><p>28 KB</p></td>
<td><p>57 KB</p></td>
</tr>
</tbody>
</table>


Microsoft 在進行效能測試期間，會針對用於監控和封存的資料庫伺服器使用下表中的硬體。此測試會收集兩個 前端集區的資料，每一個會包含 80,000 位使用者。

### 監控與封存效能測試中使用的硬體

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
<td><p>64 位元雙處理器、六核心、2.26 GHz 或更高</p></td>
</tr>
<tr class="even">
<td><p>記憶體</p></td>
<td><p>48 GB</p></td>
</tr>
<tr class="odd">
<td><p>磁碟</p></td>
<td><p>25 個 10,000 RPM 硬碟，每個磁碟上配備 300 GB，並包含下列設定</p>
<h3 id="section-3"> </h3>
<div>
<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>磁碟機</strong></p></td>
<td><p><strong>RAID 設定</strong></p></td>
<td><p><strong>磁碟數目</strong></p></td>
</tr>
<tr class="even">
<td><p>單一磁碟機上的 CDR、QoE 及封存資料庫資料檔案</p></td>
<td><p>1+0</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>CDR 資料庫記錄檔</p></td>
<td><p>1</p></td>
<td><p>2</p></td>
</tr>
<tr class="even">
<td><p>QoE 資料庫記錄檔</p></td>
<td><p>1</p></td>
<td><p>2</p></td>
</tr>
<tr class="odd">
<td><p>封存資料庫記錄檔</p></td>
<td><p>1</p></td>
<td><p>2</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
<tr class="even">
<td><p>網路</p></td>
<td><ul>
<li><p>1 張 1 Gbps 或更高速度的雙連接埠網路卡 (建議使用 2 張，需要和單一 MAC 位址和單一 IP 位址搭配使用)</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 本節內容

  - [針對 Lync Server 2013 評估語音使用方式和流量](lync-server-2013-estimating-voice-usage-and-traffic.md)

  - [Lync Server 2013 中的中繼伺服器的部署指導方針](lync-server-2013-deployment-guidelines-for-mediation-server.md)

