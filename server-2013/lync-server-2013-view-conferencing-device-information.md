---
title: 檢視會議裝置資訊
TOCTitle: 檢視會議裝置資訊
ms:assetid: 838bdbf8-8b68-4eb6-8fa3-45bfd5b0b1cd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994043(v=OCS.15)
ms:contentKeyID: 52056137
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 檢視會議裝置資訊

 

_**上次修改主題的時間：** 2013-02-20_

您可以使用 Windows PowerShell 和 **Get-CsMeetingRoom** Cmdlet 檢視供組織使用而設定之會議裝置的相關資訊。請從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段執行 **Get-CsMeetingRoom** Cmdlet。

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


如果您使用不含任何參數的 **Get-CsMeetingRoom** Cmdlet，其會傳回所有會議裝置的相關資訊。選用的參數則提供讓您篩選資訊的各種方法。如需詳細資訊，請參閱＜[Get-CsMeetingRoom](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsMeetingRoom)＞的＜參數＞一節。


## 檢視所有會議裝置的相關資訊

  - 若要檢視所有會議裝置的詳細資訊，請在 Lync Server 管理命令介面輸入下列命令，然後按 Enter：
    
        Get-CsMeetingRoom
    
    對於各個會議裝置，此 Cmdlet 會傳回類似下列的資訊。請注意，此範例僅顯示執行此 Cmdlet 會看見的部分資訊：
    
        ContactOptionFlags                : 64
        OwnerUrn                          : urn:device:roomsystem
        OriginatorSid                     :
        SamAccountName                    : room12129
        UserPrincipalName                 : room1219@litwareinc.com
        FirstName                         : 
        LastName                          :
        WindowsEmailAddress               :
        Sid                               : S-1-5-21-2831376166-2963252556-2165051629-1257
        LineServerURI                     :
        AudioVideoDisabled                : False
        IPPBXSoftPhoneRoutingEnabled      : False
        RemoteCallControlTelephonyEnabled : False
        PrivateLine                       :
        AcpInfo                           : {}
        HostedVoiceMail                   :
        DisplayName                       : Room 1219

## 檢視特定會議裝置的相關資訊

  - 若要檢視特定會議裝置的資訊，請在會議裝置識別 (通常是 Active Directory 顯示名稱) 後面加上 Identity 參數。例如：
    
        Get-CsMeetingRoom -Identity "Room 1219"

如需詳細資訊，請參閱 [Get-CsMeetingRoom](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsMeetingRoom) Cmdlet 的說明主題。

