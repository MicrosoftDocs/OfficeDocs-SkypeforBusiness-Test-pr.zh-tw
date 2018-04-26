---
title: Lync Server 2013：通話許可控制報告
TOCTitle: 通話許可控制報告
ms:assetid: ea4b0c9f-7f93-4b8a-b901-01e1636c44fb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg615043(v=OCS.15)
ms:contentKeyID: 49292698
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的通話許可控制報告

 

_**上次修改主題的時間：** 2015-03-09_

通話許可控制報告提供的相關資訊，包含通話許可控制在符合現行限制的情況下所執行的對等與會議工作階段。通話許可控制 ( Microsoft Lync Server 2010 已介紹過) 讓系統管理員能夠根據頻寬限制允許 (或不允許) 通訊工作階段。例如系統管理員可建立原則，限制語音與視訊通話的頻寬用量。若達到該頻寬限制，就不能再進行新的語音或視訊通話，直到目前的某個通話結束，釋出所需的網路資源為止。

## 存取通話許可控制報告

您可從監控報告首頁存取通話許可控制報告。您可從通話許可控制報告再向下切入至下列報告的其中一個：

  - 會議詳細資料報告：要存取此報告，請按一下會議工作階段中的詳細資料計量。

  - 對等工作階段詳細資料報告：要存取本報告，請按一下對等工作階段的詳細資料計量。

## 善用通話許可控制報告

要取得因頻寬不足導致通失敗的清單，請從通話類別下拉式清單中選擇因通話許可控制遭拒的通話。多數回電的可能診斷識別碼為 5：

頻寬不足，無法建立工作階段。請嘗試 PSTN 重新路由。

這代表通話許可控制限制不讓使用者在 VoIP 網路上撥打電話。

## 篩選器

篩選器可以讓您傳回更精確的資料集，或是以不同方法檢視傳回的資料。例如，您可利用「通話許可控制報告」依據啟動通話之使用者或依據接到通話的使用者，篩選通話。您也可以選擇資料的分組方式。在這種情況下，通話會按照小時、日、星期或月而加以分組。

下表列出您可以搭配通話許可控制報告的篩選器。

### 通話許可控制服務報告篩選器

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
<p>2012/7/17 下午 1:00</p>
<p>如果您未輸入開始時間，報告會自動從指定日期凌晨 12 點開始。若要按照日期檢視資料，只要輸入日期即可：</p>
<p>2012/7/17</p>
<p>若要按星期或月份查看，請輸入當週或該月您想查看的日期 (您不必輸入當週或該月的第一天)：</p>
<p>13.07.12</p>
<p>星期永遠是從星期日開始星期六結束。</p></td>
</tr>
<tr class="even">
<td><p><strong>到</strong></p></td>
<td><p>時間範圍的結束日期/時間。若要按照小時檢視資料，請輸入開始日期和時間，如下所示：</p>
<p>2012/7/17 下午 1:00</p>
<p>如果您未輸入結束時間，報告會自動在指定日期凌晨 12 點結束。若要按照日期檢視資料，只要輸入日期即可：</p>
<p>2012/7/17</p>
<p>若要按星期或月份查看，請輸入當週或該月您想查看的日期 (您不必輸入當週或該月的第一天)：</p>
<p>13.07.12</p>
<p>星期永遠是從星期日開始星期六結束。</p></td>
</tr>
<tr class="odd">
<td><p><strong>集區</strong></p></td>
<td><p>登錄器集區或 Edge Server 的完整網域名稱 (FQDN)。您可以選取個別的集區，或是按一下 [全部] 檢視所有集區的資料。此下拉式清單會自動將資料庫內的資料填入。</p></td>
</tr>
<tr class="even">
<td><p><strong>活動類型</strong></p></td>
<td><p>活動的類型。請選取下列其中一項活動：</p>
<ul>
<li><p>[全部]</p></li>
<li><p>對等</p></li>
<li><p>會議</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>通話類別</strong></p></td>
<td><p>指出為該通話使用 CAC 的原因。請選取下列其中一項：</p>
<ul>
<li><p>[全部]</p></li>
<li><p>因通話許可控制而拒絕通話</p></li>
<li><p>因通話許可控制而透過 PSTN 重新路由通話</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 對等工作階段的計量

