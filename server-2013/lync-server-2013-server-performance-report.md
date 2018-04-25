---
title: Lync Server 2013：伺服器效能報告
TOCTitle: 伺服器效能報告
ms:assetid: 942bb39a-1790-498e-9d99-8f6ce2d155c3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg615018(v=OCS.15)
ms:contentKeyID: 49291700
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的伺服器效能報告

 

_**上次修改主題的時間：** 2015-03-09_

伺服器效能報告提供通話不良百分比最高的 Microsoft Lync Server 2013 伺服器清單。此報告會依照伺服器類型來細分伺服器，分別針對下列類型來報告統計資料：

  - 中繼伺服器

  - A/V 會議伺服器

  - A/V Edge Server

  - 閘道 (中繼伺服器)

  - 閘道 (中繼伺服器旁路)

  - 視訊 (包含適用於 A/V 會議伺服器和 A/V Edge Server 的視訊計量)

  - 應用程式共用 (包含適用於 A/V 會議伺服器和 A/V Edge Server 的應用程式共用計量)

請務必注意此報告中所示的排名是相對排名。例如，假設效能最差的伺服器在其處理的 1,000 個通話中有一個品質不良的通話。這個百分比高於可接受的百分比 .1%。但是，如果這是您擁有之效能最差的伺服器 (亦即，假設您所有其他伺服器的通話不良百分比甚至是低於 .1%)，則該伺服器仍然會出現在伺服器效能報告中。

## 存取伺服器效能報告

伺服器效能報告可以從 \[監控報告\] 首頁進行存取。您可以按一下下列任一個計量，向下切入至 [Lync Server 2013 中的通話清單報告](lync-server-2013-call-list-report.md)：

  - 通話數

  - 通話不良百分比

此外，您可以按一下下列計量，向下切入至伺服器媒體品質趨勢報告：

  - 趨勢

## 伺服器效能報告的最佳用法

伺服器效能報告提供數種方法來篩選資料，例如，您可以根據網路類型 (撥打自有線連線的通話與撥打自無線連線的通話) 和存取類型 (從防火牆內部撥打的通話與從防火牆外部撥打的通話) 進行篩選。最好是在檢視伺服器效能報告時使用這些篩選器。例如，假設您擁有一部中繼伺服器，其通話不良百分比為 3.24%。如果您單獨查看無線通話，該相同伺服器的通話不良百分比會達到 20%。這表示伺服器在接聽無線電話時發生問題，問題可能有些模糊，因為伺服器在接聽有線通話時並沒有發生任何問題。

## 篩選器

篩選器可以讓您傳回更精確的資料集或者以不同方法檢視傳回的資料。例如，伺服器效能報告可讓您依伺服器類型或網路類型 (有線或無線) 篩選傳回的資料。您也可以選擇資料的分組方式。在這種情況下，資料會按照小時、日、星期或月來分組的。

下表列出您可以搭配伺服器效能報告的篩選器。

