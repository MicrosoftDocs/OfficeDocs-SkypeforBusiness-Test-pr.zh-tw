---
title: Lync Server 2013：使用者活動報告
TOCTitle: 使用者活動報告
ms:assetid: 3aa6fef2-ea02-4f0f-93e8-fa2e0a953d79
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg558638(v=OCS.15)
ms:contentKeyID: 49290636
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的使用者活動報告

 

_**上次修改主題的時間：** 2015-03-09_

「使用者活動報告」提供了指定期間內使用者執行之對等及會議工作階段的詳細清單。不同於多數「監控報告」，「使用者活動報告」將每通通話牽繫到個別使用者。例如，對等工作階段會指定發話者 (來源使用者) 及受話者 (目標使用者) 的 SIP URI。如展開關於會議的資訊，則會顯示所有會議參與者及其在該會議中所扮演角色的清單。

「使用者活動報告」有時稱為「服務台」報告。這是因為此報告常被服務台人員用來擷取特定使用者的工作階段資訊。在 \[使用者 URI 首碼\] 方塊中輸入使用者的 SIP URI，即可篩選個別使用者所接收或發出的通話。

如果您這麼做，「使用者活動報告」會針對 SIP URI 以指定字串開頭的使用者傳回資訊。舉例來說，如果在 \[URI\] 方塊中輸入 **ken** ，則「使用者活動報告」會找到 **Ken** .Myer@litwareinc.com，也會找到下列使用者：

  - **ken** azi@litwareinc.com

  - **ken** burg@litwareinc.com

  - **Ken** .Sanchez@litwareinc.com

  - **Ken** nedy@litwareinc.com

如要確保只傳回 Ken Myer 的資訊，請在搜尋方塊中輸入他的完整 URI (Ken.Myer@litwareinc.com)，或至少輸入足以辨識 Ken 的 URI 內容，以區隔 Ken 和組織中的其他使用者。例如：

Ken.my

## 存取使用者活動報告

從「監控報告」首頁可存取「使用者活動報告」。按一下 [Lync Server 2013 中的 IP 電話清查報告](lync-server-2013-ip-phone-inventory-report.md)上的 \[使用者 URI\] 計量，也可存取「使用者活動報告」。從「使用者活動報告」中，按一下 \[會議 URI\] (針對會議) 會移至「會議詳細資料報告」。同樣地，按一下對等通話的 \[詳細資料\] 計量會移至 [Lync Server 2013 中的對等工作階段詳細資料報告](lync-server-2013-peer-to-peer-session-detail-report.md)。

## 發揮使用者活動報告的最大效用

雖然「使用者活動報告」中有許多有用的資訊，但是有時候很難找到所需的資訊。例如，在指定期間內組織中發生的所有使用者活動全都包含在「使用者活動報告」中；這表示有關哪些確實以某些方式使用 Microsoft Lync Server 2013 之使用者的資訊，埋藏在報告之中。

<table>
<thead>
<tr class="header">
<th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>技術上而言，某些使用者活動有可能沒被記錄下來：雖然 Lync Server 盡力保存所有通話的資訊，關於某通通話的資訊仍有可能沒寫入資料庫。 Lync Server 設計為可高度精確但不一定完整地保存 Lync Server 2013 使用方式的資訊。(因為無法保證記錄所有通話，所以不應使用 Lync Server 監控作為帳務系統。)<br />
第二，「監控報告」中的報告最多僅可顯示 1,000 筆記錄。所以，取決於使用者活動的多寡及工作期間，您的查詢可能不會傳回資料庫中所有實際儲存的資料。</td>
</tr>
</tbody>
</table>


  - 在此期間內哪些使用者確實使用系統？

  - 在此期間內我的哪些使用者最為活躍？

  - 通話最多的使用者也是參與最多立即訊息工作階段的使用者嗎？

如果您需要回答此類問題，可以將「監控報告」擷取的資料匯出到 Excel 試算表。然後使用該試算表及 (或) 逗點分隔值檔案，以「使用者活動報告」無法做到的方式來分析資料。例如，假設您已將報告資料匯出到 Excel，再儲存為逗點分隔值檔案。屆時使用如下的命令，即可將資料從 .CSV 檔案匯入到 Windows PowerShell：

    $x = Import-Csv -Path "C:\Data\User_Activity_Report.csv"

匯入資料後，就可以使用簡單的 Windows PowerShell 命令來幫助您回答問題。例如，以下命令會傳回至少在一個工作階段中擔任「來源使用者」的唯一使用者清單：

    $x | Group-Object "From user" | Select Name | Sort-Object Name

