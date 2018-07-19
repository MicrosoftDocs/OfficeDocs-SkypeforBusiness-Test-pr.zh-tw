---
title: 刪除未指派號碼範圍
TOCTitle: 刪除未指派號碼範圍
ms:assetid: a8141bfb-b94d-4d0f-a7a9-2e60d10b103a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182565(v=OCS.15)
ms:contentKeyID: 49291929
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 刪除未指派號碼範圍

 

_**上次修改主題的時間：** 2012-11-01_

使用下列其中一個程序來刪除宣告的未指派號碼範圍。

## 使用 Lync Server 控制台刪除未指派的號碼範圍

1.  以 RTCUniversalServerAdmins 群組成員或者 CsVoiceAdministrator、CsServerAdministrator 或 CsAdministrator 角色成員的身分登入電腦。如需詳細資料，請參閱[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 **\[語音功能\]** 和 **\[未指派的號碼\]**。

4.  在 **\[未指派的號碼\]** 頁面上的搜尋欄位中，輸入您要刪除之未指派的號碼範圍的全部或部分名稱。

5.  在產生的號碼範圍清單中，依序按一下名稱、\[編輯\] 和 \[刪除\]。

6.  按一下 **\[全部認可\]**。

## 使用 Cmdlet 刪除未指派的號碼範圍

1.  以 RTCUniversalServerAdmins 群組成員身分或使用[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)中描述的必要使用者權限，登入裝有 Lync Server 管理命令介面的電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  在命令列中輸入：
    
        Remove-CsUnassignedNumber -Identity "<name of unassigned number range>" 
    
    例如：
    
        Remove-CsUnassignedNumber -Identity "Unassigned range 1"
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如需關於其他選項的詳細資訊，請參閱＜<a href="https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsCallParkOrbit">Remove-CsCallParkOrbit</a>＞。</td>
    </tr>
    </tbody>
    </table>


## 請參閱

#### 工作

[在 Lync Server 2013 中建立或修改未指派號碼範圍](lync-server-2013-create-or-modify-an-unassigned-number-range.md)  

#### 其他資源

[Remove-CsUnassignedNumber](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsUnassignedNumber)  
[Get-CsUnassignedNumber](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsUnassignedNumber)