### 伺服器效能報告篩選器

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>名稱</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>從</strong></p></td>
<td><p>時間範圍的開始日期/時間。若要按照小時檢視資料，請輸入開始日期和時間，如下所示：</p>
<p>7/7/2012 1:00 PM</p>
<p>如果您未輸入開始時間，報告會自動從指定日期凌晨 12 點開始。若要按照日期檢視資料，只要輸入日期即可：</p>
<p>7/7/2012</p>
<p>若要按星期或月份查看，請輸入當週或該月您想查看的日期 (您不必輸入當週或該月的第一天)：</p>
<p>7/3/2012</p>
<p>星期永遠是從星期日開始星期六結束。</p></td>
</tr>
<tr class="even">
<td><p><strong>到</strong></p></td>
<td><p>時間範圍的結束日期/時間。若要按照小時檢視資料，請輸入開始日期和時間，如下所示：</p>
<p>7/7/2012 1:00 PM</p>
<p>如果您未輸入結束時間，報告會自動在指定日期凌晨 12 點結束。若要按照日期檢視資料，只要輸入日期即可：</p>
<p>7/7/2012</p>
<p>若要按星期或月份查看，請輸入當週或該月您想查看的日期 (您不必輸入當週或該月的第一天)：</p>
<p>7/3/2012</p>
<p>星期永遠是從星期日開始星期六結束。</p></td>
</tr>
<tr class="odd">
<td><p><strong>伺服器類型</strong></p></td>
<td><p>指出要產生效能報告的伺服器類型。請選取下列其中一項：</p>
<ol>
<li><p>[全部]</p></li>
<li><p>中繼伺服器</p></li>
<li><p>A/V 會議伺服器</p></li>
<li><p>A/V Edge Server</p></li>
</ol></td>
</tr>
<tr class="even">
<td><p><strong>榜尾數量</strong></p></td>
<td><p>指出每個類別要顯示的伺服器數量 (依它們的通話不良率來排名)。例如，設為 <strong>5</strong> 就會顯示出前五名表現最差的伺服器。請選取下列其中一項：</p>
<ol>
<li><p>[全部]</p></li>
<li><p>5</p></li>
<li><p>10</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p><strong>存取類型</strong></p></td>
<td><p>指出撥打電腦時，用戶端是否登入內部網路或外部網路。請選取下列其中一項：</p>
<ol>
<li><p>[全部]</p></li>
<li><p>內部</p></li>
<li><p>外部</p></li>
</ol></td>
</tr>
<tr class="even">
<td><p><strong>網路類型</strong></p></td>
<td><p>指出當撥打電話時，用戶端連線的網路類型。請選取下列其中一項：</p>
<ol>
<li><p>[全部]</p></li>
<li><p>有線</p></li>
<li><p>無線</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p><strong>VPN</strong></p></td>
<td><p>指出當撥打電話時，外部用戶端是否使用虛擬私人網路 (VPN) 連線。請選取下列其中一項：</p>
<ol>
<li><p>[全部]</p></li>
<li><p>VPN</p></li>
<li><p>非 VPN</p></li>
</ol></td>
</tr>
</tbody>
</table>


## 計量

下表列出伺服器效能報告提供的資訊。

### 伺服器效能報告計量：音訊通話摘要

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>名稱</th>
<th>可以排序</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>伺服器</strong></p></td>
<td><p>否</p></td>
<td><p>伺服器的名稱/IP 位址。</p></td>
</tr>
<tr class="even">
<td><p><strong>通話數</strong></p></td>
<td><p>否</p></td>
<td><p>撥打的通話總數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>通話不良百分比</strong></p></td>
<td><p>否</p></td>
<td><p>歸類為通話不良的次數。通話不良是指至少一項測量的計量超過允許的值 (例如，通話時斷斷續續聽不清楚)。</p></td>
</tr>
<tr class="even">
<td><p><strong>來回時間 (ms)</strong></p></td>
<td><p>是</p></td>
<td><p>即時傳輸通訊協定 (RTP) 封包傳送至另一個端點再返回，平均所需的時間 (毫秒)。來回時間為 100 ms (毫秒) 或更少被視為可接受的品質。</p>
<p>國際電話路由、路由設定錯誤，或者媒體伺服器超過負載時，會造成來回時間值變得相當大。來回時間長會造成雙向、即時語音交談發生問題。</p></td>
</tr>
<tr class="odd">
<td><p><strong>降低 (MOS)</strong></p></td>
<td><p>是</p></td>
<td><p>通話時經歷的平均意見分數 (MOS) 平均降級量。降級值的範圍可以從 0.0 (低) 到 5.0 (高)。值為 0.5 或更少的時間表示可接受的降級。根據歷史經驗，平均意見分數的計算方式就是讓使用者為通話品質打上 1 到 5 的分數。在 Lync Server 中，監控伺服器使用一組演算法來預告使用者如何為通話打分數。</p>
<p>網路堵塞、頻寬不足、無線網路堵塞或受到干援，或者媒體伺服器或端點超過負載，都會造成降級值變得相當高。降級太高會造成音訊扭曲或遺漏。</p></td>
</tr>
<tr class="even">
<td><p><strong>封包遺漏</strong></p></td>
<td><p>是</p></td>
<td><p>即時傳輸通訊協定 (RTP) 封包遺漏的平均速率 (當 RTP 封包 (在網際網路傳輸音訊和視訊使用的通訊協定) 無法抵達目的地時，就會發生封包遺漏)。高遺漏值通常是由下列幾種狀況造成：壅塞、頻寬不足、無線網路壅塞或干擾，或是媒體伺服器超載。封包遺漏一般會導致聲音扭曲或遺失音訊。</p></td>
</tr>
<tr class="odd">
<td><p><strong>抖動 (ms)</strong></p></td>
<td><p>是</p></td>
<td><p>RTP 封包之間抵達時間的平均抖動。(抖動是估算通話「不穩定」的方法)。高抖動值通常是由下列幾種狀況造成：壅塞，或是媒體伺服器超載，導致聲音扭曲或遺失音訊。</p></td>
</tr>
<tr class="even">
<td><p><strong>修復隱藏比率</strong></p></td>
<td><p>是</p></td>
<td><p>隱藏音訊樣本與樣本總數的平均比率 (隱藏音訊樣本是一種用於平滑音訊因一般網路封包遺漏而造成突然轉變的技術)。高比值表示因為封包遺漏或抖動而運用了大量的遺失隱藏技術，導致聲音扭曲或遺失音訊。</p></td>
</tr>
<tr class="odd">
<td><p><strong>修復延伸比率</strong></p></td>
<td><p>是</p></td>
<td><p>延伸音訊樣本與樣本總數的平均比率 (延伸音訊是指當偵測到網路封包遺漏時，為了維持通話品質而延展的音訊)。高比值表示有大量因抖動產生的樣本延伸，導致音訊聽起來像機器人或扭曲。</p></td>
</tr>
<tr class="even">
<td><p><strong>修復壓縮比率</strong></p></td>
<td><p>是</p></td>
<td><p>壓縮音訊樣本與樣本總數的平均比率 (壓縮音訊是指當偵測到網路封包遺漏時，為了維持通話品質而壓縮的音訊)。高比值表示有大量因抖動產生的樣本壓縮，導致音訊聽起來變快或扭曲。</p></td>
</tr>
</tbody>
</table>


