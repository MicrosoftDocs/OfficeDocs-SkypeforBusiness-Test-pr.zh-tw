---
title: 啟用或停用會議裝置
TOCTitle: 啟用或停用會議裝置
ms:assetid: d5140e38-d015-4706-9bde-cf2fa748c36b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994070(v=OCS.15)
ms:contentKeyID: 52056228
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 啟用或停用會議裝置

 

_**上次修改主題的時間：** 2013-02-20_

使用 **Enable-CsMeetingRoom** Cmdlet 和 **Disable-CsMeetingRoom** Cmdlet 啟用和停用會議裝置。可從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段執行這些 Cmdlet。

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



## 啟用會議裝置

  - 若要啟用會議裝置，請使用 **Enable-CsMeetingRoom** Cmdlet。啟用會議裝置時，您必須加入 a) 會議裝置身分識別、b) 主控會議室帳戶的登錄器集區，以及 c) 指派給帳戶的 SIP 位址。
    
        Enable-CsMeetingRoom -Identity "Redmond Conferencing device" -RegistrarPool "atl-cs-001.litwareinc.com" -SipAddress "sip:RedmondMeetingRoom@litwareinc.com"

## 停用會議室裝置

  - 若要停用會議室裝置，請使用 **Disable-CsMeetingRoom** Cmdlet。請務必指定要停用的會議室裝置身分識別：
    
        Disable-CsMeetingRoom -Identity "sip:RedmondMeetingRoom@litwareinc.com"

如需詳細資訊，請參閱＜[Enable-CsMeetingRoom](https://docs.microsoft.com/en-us/powershell/module/skype/Enable-CsMeetingRoom)＞ Cmdlet 和＜[Disable-CsMeetingRoom](https://docs.microsoft.com/en-us/powershell/module/skype/Disable-CsMeetingRoom)＞ Cmdlet 的說明主題。

