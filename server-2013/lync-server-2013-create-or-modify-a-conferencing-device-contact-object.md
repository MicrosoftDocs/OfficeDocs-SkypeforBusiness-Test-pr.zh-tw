---
title: 建立或修改會議裝置連絡人物件
TOCTitle: 建立或修改會議裝置連絡人物件
ms:assetid: 62ed64be-379c-417d-9453-511881cf5604
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994035(v=OCS.15)
ms:contentKeyID: 52056117
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 建立或修改會議裝置連絡人物件

 

_**上次修改主題的時間：** 2013-10-02_

若要建立會議室物件，首先建立 Active Directory 使用者帳戶來代表該裝置。然後使用 **Enable-CsMeetingRoom** Cmdlet，以啟用該帳戶做為會議裝置。如果需要變更現有會議裝置的內容，可使用 **Set-CsMeetingRoom** Cmdlet。

可從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段執行這些 Cmdlet。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：<a href="http://go.microsoft.com/fwlink/p/?linkid=255876">http://go.microsoft.com/fwlink/p/?linkId=255876</a>。</td>
</tr>
</tbody>
</table>



## 建立會議裝置

  - 在建立要代表新會議裝置的 Active Directory 使用者帳戶之後，可使用 **Enable-CsMeetingRoom** Cmdlet 予以啟用。但務必包括 a) 會議裝置識別碼、b) 會議室帳戶將隸屬的登錄器集區，以及 c) 要指派給該帳戶的 SIP 位址。例如︰
    
        Enable-CsMeetingRoom -Identity "Redmond Conferencing device" -RegistrarPool "atl-cs-001.litwareinc.com" -SipAddress "sip:RedmondMeetingRoom@litwareinc.com"

## 修改會議裝置

  - 若要修改現有會議裝置的內容值，可使用 **Set-CsMeetingRoom** Cmdlet。例如，下列命令會更新與會議裝置關聯的電話號碼 (LineUri)︰
    
        Set-CsMeetingRoom -Identity "Redmond Conferencing device" -LineUri "tel:+12065551219"

如需詳細資訊，請參閱＜[Enable-CsMeetingRoom](https://docs.microsoft.com/en-us/powershell/module/skype/Enable-CsMeetingRoom) Cmdlet 和 [Set-CsMeetingRoom](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsMeetingRoom)＞ Cmdlet 的說明主題。