下表列出對等工作階段 (也就是只有兩位參與者的工作階段) 的通話許可控制報告內所提供的資訊。

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
<td><p>當您按一下此項目時，報告會顯示所指定之工作階段的對等工作階段詳細資料報告。</p></td>
</tr>
<tr class="even">
<td><p><strong>來源使用者</strong></p></td>
<td><p>是</p></td>
<td><p>啟動工作階段之使用者的 SIP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><strong>目標使用者</strong></p></td>
<td><p>是</p></td>
<td><p>被邀請加入工作階段之使用者的 SIP 位址。</p></td>
</tr>
<tr class="even">
<td><p><strong>形式</strong></p></td>
<td><p>是</p></td>
<td><p>工作階段期間所使用的溝通形式 (如音訊或視訊)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>邀請時間</strong></p></td>
<td><p>是</p></td>
<td><p>初始工作階段邀請傳送至「從」使用者的日期與時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>回應時間</strong></p></td>
<td><p>是</p></td>
<td><p>收到接受邀請的日期與時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>結束時間</strong></p></td>
<td><p>是</p></td>
<td><p>工作階段結束的日期與時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>診斷識別碼</strong></p></td>
<td><p>是</p></td>
<td><p>附加在 SIP 訊息中的唯一識別碼 (採用 ms-diagnostics 標頭的格式)，常可以在疑難排解錯誤時提供實用的資訊。診斷標頭為選用 (也可能有 SIP 工作階段不包含這些標頭)。只有發生特定問題的工作階段才會回報診斷識別碼。</p></td>
</tr>
</tbody>
</table>


## 會議工作階段的計量

下表列出會議工作階段 (也就是有三位或更多位參與者的工作階段) 的通話許可控制報告內所提供的資訊。

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
<td><p>會議的唯一識別碼。當您按一下此項目時，報告會顯示各個會議參與者。</p></td>
</tr>
<tr class="even">
<td><p><strong>召集人</strong></p></td>
<td><p>是</p></td>
<td><p>召開會議之使用者的 SIP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><strong>集區</strong></p></td>
<td><p>是</p></td>
<td><p>會議所使用的 Edge Server。</p></td>
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


## 個別會議參與者的計量

下表列出個別參與者的通話許可控制報告內所提供的資訊。

### 個別會議參與者的計量

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
<td><p>會議參與者所扮演的角色 (例如，簡報者)。</p></td>
</tr>
<tr class="even">
<td><p><strong>參與者</strong></p></td>
<td><p>否</p></td>
<td><p>會議參與者的 SIP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><strong>連接性</strong></p></td>
<td><p>否</p></td>
<td><p>參與者的網路連線 (一般來說是從內部或從外部)。</p></td>
</tr>
<tr class="even">
<td><p><strong>形式</strong></p></td>
<td><p>否</p></td>
<td><p>會議類型 (例如，A/V 會議)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>加入時間</strong></p></td>
<td><p>否</p></td>
<td><p>參與者加入會議的日期與時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>離開時間</strong></p></td>
<td><p>否</p></td>
<td><p>參與者離開會議的日期與時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>診斷識別碼</strong></p></td>
<td><p>否</p></td>
<td><p>附加在 SIP 訊息中的唯一識別碼 (採用 ms-diagnostics 標頭的格式)，常可以在疑難排解錯誤時提供實用的資訊。診斷標頭為選用 (也可能有 SIP 工作階段不包含這些標頭)。只有發生特定問題的工作階段才會回報診斷識別碼。</p></td>
</tr>
</tbody>
</table>

