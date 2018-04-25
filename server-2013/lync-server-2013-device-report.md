---
title: Lync Server 2013：裝置報告
TOCTitle: 裝置報告
ms:assetid: f42e4d60-699b-4870-8bb5-13b51bb6eb2b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg615049(v=OCS.15)
ms:contentKeyID: 49292806
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的裝置報告

 

_**上次修改主題的時間：** 2015-03-09_

「裝置報告」的標題最好使用「麥克風與喇叭報告」；因為「裝置報告」會擷取與通話相關，且歸類為通話中所用麥克風與喇叭的計量 (例如通話不良百分比、回音及語音交換時間)。如果您想了解 IP 電話 (亦通稱為「裝置」)，請改用 [Lync Server 2013 中的 IP 電話清查報告](lync-server-2013-ip-phone-inventory-report.md)。

對於判斷特定裝置是否音量較高或通話品質較不良的系統管理員而言，「裝置報告」非常實用。因此也可能會影響您購買新裝置或取代現有裝置時所做的任何決定。

根據預設，「裝置報告」中顯示的資訊也是根據通話中使用的麥克風 (擷取裝置) 與喇叭/耳機 (轉換裝置)。例如，假設有幾位使用者使用下列擷取裝置與轉換裝置：

  - 擷取裝置 -- 麥克風 (SoundMAX Integrated Digital HD Audio)

  - 轉換裝置 -- 耳麥式耳機 (Microsoft LifeChat LX-3000)

如果使用者總共來電 254 通，您會在報告中看到這樣的記錄：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>擷取裝置</th>
<th>轉換裝置</th>
<th>通話數</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>麥克風 (SoundMAX Integrated Digital HD Audio)</p></td>
<td><p>耳麥式耳機 (Microsoft LifeChat LX-3000)</p></td>
<td><p>254</p></td>
</tr>
</tbody>
</table>


現在，假設有幾位使用者使用相同的擷取裝置，但轉換裝置不同。在這個情況下，您會在報告中看到第二行記錄，就是捕捉裝置與轉換裝置的特殊組合：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>擷取裝置</th>
<th>轉換裝置</th>
<th>通話數</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>麥克風 (SoundMAX Integrated Digital HD Audio)</p></td>
<td><p>耳麥式耳機 (Microsoft LifeChat LX-3000)</p></td>
<td><p>254</p></td>
</tr>
<tr class="even">
<td><p>麥克風 (SoundMAX Integrated Digital HD Audio)</p></td>
<td><p>喇叭 (SoundMAX Integrated Digital HD Audio)</p></td>
<td><p>319</p></td>
</tr>
</tbody>
</table>


如果您比較想看到指定裝置量的總計 (例如 SoundMAX 擷取裝置量，無論使用的轉換裝置為何)，請從 \[裝置類型\] 下拉式清單中選取適當選項 (\[擷取裝置\] 或 \[轉換裝置\])。如果在此範例中您選取 \[擷取裝置\]，結果看起來如下：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>擷取裝置</th>
<th>通話數</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>麥克風 (SoundMAX Integrated Digital HD Audio)</p></td>
<td><p>573</p></td>
</tr>
</tbody>
</table>


## 存取裝置報告

通常是從「監視報告」首頁存取「裝置報告」。但是，如果您正在檢視 [Lync Server 2013 中的詳細通話報告](lync-server-2013-call-detail-report.md)，也可按一下任一個下列計量，向下切入至「裝置報告」找特定裝置。

  - 擷取裝置

  - 轉換裝置

您可按一下以下任一個計量，從「裝置報告」中向下切入至 [Lync Server 2013 中的通話清單報告](lync-server-2013-call-list-report.md)：

  - 通話數

  - 通話不良百分比

## 善用裝置報告

在「裝置報告」中，裝置名稱十分詳細；例如，假設您有下列擷取裝置：

  - Aastra 3002 麥克風 (2- Aastra 3002)

  - Aastra 3002 麥克風 (3- Aastra 3002)

  - Aastra 3002 麥克風 (Aastra 3002)

  - Aastra 6725ip

  - Aastra 6725ip 麥克風 (10- Aastra 6725ip)

  - Aastra 6725ip 麥克風 (10- Aastra 6725ip)-V0

  - Aastra 6725ip 麥克風 (2- Aastra 6725ip)

  - Aastra 6725ip 麥克風 (3- Aastra 6725ip)

  - Aastra 6725ip 麥克風 (4- Aastra 6725ip)

  - Aastra 6725ip 麥克風 (5- Aastra 6725ip)

  - Aastra 6725ip 麥克風 (6- Aastra 6725ip)

  - Aastra 6725ip 麥克風 (7- Aastra 6725ip)

  - Aastra 6725ip 麥克風 (9- Aastra 6725ip)

  - Aastra 6725ip 麥克風 (9- Aastra 6725ip)-V0

  - Aastra 6725ip 麥克風 (Aastra 6725ip)

  - Aastra 6725ip 麥克風 (Aastra 6725ip)-V0

  - Aastra 6725ip 麥克風 (USB 音訊裝置)

  - Aastra 6725ip 麥克風 (USB 音訊裝置)-V0

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>請記住，如果執行的是 Lync Server 2013 的本地化版本，擷取裝置名稱可能會不同。美式英文中使用的名稱為「Aastra 6725ip Microphone (Aastra 6725ip)-V0」，法文或西班牙文的名稱可能不一樣。</td>
</tr>
</tbody>
</table>


