---
title: Lync Server 2013：(選用) 修改 DTMF 命令的按鍵對應
TOCTitle: (選用) 修改 DTMF 命令的按鍵對應
ms:assetid: d753b78d-400c-4df2-957f-e7576b2019c2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398943(v=OCS.15)
ms:contentKeyID: 49292449
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# (選用) 在 Lync Server 2013 中修改 DTMF 命令的按鍵對應

 

_**上次修改主題的時間：** 2012-09-30_

電話撥入式會議使用者可以按電話鍵盤上的按鍵，以執行複頻式訊號 (DTMF) 命令。DTMF 命令可讓撥電話參與會議的使用者使用其電話鍵盤來控制會議設定 (例如自行設定靜音和解除靜音，或鎖定和解除鎖定會議)。您可以使用 Cmdlet 來修改 DTMF 命令所用的按鍵。這是選用步驟。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如需這些 Cmdlet 及可用 DTMF 選項的詳細資訊，請參閱 Lync Server 管理命令介面文件或 Lync Server 管理命令介面命令列說明。</td>
</tr>
</tbody>
</table>


## 若要修改 DTMF 命令的按鍵對應

1.  以 **RTCUniversalServerAdmins** 群組成員身分，或是 **Cs-ServerAdministrator** 或 **CsAdministrator** 角色成員的身分登入電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  在命令提示字元中執行下列命令：
    
        Get-CsDialinConferencingDtmfConfiguration
    
    此 Cmdlet 會傳回用於撥入式電話會議的 DTMF 設定。

4.  執行下列 Cmdlet，並為您要變更的每個選項指定要按下的按鍵：
    
        Set-CsDialinConferencingDtmfConfiguration [-Identity <global or site collection to be changed>]
        [-AdmitAll <default key is 8>] [-AudienceMuteCommand <default key is 4>]
        [-CommandCharacter <* (default) | #>] [-EnableDisableAnnouncementsCommand <default key is 9>]
        [-HelpCommand <default key is 1>] [-LockUnlockConferenceCommand <default key is 7>]
        [-MuteUnmuteCommand <default key is 6>] [-PrivateRollCallCommand <default key is 3>]
    
    此 Cmdlet 會修改用於電話撥入式會議的 DTMF 設定。
    
    例如：
    
        Set-CsDialinConferencingDtmfConfiguration -EnableDisableAnnouncementsCommand 4 -AudienceMuteCommand 9
    
    此範例會切換下列按鍵：按下時可啟用或停用宣告的按鍵，以及按下時可將所有參與者靜音或解除靜音的按鍵。由於未指定任何身分識別，因此這些變更會套用至全域 DTMF 設定。

5.  (選用) 若要為特定網站建立額外的 DTMF 命令集合，請使用指定網站身分識別的 **New-CsDialinConferencingDtmfConfiguration** Cmdlet。當您為網站建立新的 DTMF 設定時，網站設定會優先於全域設定。如需詳細資訊，請參閱 Lync Server 管理命令介面文件或 Lync Server 管理命令介面命令列說明。