### 伺服器效能報告計量：視訊通話摘要

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>名稱</th>
<th>可以排序這個項目嗎？</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[通話類型/端點類型]</p></td>
<td><p>否</p></td>
<td><p>當您按一下這個項目，報告會顯示該類型的通話詳細資訊。通話類型包括：</p>
<ul>
<li><p>UC 對等通話</p></li>
<li><p>UC 會議工作階段</p></li>
<li><p>PSTN 會議工作階段</p></li>
<li><p>PSTN 通話：媒體旁路</p></li>
<li><p>PSTN 通話 (非旁路)：UC Leg</p></li>
<li><p>PSTN 通話 (非旁路)：閘道 Leg</p></li>
<li><p>其他通話類型</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>通話數</strong></p></td>
<td><p>否</p></td>
<td><p>每一種通話類型的總通話數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>通話不良百分比</strong></p></td>
<td><p>否</p></td>
<td><p>歸類為通話不良的次數。通話不良是指至少一項測量的計量超過允許的值 (例如，通話時斷斷續續聽不清楚)。</p></td>
</tr>
<tr class="even">
<td><p>[通話數 (無線通話)]</p></td>
<td><p>否</p></td>
<td><p>使用無線連線的總通話數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>通話數 (VPN 通話)</strong></p></td>
<td><p>否</p></td>
<td><p>使用 VPN 連線的總通話數。</p></td>
</tr>
<tr class="even">
<td><p>[通話數 (外部通話)]</p></td>
<td><p>否</p></td>
<td><p>使用外部連線的通話數 (也就是指內部網路以外的連線)。</p></td>
</tr>
<tr class="odd">
<td><p>[平均位元速率 (Kb/秒)]</p></td>
<td><p>否</p></td>
<td><p>平均視訊位元速率 (每秒的 KB)。</p></td>
</tr>
<tr class="even">
<td><p>[低位元速率 %]</p></td>
<td><p>否</p></td>
<td><p>位元速率較低的通話百分比。</p></td>
</tr>
<tr class="odd">
<td><p>[輸出封包遺漏]</p></td>
<td><p>否</p></td>
<td><p>輸出封包的即時傳輸通訊協定 (RTP) 封包 (當 RTP 封包 (在網際網路傳輸音訊和視訊使用的通訊協定) 無法抵達目的地時，就會發生封包遺漏)。高遺漏值通常是由下列幾種狀況造成：壅塞、頻寬不足、無線網路壅塞或干擾，或是媒體伺服器超載。封包遺漏一般會導致聲音扭曲或遺失音訊。</p></td>
</tr>
<tr class="even">
<td><p>[凍結的畫面 %]</p></td>
<td><p>否</p></td>
<td><p>「凍結」的畫面百分比。在凍結的畫面中，當通話的音訊部分繼續執行時，視訊會停止播放。</p></td>
</tr>
<tr class="odd">
<td><p>[輸出平均播放速率]</p></td>
<td><p>否</p></td>
<td><p>通話期間輸出傳輸的平均播放速率。</p></td>
</tr>
<tr class="even">
<td><p>[輸入平均播放速率]</p></td>
<td><p>否</p></td>
<td><p>通話期間輸入傳輸的平均播放速率。</p></td>
</tr>
<tr class="odd">
<td><p>[輸入低播放速率 %]</p></td>
<td><p>否</p></td>
<td><p>輸入視訊的位元速率較低之通話的百分比。</p></td>
</tr>
<tr class="even">
<td><p>[用戶端健康情況 %]</p></td>
<td><p></p></td>
<td><p>表示通話期間用戶端裝置的相關健康情況。</p></td>
</tr>
</tbody>
</table>