通常您會想知道如此詳細；但有時候，您可能只想知道有幾則通話是使用 Aastra 麥克風，無論型號為何。取得此資訊的一種方法，就是將「裝置報告」的資料匯出至 Microsoft Excel，然後將資料儲存為逗號分隔值檔案 (例如 C:\\Data\\Devices\_Report.csv)。可使用一組與將 .CSV 檔案匯入至 Windows PowerShell 相似的命令，回報使用 Aastra 擷取裝置的通話總數：

    $devices = Import-Csv "C:\Data\Device_Report.csv
    $sum = $devices | Where-Object {$_."Capture device" -match "Aastra"}
    $sum | foreach-object {[Int]$x = [Int]$x + [Int]$_."call volume"}
    $x

這會傳回代表使用 Aastra 擷取裝置之通話總數的單一值。例如：

    384

## 篩選器

篩選器可以讓您傳回更精確的資料集或者以不同方法檢視傳回的資料。例如，您可利用「裝置報告」篩選像是通話類型等項目 (也就是說，撥打用戶端通話)、會議通話，或是公用交換電話網路 (PSTN) 通話。您也可以選擇資料的分組方式。在這種情況下，裝置會按照小時、日、星期或月而加以分組。

下表列出您可以搭配裝置報告的篩選器。

### 裝置報告篩選器

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
<td><p><strong>語音交換原因</strong></p></td>
<td><p>通話必須切換至半雙工模式以防止回音的原因。在半雙工模式中，同一時間通訊只能單向傳送，類似於使用對講機時使用者輪流通訊。請選取下列其中一項：</p>
<dl>
<dt><span></span></dt>
<dd><p>[全部]</p>
</dd>
<dt><span></span></dt>
<dd><p>無</p>
</dd>
<dt><span></span></dt>
<dd><p>損毀的時間戳記</p>
</dd>
<dt><span></span></dt>
<dd><p>回音</p>
</dd>
<dt><span></span></dt>
<dd><p>DNLP (動態非線性處理器)</p>
</dd>
<dt><span></span></dt>
<dd><p>低複雜性</p>
</dd>
<dt><span></span></dt>
<dd><p>不良的裝置狀態</p>
</dd>
<dt><span></span></dt>
<dd><p>AEC 後的回音 (柔和式迴音效果取消功能)</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td><p><strong>回音的原因</strong></p></td>
<td><p>在通話中偵測到超出可接受之程度的回音原因。(在電信中，回音是聲音的反射，當您對著水井的底部大叫時會聽到相同的現象)。請選取下列其中一項：</p>
<dl>
<dt><span></span></dt>
<dd><p>[全部]</p>
</dd>
<dt><span></span></dt>
<dd><p>無</p>
</dd>
<dt><span></span></dt>
<dd><p>損毀的時間戳記</p>
</dd>
<dt><span></span></dt>
<dd><p>AEC 後的回音 (柔和式迴音效果取消功能)</p>
</dd>
<dt><span></span></dt>
<dd><p>ANLP (調適式非線性處理器)</p>
</dd>
<dt><span></span></dt>
<dd><p>DNLP (動態非線性處理器)</p>
</dd>
<dt><span></span></dt>
<dd><p>麥克風雜音</p>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td><p><strong>通話類型</strong></p></td>
<td><p>指出所進行的通話類型。請選取下列其中一項：</p>
<dl>
<dt><span></span></dt>
<dd><p>[全部]</p>
</dd>
<dt><span></span></dt>
<dd><p>用戶端通話</p>
</dd>
<dt><span></span></dt>
<dd><p>PSTN 通話</p>
</dd>
<dt><span></span></dt>
<dd><p>會議通話</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td><p><strong>存取類型</strong></p></td>
<td><p>指出撥打電腦時，用戶端是否登入內部網路或外部網路。請選取下列其中一項：</p>
<dl>
<dt><span></span></dt>
<dd><p>[全部]</p>
</dd>
<dt><span></span></dt>
<dd><p>內部</p>
</dd>
<dt><span></span></dt>
<dd><p>外部</p>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td><p><strong>網路類型</strong></p></td>
<td><p>指出當撥打電話時，用戶端連線的網路類型。請選取下列其中一項：</p>
<dl>
<dt><span></span></dt>
<dd><p>[全部]</p>
</dd>
<dt><span></span></dt>
<dd><p>有線</p>
</dd>
<dt><span></span></dt>
<dd><p>無線</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td><p><strong>VPN</strong></p></td>
<td><p>指出當撥打電話時，外部用戶端是否使用虛擬私人網路 (VPN) 連線。請選取下列其中一項：</p>
<dl>
<dt><span></span></dt>
<dd><p>[全部]</p>
</dd>
<dt><span></span></dt>
<dd><p>VPN</p>
</dd>
<dt><span></span></dt>
<dd><p>非 VPN</p>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td><p><strong>裝置類型</strong></p></td>
<td><p>指出裝置類型。請選取下列其中一項：</p>
<dl>
<dt><span></span></dt>
<dd><p>擷取裝置</p>
</dd>
<dt><span></span></dt>
<dd><p>轉換裝置</p>
</dd>
<dt><span></span></dt>
<dd><p>成對的擷取/轉換裝置</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td><p><strong>裝置名稱</strong></p></td>
<td><p>擷取/轉換裝置的名稱。您可以完整的裝置名或裝置名稱的任一部分。例如，若要尋找裝置 Microphone (Microsoft LifeCam VX-1000.)，您可以如下輸入完整的裝置名稱：</p>
<p>Microphone (Microsoft LifeCam VX-1000.)</p>
<p>或者，您可以只輸入部分名稱。例如：</p>
<p>LifeCam</p>
<p>請注意，先前的篩選器會傳回在名稱的任意處包含字串 &quot;LifeCam&quot; 的所有裝置。</p></td>
</tr>
</tbody>
</table>


