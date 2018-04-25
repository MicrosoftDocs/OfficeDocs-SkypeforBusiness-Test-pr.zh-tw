---
title: Lync Server 2013：為使用者啟用通話駐留
TOCTitle: 為使用者啟用通話駐留
ms:assetid: 9430763f-3394-467c-9c6d-426bf761604e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398753(v=OCS.15)
ms:contentKeyID: 49291692
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中為使用者啟用通話駐留

 

_**上次修改主題的時間：** 2012-09-11_

除非語音原則允許使用者使用 通話駐留功能，否則使用者不能駐留通話或擷取駐留的通話。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>根據預設，所有使用者的 通話駐留都是停用。</td>
</tr>
</tbody>
</table>


您可以在全域範圍、網站範圍或使用者範圍上啟用 通話駐留。使用者範圍的優先順序高於網站範圍，網站範圍的優先順序高於全域範圍。如果您有多個語音原則，請檢閱所有原則以啟用 通話駐留，而不是僅檢閱全域原則。

## 使用 Lync Server 控制台來為使用者啟用 通話駐留

1.  以 **RTCUniversalServerAdmins** 群組成員或 **CsVoiceAdministrator** 、 **CsServerAdministrator** 、 **CsAdministrator** 系統管理角色成員的身分登入電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[語音路由\] 。

4.  按一下 **\[語音原則\]** 索引標籤。

5.  按兩下現有的語音原則以開啟 **\[編輯語音原則\]** 對話方塊。

6.  選取 **\[撥號功能\]** 下的 **\[啟用通話駐留\]** 。

7.  按一下 **\[確定\]** 以儲存語音原則。

## 使用 Cmdlet 為使用者啟用 通話駐留

1.  以 RTCUniversalServerAdmins 群組成員或 CsVoiceAdministrator、CsServerAdministrator 或 CsAdministrator 系統管理角色成員的身分登入電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  執行：
    
        Set-CsVoicePolicy -Identity <VoicePolicy> -EnableCallPark $true
    
    例如，若要為預設的全域語音原則啟用 通話駐留：
    
        Set-CsVoicePolicy -EnableCallPark $true

## 請參閱

#### 工作

[在 Lync Server 2013 中建立語音原則和設定 PSTN 使用方式記錄](lync-server-2013-create-a-voice-policy-and-configure-pstn-usage-records.md)

