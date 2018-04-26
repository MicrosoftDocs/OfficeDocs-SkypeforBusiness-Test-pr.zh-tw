---
title: Lync Server 2013：設定語音信箱重新路由設定
TOCTitle: 設定語音信箱重新路由設定
ms:assetid: 7ab6be28-eabb-4a79-a796-648887d71b83
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398606(v=OCS.15)
ms:contentKeyID: 49291406
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定語音信箱重新路由設定

 

_**上次修改主題的時間：** 2012-10-18_

如果已在中央網站安裝 Exchange 整合通訊 (UM)，並已部署 Exchange UM 訊息自動語音應答 (AA)，則 Survivable Branch Appliance 和 Survivable Branch 伺服器可在 WAN 中斷期間為分支網站使用者提供語音信箱存續能力。建議您的 Exchange 系統管理員應將 AA 設定成僅接受訊息，而停用其他一般功能 (例如轉接給使用者或轉接給操作員)。或者，您也可以使用一般 AA 或自訂 AA 來路由電話。

如需詳細資訊，請參閱規劃文件中 [Lync Server 2013 的分支網站復原需求](lync-server-2013-branch-site-resiliency-requirements.md)的＜準備語音信箱存續能力＞一節。

## 若要設定語音信箱存續能力

1.  要求您的 Exchange 系統管理員將 AA 設定成僅接受訊息 (在 Exchange 命令介面中，請使用下列 Cmdlet： **Set-UMAutoAttendant \<AA name\> -CallSomeoneEnabled $false**。指定要允許留言的參數 ( *SendVoiceMsgEnabled*) 預設為 true。

2.  在 Lync Server 管理命令介面中使用 **New-CSVoiceMailReroutingConfiguration** Cmdlet，將 AA 電話號碼設定作為 Survivable Branch Appliance 或 Survivable Branch 伺服器 上語音信箱重新路由設定中的 Exchange UM 自動語音應答電話號碼。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您之後需要修改語音信箱重新路由設定，請使用 <strong>Set-CsVoiceMailReRoutingConfiguration</strong> Cmdlet 來執行。如需 <strong>New-</strong> 和 <strong>Set-CSVoiceMailReroutingConfiguration</strong> 的詳細資訊，請參閱命令介面的說明主題。</td>
    </tr>
    </tbody>
    </table>


3.  將與分支網站使用者的 Exchange UM 撥號對應表對應的 Exchange UM 訂戶存取號碼，設定作為 Survivable Branch Appliance 或 Survivable Branch 伺服器上語音信箱重新路由設定中的 Exchange UM 訂戶存取號碼。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>設定 Exchange UM 使用者的撥號對應表，讓所有在 WAN 中斷期間需要存取 [進入語音信箱] 功能的分支網站使用者只有一個相關聯的撥號對應表。</td>
    </tr>
    </tbody>
    </table>


Survivable Branch Appliance 或 Survivable Branch 伺服器的 **下一個步驟** ： [在 Lync Server 2013 中將使用者隸屬於 Survivable Branch Appliance 或 Survivable Branch Server](lync-server-2013-home-users-on-a-survivable-branch-appliance-or-server.md)。