換句話說：

    Name
    ----
    David.Ahs@litwareinc.com
    Gilead.Amosnino@litwareinc.com
    Henrik.Jensen@litwareinc.com
    Ken.Myer@litwareinc.com
    Pilar.Ackerman@litwareinc.com

此命令會列出唯一使用者 (根據他們參與的工作階段總數)：

    $x | Group-Object "From user" | Select Count, Name | Sort-Object Count -Descending

這會傳回如下的資訊：

    Count    Name
    -----    ----
      523    Ken.Myer@litwareinc.com
       63    David.Ahs@litwareinc.com
       29    Pilar.Ackerman@litwareinc.com
       17    Gilead.Amosnino@litwareinc.com
       10    Henrik.Jensen@litwareinc.com

此命令會將報告的工作階段限制為包含音訊形式的工作階段：

    $x | Where-Object {$_.Modalities -match "audio"} | Group-Object "From user" | Select Count, Name | Sort-Object Count -Descending

如果將滑鼠停留在報告上顯示的任何 \[診斷識別碼\] 上，說明該識別碼的工具提示就會顯示。

## 篩選器

篩選可以讓您傳回更精確的資料集或者以不同方法檢視傳回的資料。例如，使用者活動報告可讓您依據活動類型之類的項目 (也就是，對等工作階段或會議工作階段)，或是依使用者的 SIP 位址 (可讓您檢視一位使用者的活動)，篩選傳回的資料。您也可以選擇資料的分組方式。在這種情況下，使用量會按照小時、日、星期或月加以分組。

下表列出您可以用於使用者活動報告的篩選。

### 使用者活動報告篩選

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
<p>7/17/2012 1:00 PM</p>
<p>如果您未輸入開始時間，報告會自動從指定日期凌晨 12 點開始。若要按照日期檢視資料，只要輸入日期即可：</p>
<p>7/17/2012</p>
<p>若要按星期或月份查看，請輸入當週或該月您想查看的日期 (您不必輸入當週或該月的第一天)：</p>
<p>7/13/2012</p>
<p>星期永遠是從星期日開始星期六結束。</p></td>
</tr>
<tr class="even">
<td><p><strong>到</strong></p></td>
<td><p>時間範圍的結束日期/時間。若要按照小時檢視資料，請輸入開始日期和時間，如下所示：</p>
<p>7/17/2012 1:00 PM</p>
<p>如果您未輸入結束時間，報告會自動在指定日期凌晨 12 點結束。若要按照日期檢視資料，只要輸入日期即可：</p>
<p>7/17/2012</p>
<p>若要按星期或月份查看，請輸入當週或該月您想查看的日期 (您不必輸入當週或該月的第一天)：</p>
<p>7/13/2012</p>
<p>星期永遠是從星期日開始星期六結束。</p></td>
</tr>
<tr class="odd">
<td><p><strong>活動類型</strong></p></td>
<td><p>活動的類型。請選取下列其中一項：</p>
<ul>
<li><p>[全部]</p></li>
<li><p>對等</p></li>
<li><p>會議</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>形式</strong></p></td>
<td><p>您可以使用的 [形式] 取決於選取的 [活動類型]。如果 [活動類型]為 [對等]，您可以選取 [IM]；[檔案傳輸]；[應用程式共用]；[語音] 或 [視訊] 作為形式。</p>
<p>如果 [活動類型] 為 [會議]，您可以選取 [IM 電話會議]；[Web 會議]；[應用程式共用]；[語音/視訊會議]；或 [電話會議]。</p></td>
</tr>
<tr class="odd">
<td><p><strong>工作階段類別</strong></p></td>
<td><p>指出有疑問的活動為成功或失敗。請選取下列其中一項：</p>
<ul>
<li><p>[全部]</p></li>
<li><p>成功</p></li>
<li><p>預期的失敗</p></li>
<li><p>未預期的失敗</p></li>
</ul>
<p>「預期的失敗」是指預期會發生的失敗；例如，當使用者將其狀態設為「勿打擾」時，即應預期所有撥話給該使用者的通話皆會失敗。「未預期的失敗」是指起因於系統不健全的失敗。例如，當發話者處於保留狀態時，不應掛斷通話。當發生此狀況時，會將其標幟為未預期的失敗。</p></td>
</tr>
<tr class="even">
<td><p><strong>使用者 URI 字首</strong></p></td>
<td><p>使用者的 SIP 位址。如果只要檢視使用者 Ken Myer 的記錄，則需要輸入 Ken Myer 的 SIP 位址。例如：</p>
<p>sip:kenmyer@litwareinc.com</p></td>
</tr>
</tbody>
</table>


