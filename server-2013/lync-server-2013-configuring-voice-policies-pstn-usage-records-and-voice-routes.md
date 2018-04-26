---
title: Lync Server 2013：設定語音原則、PSTN 使用方式記錄和語音路由
TOCTitle: 設定語音原則、PSTN 使用方式記錄和語音路由
ms:assetid: 1e5a15f9-6f42-4dc6-baaa-24daf54afc4d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398272(v=OCS.15)
ms:contentKeyID: 49290289
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定語音原則、PSTN 使用方式記錄和語音路由

 

_**上次修改主題的時間：** 2012-10-10_

語音原則、PSTN 使用方式記錄和語音路由密切相關。您可以選取一組撥號功能，接著指派一組 PSTN 使用方式記錄給原則，以便指定獲指派語音原則的使用者或群組可獲得哪些權限授權，如此就能設定語音原則。語音路由也會被指派 PSTN 使用方式記錄，這些記錄會用來比對路由與獲授權使用這些路由的使用者。也就是說，使用者可以撥打的電話，只限於使用他們有相符 PSTN 使用方式記錄之路由的電話。

新 Enterprise Voice 部署的建議工作流程是：從設定包含適當 PSTN 使用方式記錄的語音原則開始，接著將適當路由關聯給每個 PSTN 使用方式記錄。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您也可以在「 <em>使用者</em> 」範圍建立語音原則，然後將其指派給個別使用者或群組。</td>
</tr>
</tbody>
</table>


如需執行每項工作的詳細步驟，請參閱本節程序。

## 本章節內容

  - [在 Lync Server 2013 中設定用於授權撥號功能和權限的語音原則和 PSTN 使用方式記錄](lync-server-2013-configuring-voice-policies-and-pstn-usage-records-to-authorize-calling-features-and-privileges.md)

  - [在 Lync Server 2013 中檢視 PSTN 使用方式記錄](lync-server-2013-view-pstn-usage-records.md)

  - [Lync Server 2013 中設定撥出電話的語音路由](lync-server-2013-configuring-voice-routes-for-outbound-calls.md)

  - [在 Lync Server 2013 中匯出和匯入語音路由組態](lync-server-2013-exporting-and-importing-voice-routing-configuration.md)

  - [在 Lync Server 2013 中發佈擱置變更至語音路由設定](lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md)

  - [在 Lync Server 2013 中測試語音路由](lync-server-2013-test-voice-routing.md)

