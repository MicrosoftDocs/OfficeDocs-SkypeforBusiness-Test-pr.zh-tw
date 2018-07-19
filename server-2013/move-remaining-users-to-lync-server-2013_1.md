---
title: 將剩餘使用者移到 Lync Server 2013
TOCTitle: 將剩餘使用者移到 Lync Server 2013
ms:assetid: 0eb990f0-f720-47a7-aaee-437fbd4c4c33
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ687968(v=OCS.15)
ms:contentKeyID: 49889939
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 將剩餘使用者移到 Lync Server 2013

 

_**上次修改主題的時間：** 2012-09-26_

您可使用 Lync Server 控制台或 Lync Server 管理命令介面將使用者移至新的 Lync Server 2013 部署。您必須符合某些特定要求，才能順利轉換至 Lync Server 2013。如需有關本主題中完成此程序之先決條件的詳細資訊，請參閱＜ [設定用戶端以進行移轉](configure-clients-for-migration_1.md)＞。如需有關移動使用者的詳細資訊，請參閱＜ [第 6 階段：將使用者移至試驗集區](phase-6-move-users-to-the-pilot-pool.md)＞。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法使用「Active Directory 使用者及電腦」嵌入式管理單元或 Microsoft Office Communications Server 2007 R2 系統管理工具將使用者從舊版環境移至 Lync Server 2013。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Move-CsLegacyUser</strong> Cmdlet 需要格式正確的使用者名稱，且名稱開頭及結尾不可包含任何空格，否則將無法使用 <strong>Move-CsLegacyUser</strong> Cmdlet 移動使用者帳戶。</td>
</tr>
</tbody>
</table>


當您將使用者移至 Lync Server 2013 集區之時，使用者的資料會移至與新集區相關聯的後端資料庫。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>這包括由舊版使用者所建立的作用中的會議。例如，若舊版使用者已設定了 [我的會議] 會議，則在移動使用者之後，該會議仍可使用於新的 Lync Server 2013 集區。存取該會議的詳細資料仍是相同的 [會議 URL 及會議 ID] 。唯一的差異是，現在會議是位於 Lync Server 2013 集區，而不是 Office Communications Server 2007 R2 集區。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Lync Server 2013 設定使用者不需要同時部署升級用戶端。只有當使用者已升級為新的用戶端軟體時，才可使用新功能。</td>
</tr>
</tbody>
</table>


## 移轉後的工作

1.  一旦移除使用者之後，請驗證指派給他們的會議原則。

2.  若要確保位於 Lync Server 2013 上的使用者所召集的會議，與位於 Office Communications Server 2007 R2 上的同盟使用者能順暢運作，指派給移轉使用者的會議原則應該允許匿名參與者。

3.  在 Lync Server 2013 控制台中，允許匿名參與者的會議原則應選取 **\[允許參與者邀請匿名使用者\]** ，且來自 Lync Server 管理命令介面 中的 **Get-CsConferencingPolicy** Cmdlet 輸出之 **AllowAnonymousParticipantsInMeeting\]** 應設為 **True** 。

4.  如需有關使用 Lync Server 管理命令介面設定會議原則的詳細資訊，請參閱＜Lync Server 管理命令介面＞文件中的 [Set-CsConferencingPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsConferencingPolicy)。