## 對等工作階段的計量

下表列出使用者活動報告中提供的對等工作階段資訊 (也就是只有兩個參與者的工作階段)。

### 對等工作階段的計量

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
<td><p><strong>詳細資料</strong></p></td>
<td><p>否</p></td>
<td><p>當您按一下此項目，報告即顯示所選取之工作階段的對等工作階段詳細資料報告。</p></td>
</tr>
<tr class="even">
<td><p><strong>來源使用者</strong></p></td>
<td><p>是</p></td>
<td><p>啟動對等工作階段之使用者的 SIP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><strong>目標使用者</strong></p></td>
<td><p>是</p></td>
<td><p>參與對等工作階段之使用者的 SIP 位址。</p></td>
</tr>
<tr class="even">
<td><p><strong>形式</strong></p></td>
<td><p>是</p></td>
<td><p>工作階段中所使用的通訊類型。例如 IM、音訊或檔案傳輸。</p></td>
</tr>
<tr class="odd">
<td><p><strong>邀請時間</strong></p></td>
<td><p>是</p></td>
<td><p>初始邀請加入對等工作階段時，傳送邀請的日期和時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>回應時間</strong></p></td>
<td><p>是</p></td>
<td><p>「受邀」的使用者接受工作階段邀請的日期和時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>結束時間</strong></p></td>
<td><p>是</p></td>
<td><p>對等工作階段結束的日期和時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>診斷識別碼</strong></p></td>
<td><p>是</p></td>
<td><p>附加在 SIP 訊息中的唯一識別碼 (採用 ms-diagnostics 標頭的格式)，常可以在疑難排解錯誤時提供實用的資訊。診斷標頭為選用 (也可能有 SIP 工作階段不包含這些標頭)。只有發生特定問題的工作階段才會回報診斷識別碼。</p></td>
</tr>
</tbody>
</table>


## 會議工作階段的計量

下表列出使用者活動報告中提供的會議工作階段資訊 (也就是有三個以上參與者的工作階段)。

### 會議工作階段的計量

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
<td><p><strong>會議 URI</strong></p></td>
<td><p>是</p></td>
<td><p>唯一會議識別碼。當您按一下此項目，報告即顯示所選取之工作階段的會議詳細資料報告。當您展開此項目，報告會顯示會議參與者的相關資訊。如需詳細資訊，請參閱本主題稍後的＜會議參與者的計量＞一節。</p></td>
</tr>
<tr class="even">
<td><p><strong>召集人</strong></p></td>
<td><p>是</p></td>
<td><p>召開會議之使用者的 SIP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><strong>集區</strong></p></td>
<td><p>是</p></td>
<td><p>會議中使用的 Edge Server 名稱 (若有的話)。</p></td>
</tr>
<tr class="even">
<td><p><strong>開始時間</strong></p></td>
<td><p>是</p></td>
<td><p>會議開始的日期與時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>結束時間</strong></p></td>
<td><p>是</p></td>
<td><p>會議結束的日期與時間。</p></td>
</tr>
</tbody>
</table>


## 會議參與者的計量

下表列出使用者活動報告中為會議每位參與者提供的資訊。

### 會議參與者的計量

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
<td><p><strong>角色</strong></p></td>
<td><p>否</p></td>
<td><p>使用者的會議角色 (例如簡報者)。</p></td>
</tr>
<tr class="even">
<td><p><strong>參與者</strong></p></td>
<td><p>否</p></td>
<td><p>使用者的 SIP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><strong>連接性</strong></p></td>
<td><p>否</p></td>
<td><p>網路連線類型。例如，「來自內部」代表內部連線，或是「來自 PSTN」代表撥入使用者。</p></td>
</tr>
<tr class="even">
<td><p><strong>加入時間</strong></p></td>
<td><p>否</p></td>
<td><p>使用者加入會議的日期與時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>離開時間</strong></p></td>
<td><p>否</p></td>
<td><p>使用者離開會議的日期與時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>診斷識別碼</strong></p></td>
<td><p>否</p></td>
<td><p>附加在 SIP 訊息中的唯一識別碼 (採用 ms-diagnostics 標頭的格式)，常可以在疑難排解錯誤時提供實用的資訊。診斷標頭為選用 (也可能有 SIP 工作階段不包含這些標頭)。只有發生特定問題的工作階段才會回報診斷識別碼。</p></td>
</tr>
</tbody>
</table>

