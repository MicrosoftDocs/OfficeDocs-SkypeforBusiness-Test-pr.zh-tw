---
title: 會議詳細資料報告
TOCTitle: 會議詳細資料報告
ms:assetid: 1d61cd81-dcfe-40b4-9a41-a73b038bc216
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204728(v=OCS.15)
ms:contentKeyID: 49290273
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 會議詳細資料報告

 

_**上次修改主題的時間：** 2015-03-09_

「會議詳細資料報告」可提供參與會議之使用者的詳細資訊。例如，您可以查看使用者加入會議的日期和時間、使用者離開會議的日期和時間，以及用來將使用者與會議連線的端點使用者代理程式之類的資訊。您也可以查看使用者在每個會議中的角色 (例如，簡報者或是出席者)。更重要的是，您可以更快速地查看哪些使用者已順利加入並完成會議，而哪些使用者無法順利加入並完成會議。

## 存取會議詳細資料報告

您可從下列報告來存取會議詳細資料報告：

  - [Lync Server 2013 中的通話許可控制報告](lync-server-2013-call-admission-control-report.md) (按一下會議的 \[詳細資料\] 計量)

  - [Lync Server 2013 中的失敗清單報告](lync-server-2013-failure-list-report.md) (按一下 \[會議\] 計量)

  - [Lync Server 2013 中的使用者活動報告](lync-server-2013-user-activity-report.md) (按一下 \[會議 URI\] 計量)

您還可從會議詳細資料報告中，按一下 \[診斷報告\] (\[詳細資料\]) 計量，來存取[Lync Server 2013 中的診斷報告](lync-server-2013-diagnostic-report.md)。

## 篩選器

無。您無法篩選會議詳細資料報告。

## 計量

下表列出會議詳細資料報告的「會議資訊」區段中所提供的資訊。

### 會議資訊計量

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
<td><p></p></td>
<td><p>指派給會議的 URI。例如：</p>
<p>sip:kmyer@litwareinc.com;gruu;opaque=app:conf:focus:id:drg2y8v4</p></td>
</tr>
<tr class="even">
<td><p><strong>集區 FQDN</strong></p></td>
<td><p></p></td>
<td><p>工作階段所涉及的登錄器集區或 Edge Server 的完整網域名稱。</p></td>
</tr>
<tr class="odd">
<td><p><strong>開始時間</strong></p></td>
<td><p></p></td>
<td><p>會議開始的日期與時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>召集人</strong></p></td>
<td><p></p></td>
<td><p>召開會議之使用者的 SIP 位址。</p></td>
</tr>
<tr class="odd">
<td><p><strong>結束時間</strong></p></td>
<td><p></p></td>
<td><p>會議結束的日期與時間。</p></td>
</tr>
</tbody>
</table>


下表列出會議詳細資料報告的「會議參與區段」中所提供的資訊。

### 會議參與計量

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
<td><p><strong>使用者</strong></p></td>
<td><p></p></td>
<td><p>參與會議之使用者的 SIP 位址。</p></td>
</tr>
<tr class="even">
<td><p><strong>角色</strong></p></td>
<td><p></p></td>
<td><p>會議參與者所扮演的角色 (例如，簡報者)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>連線</strong></p></td>
<td><p></p></td>
<td><p>參與者的網路連線 (一般來說是從內部或從外部)。</p></td>
</tr>
<tr class="even">
<td><p>加入時間</p></td>
<td><p></p></td>
<td><p>參與者加入會議的日期與時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>離開時間</strong></p></td>
<td><p></p></td>
<td><p>參與者離開會議的日期與時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>使用者代理程式</strong></p></td>
<td><p></p></td>
<td><p>參與者端點所使用的軟體識別碼。</p></td>
</tr>
<tr class="odd">
<td><p><strong>診斷報告</strong></p></td>
<td><p></p></td>
<td><p>可提供診斷和疑難排解資訊，包括 SIP 回應碼、診斷標頭、會議加入時間以及失敗之工作階段的診斷識別碼。</p></td>
</tr>
</tbody>
</table>


下表列出會議詳細資料報告的「會議形式」區段中所提供的資訊。

### 會議形式計量

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
<td><p><strong>使用者</strong></p></td>
<td><p></p></td>
<td><p>參與會議之使用者的 SIP 位址。</p></td>
</tr>
<tr class="even">
<td><p><strong>加入時間</strong></p></td>
<td><p></p></td>
<td><p>參與者加入會議的日期與時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>離開時間</strong></p></td>
<td><p></p></td>
<td><p>參與者離開會議的日期與時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>會議伺服器 URI</strong></p></td>
<td><p></p></td>
<td><p>會議中所使用之會議伺服器的 URI。</p></td>
</tr>
<tr class="odd">
<td><p><strong>診斷報告</strong></p></td>
<td><p></p></td>
<td><p>可提供診斷和疑難排解資訊，包括 SIP 回應碼、診斷標頭、會議加入時間以及失敗之工作階段的診斷識別碼。</p></td>
</tr>
</tbody>
</table>