## 計量

下表列出裝置報告中所提供的資訊。

### 裝置報告計量

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
<td><p><strong>擷取裝置</strong></p></td>
<td><p>是</p></td>
<td><p>傳輸音訊的裝置 (例如，麥克風或網路攝影機)。</p></td>
</tr>
<tr class="even">
<td><p><strong>轉換裝置</strong></p></td>
<td><p>是</p></td>
<td><p>接收音訊的裝置 (例如，耳機或喇叭)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>通話數</strong></p></td>
<td><p>是</p></td>
<td><p>進行的通話總數。</p></td>
</tr>
<tr class="even">
<td><p><strong>通話不良百分比</strong></p></td>
<td><p>是</p></td>
<td><p>歸類為品質不良的通話百分比。通話不良是指至少一項計算的次數超過允許的值 (例如，通話時斷斷續續聽不清楚)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>單獨使用者</strong></p></td>
<td><p>是</p></td>
<td><p>使用該裝置的單獨使用者。若某位使用者使用了裝置 13 次，仍會將其算為一個單獨的使用者，和只使用了一次該裝置的使用者一樣。</p></td>
</tr>
<tr class="even">
<td><p><strong>語音交換時間的比率</strong></p></td>
<td><p>是</p></td>
<td><p>通話必須在半雙工模式中進行以防止回音的百分比。在半雙工模式中，同一時間通訊只能單向傳送，類似於使用對講機時使用者輪流通訊。</p></td>
</tr>
<tr class="odd">
<td><p><strong>麥克風未運作的比率</strong></p></td>
<td><p>是</p></td>
<td><p>擷取裝置的運作不是可接受程度的通話百分比。比較高的值表示通話的品質問題主要是因為擷取裝置的運作不如預期。</p></td>
</tr>
<tr class="even">
<td><p><strong>喇叭未運作的比率</strong></p></td>
<td><p>是</p></td>
<td><p>轉換裝置的運作不是可接受程度的通話百分比。比較高的值表示通話的品質問題主要是因為轉換裝置的運作不如預期。</p></td>
</tr>
<tr class="odd">
<td><p><strong>發生語音交換的通話 (%)</strong></p></td>
<td><p>是</p></td>
<td><p>必須在半雙工模式中進行的總通話數百分比。在半雙工模式中，同一時間通訊只能單向傳送，類似於使用對講機時使用者輪流通訊。</p></td>
</tr>
<tr class="even">
<td><p><strong>麥克風回音 (%)</strong></p></td>
<td><p>是</p></td>
<td><p>麥克風擷取資料流時偵測到回音的時間百分比。通常，耳機或話筒的值較低，而免持通話器或獨立喇叭的值較高。若是支援內建原音回音取消的裝置，較高的值表示回音流失。針對其他裝置，此計量不應用來評估裝置品質。</p></td>
</tr>
<tr class="odd">
<td><p><strong>回音傳送 (%)</strong></p></td>
<td><p>是</p></td>
<td><p>傳輸至其使用者的回音百分比。</p></td>
</tr>
<tr class="even">
<td><p><strong>有回音的通話 (%)</strong></p></td>
<td><p>是</p></td>
<td><p>回音超出可接受程度的總通話百分比。</p>
<p></p></td>
</tr>
</tbody>
</table>

