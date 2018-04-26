---
title: 將剩餘使用者移到 Lync Server 2013
TOCTitle: 將剩餘使用者移到 Lync Server 2013
ms:assetid: 72025e1b-97d1-40e9-8a98-28c018942b48
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688090(v=OCS.15)
ms:contentKeyID: 49890113
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 將剩餘使用者移到 Lync Server 2013

 

_**上次修改主題的時間：** 2012-09-29_

您可使用 Lync Server 控制台或 Lync Server 管理命令介面將使用者移至新的 Lync Server 2013 部署。您必須符合某些特定要求，才能順利轉換至 Lync Server 2013。如需有關本主題中完成此程序之先決條件的詳細資訊，請參閱＜ [設定用戶端以進行移轉](configure-clients-for-migration.md)＞。如需有關移動使用者的詳細資訊，請參閱＜ [第 4 階段：將測試使用者移至試驗集區](phase-4-move-test-users-to-the-pilot-pool.md)＞。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法使用「Active Directory 使用者及電腦」嵌入式管理單元或 Lync Server 2010 系統管理工具將使用者從舊版環境移至 Lync Server 2013。</td>
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
<td>這包括由舊使用者所建立之作用中的會議。例如，如果舊使用者已設定一個 <strong>[我的會議]</strong> 會議，在移動該使用者之後，會議仍可於新的 Lync Server 2013 集區中使用。存取該會議的詳細資料仍為相同的 <strong>[會議 URL 及會議 ID]</strong> 。唯一的差異是，會議現由 Lync Server 2013 集區主控，而非 Lync Server 2010 集區。</td>
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

2.  若要確保位於 Lync Server 2013 上的使用者所召集的會議，與位於 Lync Server 2010 上的同盟使用者能順暢運作，指派給移轉使用者的會議原則應該允許匿名參與者。

3.  在 Lync Server 2013 控制台中，允許匿名參與者的會議原則應選取 **\[允許參與者邀請匿名使用者\]** ，且來自 Lync Server 管理命令介面 中的 **Get-CsConferencingPolicy** Cmdlet 輸出之 **AllowAnonymousParticipantsInMeeting\]** 應設為 **True** 。

4.  如需有關使用 Lync Server 管理命令介面設定會議原則的詳細資訊，請參閱＜Lync Server 管理命令介面＞文件中的 [Set-CsConferencingPolicy](set-csconferencingpolicy.md)。

