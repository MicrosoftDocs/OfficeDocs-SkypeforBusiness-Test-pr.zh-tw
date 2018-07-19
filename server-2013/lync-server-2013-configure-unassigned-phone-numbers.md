---
title: 設定未指派電話號碼
TOCTitle: 設定未指派電話號碼
ms:assetid: a0650659-dce7-455f-8977-02454bbfa400
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182559(v=OCS.15)
ms:contentKeyID: 49291856
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定未指派電話號碼

 

_**上次修改主題的時間：** 2012-11-01_

Lync Server 可讓您設定如何處理撥打至組織內有效，但未指派給使用者或電話之電話號碼的來電。若要設定這類通話的處理方式，您可設定未指派號碼表。您可利用此表格將通話路由傳送至宣告應用程式或 Exchange UM 伺服器。

設定未指派號碼表的方式取決於其使用方式。您可以設定包含組織所有有效分機號碼、只包含未指派的分機號碼，或包含結合這兩種類型之號碼的表格。未指派號碼表可以同時包含已指派和未指派的號碼，但是只有在來電者撥打目前未指派的號碼時才會叫用。如果您在未指派號碼表中納入所有有效的分機號碼，可以指定每次某人離開組織時要執行的動作，而不必重新設定表格。如果表格中包含未指派的分機號碼，您可以針對特定號碼設計要採取的動作。例如，如果您變更客戶服務人員的分機號碼，則可以在表格中包含舊的客戶服務號碼，並且將它指派給提供新號碼的宣告。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須先定義一個或多個宣告或設定 Exchange UM 自動語音應答，才能設定未指派號碼表。如需建立宣告的詳細資訊，請參閱＜<a href="lync-server-2013-create-an-announcement.md">在 Lync Server 2013 中建立宣告</a>＞。若要查看是否已進行 Exchange UM 設定，請執行 <strong>Get-CsExUmContact</strong> Cmdlet。如需詳細資訊，請參閱＜<a href="https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsExUmContact">Get-CsExUmContact</a>＞。</td>
</tr>
</tbody>
</table>


## 本章節內容

  - [在 Lync Server 2013 中建立或修改未指派號碼範圍](lync-server-2013-create-or-modify-an-unassigned-number-range.md)

  - [刪除未指派號碼範圍](lync-server-2013-delete-an-unassigned-number-range.md)

