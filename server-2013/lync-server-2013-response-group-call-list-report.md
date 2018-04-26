---
title: Lync Server 2013：回應群組通話清單報告
TOCTitle: 回應群組通話清單報告
ms:assetid: a2d3e08b-511b-4507-abba-8ff71aa27c8e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg615443(v=OCS.15)
ms:contentKeyID: 49291876
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的回應群組通話清單報告

 

_**上次修改主題的時間：** 2015-03-09_

回應群組應用程式可讓 Microsoft Lync Server 2013 根據撥打的號碼以及 (選用) 來電者對於一系列問題的回應，來接聽和路由傳送電話。回應群組電話通常不會路由傳送給個別人員，而是會路由傳送給一組人員 (也稱為代理人群組)。例如，若有人撥打您的服務電話號碼， Lync Server 2013 即可自動將這通電話路由傳送給第一個方便接聽電話的服務代理人。此外， Lync Server 可能會詢問一系列問題 (「如有硬體問題，請按 1。如有軟體問題，請按 2。如有網路問題，請按 3。」)，然後根據這些問題的回答，將這通電話路由傳送給最合適的服務代理人。

「回應群組通話清單報告」代表針對指定的時間和指定的通話類型所撥打的電話集合。「回應群組使用量報告」(必須先開啟此報告，才能開啟「回應群組通話清單報告」) 可辨識下列通話類型：

  - **接收的通話** 。回應群組應用程式的所有執行個體所接收的通話數目。

  - **成功的通話**。回應群組應用程式所接起的通話總數。

  - **提供的通話** 。轉接給回應群組代理人的通話總數。

  - **接聽的通話** 。回應群組代理人實際接聽的通話總數。

  - 放棄的通話百分比。回應群組應用程式已接收，但代理人從未接聽的通話百分比。此值的計算方式為從接收的通話減掉接聽的通話，再除以接收的通話數。例如，如果您收到 10 次通話並接聽 7 次，就要從 10 減掉 7，剩下 3 次未接聽的通話。該值再除以 10，則得到的放棄通話百分比為 30%。

  - **轉接的通話** 。因為佇列逾時或佇列溢位而轉接的回應群組通話總數。

## 存取回應群組通話清單報告

唯有按一下在 [Lync Server 2013 中的回應群組使用量報告](lync-server-2013-response-group-usage-report.md)報告上找到的計量，才能存取「回應群組通話清單報告」：

  - 接收的通話

  - 成功的通話

  - 提供的通話

  - 接聽的通話

  - 轉接的通話

## 充分利用回應群組通話清單報告

「回應群組通話清單報告」可讓您將顯示的資料限制為與特定回應群組工作流程有關的通話。若要這麼做，您必須在 \[工作流程 URI\] 方塊中輸入工作流程 URI (工作流程的 SIP 位址)。但是，您必須先實際看得見 \[工作流程 URI\] 方塊，才能輸入資料。若要顯示「回應群組通話清單報告」的篩選選項，請按一下報告視窗左上方的 \[顯示/隱藏參數\] 按鈕。

請注意，如果您將滑鼠停留在 \[回應碼\] 或 \[診斷 ID\] 的上方，「回應群組通話清單」並不會顯示有關這些計量的資訊。如需詳細資訊，您可以記下 \[回應碼\] 及/或 \[診斷 ID\]，然後在 [Lync Server 2013 中的 Top Failures 報告](lync-server-2013-top-failures-report.md)中搜尋這些值。

對於以下這個問題：「哪一個個別工作流程接收最多通話？」，您可以執行下列動作：

1.  在「回應群組使用量報告」中設定想要的期間，然後按一下 \[接收的通話\] 計量，將會開啟「回應群組通話清單報告」。

2.  匯出「回應群組通話清單報告」上顯示的資料。例如，您可以將資料匯出成 Microsoft Excel 格式，然後使用 Excel 將該資料轉換為逗號分隔的檔案 (.csv)。

3.  使用 Windows PowerShell 執行分析。

例如，若將資料儲存到名為 C:\\Data\\Response\_Group\_Call\_List\_Report.csv 的檔案，即可使用下列命令傳回報告中所列的各工作流程的已接收通話總數：

    $calls = Import-Csv -Path "C:\ Data\Response_Group_Call_List_Report.csv"
    $calls | Group-Object Workflow | Select-Object Count, Name | Sort-Object Count -Descending

傳回類似以下的資訊：

    Count    Name
    -----    ----
      160    Redmond Help Desk
       47    Dublin Help Desk
       31    North America Customer Support
       16    EMEA Customer Support
       14    Employment Opportunities

## 篩選器

篩選器可以讓您傳回更精確的資料集或者以不同方法檢視傳回的資料。下表列出您可以搭配回應群組通話清單報告的篩選器。

### 回應群組通話清單報告的篩選器

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
<td><p><strong>工作流程 URI</strong></p></td>
<td><p>可讓您將傳回的資料限定在指定的回應群組工作流程。若要使用此篩選，請輸入工作流程 SIP 位址。例如：</p>
<p>sip:helpdesk@litwareinc.com</p></td>
</tr>
<tr class="even">
<td><p><strong>通話</strong></p></td>
<td><p>您可選取下列任何一種通話類型：</p>
<ul>
<li><p>接聽通話</p></li>
<li><p>成功通話</p></li>
<li><p>已提供的通話</p></li>
<li><p>已接聽的通話</p></li>
<li><p>已轉接的通話</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 計量

下表列出回應群組通話清單報告針對回應群組應用程式接聽之每通電話所提供的資訊。

### 回應群組通話清單報告計量

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
<td><p><strong>來電者</strong></p></td>
<td><p>否</p></td>
<td><p>發話者的 SIP 位址。</p></td>
</tr>
<tr class="even">
<td><p><strong>工作流程</strong></p></td>
<td><p>否</p></td>
<td><p>回應群組工作流程的 SIP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><strong>開始時間</strong></p></td>
<td><p>否</p></td>
<td><p>通話的開始日期與時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>結束時間</strong></p></td>
<td><p>否</p></td>
<td><p>通話的結束日期與時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>回應碼</strong></p></td>
<td><p>否</p></td>
<td><p>工作階段失敗時所傳送的 SIP 回應碼。</p></td>
</tr>
<tr class="even">
<td><p><strong>診斷識別碼</strong></p></td>
<td><p>否</p></td>
<td><p>附加在 SIP 訊息中的唯一識別碼 (採用 ms-diagnostics 標頭的格式)，常可以在疑難排解錯誤時提供實用的資訊。</p></td>
</tr>
</tbody>
</table>

