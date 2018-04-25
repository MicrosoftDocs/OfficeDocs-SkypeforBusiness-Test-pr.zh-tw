---
title: 管理 Lync 線上會議與會議
TOCTitle: 管理 Lync 線上會議與會議
ms:assetid: a4d0c070-4df2-47df-a1e2-6ce62600a287
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362833(v=OCS.15)
ms:contentKeyID: 56269138
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 管理 Lync 線上會議與會議

 

_**上次修改主題的時間：** 2015-06-22_

下列 Cmdlet 可用於管理會議與會議設定：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="disable-csmeetingroom.md">Disable-CsMeetingRoom</a><br />
<a href="enable-csmeetingroom.md">Enable-CsMeetingRoom</a><br />
<a href="get-csmeetingroom.md">Get-CsMeetingRoom</a><br />
<a href="set-csmeetingroom.md">Set-CsMeetingRoom</a></p></td>
<td><p>管理會議室的端點裝置。</p>
<p>在 商務用 Skype Online 中，會議室為裝設於會議空間中的獨立式電腦裝置，並可提供進階會議功能。若要管理這些新端點裝置，其中您必須為裝置建立並啟用 Exchange 資源信箱帳戶，然後啟用該資源帳戶的 商務用 Skype Online。</p></td>
</tr>
<tr class="even">
<td><p><a href="get-csaudioconferencingprovider.md">Get-CsAudioConferencingProvider</a></p></td>
<td><p>傳回您的組織與之訂有合約的音訊會議提供者相關資訊。</p>
<p>音訊會議提供者是提供會議服務給組織的第三方公司，包括即時翻譯、記錄以及個別會議即時總機服務等高階服務。</p></td>
</tr>
<tr class="odd">
<td><p><a href="get-csmeetingconfiguration.md">Get-CsMeetingConfiguration</a><br />
<a href="set-csmeetingconfiguration.md">Set-CsMeetingConfiguration</a></p></td>
<td><p>控制使用者可建立的會議類型，並決定會議處理匿名使用者與撥入式會議使用者的方式。</p>
<p>會議是 商務用 Skype Online 不可或缺的一部分。例如，透過這些 Cmdlet，您可以將會議設定為禁止撥入使用者被自動登入會議，改為路由至會議大廳。這些撥入使用者會一直停留在大廳，直到簡報者准許他們加入會議為止。</p></td>
</tr>
</tbody>
</table>


您亦可使用 商務用 Skype Online 系統管理中心管理部分的會議設定內容：

![Lync 管理中心一般選項內容](images/Dn362833.acf90793-7ee4-4faf-b791-f149dd5df2a5(OCS.15).png "Lync 管理中心一般選項內容")

## 請參閱

#### 概念

[Lync Online Cmdlet](the-skype-for-business-online-cmdlets.md)  
[快速參考：使用 Windows PowerShell 執行 Lync Online 的一般管理工作](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