### 伺服器效能報告計量：應用程式共用通話摘要

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>名稱</th>
<th>可以排序這個項目嗎？</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[通話類型/端點類型]</p></td>
<td><p>否</p></td>
<td><p>當您按一下這個項目，報告會顯示該類型的通話詳細資訊。通話類型包括：</p>
<ul>
<li><p>UC 對等通話</p></li>
<li><p>UC 會議工作階段</p></li>
<li><p>PSTN 會議工作階段</p></li>
<li><p>PSTN 通話：媒體旁路</p></li>
<li><p>PSTN 通話 (非旁路)：UC Leg</p></li>
<li><p>PSTN 通話 (非旁路)：閘道 Leg</p></li>
<li><p>其他通話類型</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>通話數</strong></p></td>
<td><p>否</p></td>
<td><p>每一種通話類型的總通話數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>通話不良百分比</strong></p></td>
<td><p>否</p></td>
<td><p>歸類為通話不良的次數。通話不良是指至少一項測量的計量超過允許的值 (例如，通話時斷斷續續聽不清楚)。</p></td>
</tr>
<tr class="even">
<td><p>[通話數 (無線通話)]</p></td>
<td><p>否</p></td>
<td><p>使用無線連線的總通話數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>通話數 (VPN 通話)</strong></p></td>
<td><p>否</p></td>
<td><p>使用 VPN 連線的總通話數。</p></td>
</tr>
<tr class="even">
<td><p>[通話數 (外部通話)]</p></td>
<td><p>否</p></td>
<td><p>使用外部連線的通話數 (也就是指內部網路以外的連線)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>抖動 (ms)</strong></p></td>
<td><p>否</p></td>
<td><p>RTP 封包之間抵達時間的平均抖動。(抖動是估算通話「不穩定」的方法)。高抖動值通常是由下列幾種狀況造成：壅塞，或是媒體伺服器超載，導致聲音扭曲或遺失音訊。</p></td>
</tr>
<tr class="even">
<td><p>[平均相對單向]</p></td>
<td><p>否</p></td>
<td><p>兩個媒體端點間的平均相對單向延遲。此為單一躍點延遲衡量方法。</p></td>
</tr>
<tr class="odd">
<td><p>[平均 RDP 並排顯示處理延遲]</p></td>
<td><p>否</p></td>
<td><p>在檢視工作階段期間 AS 會議伺服器中的平均 RDP 並排顯示處理延遲。這個衡量標準未涵蓋網路延遲。較高的平均反映檢視經驗中較長的延遲。超載的會議伺服器可能會遇到較高的平均延遲。</p></td>
</tr>
<tr class="even">
<td><p>[毀損之並排顯示的總百分比]</p></td>
<td><p>否</p></td>
<td><p>毀損之 RDP 並排顯示的總百分比。</p></td>
</tr>
</tbody>
</table>

