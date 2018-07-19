---
title: Lync Server 2013：建立或修改未指派號碼範圍
TOCTitle: 建立或修改未指派號碼範圍
ms:assetid: a102b226-0460-4d5c-82f9-79b8444fa958
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412748(v=OCS.15)
ms:contentKeyID: 49291842
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建立或修改未指派號碼範圍

 

_**上次修改主題的時間：** 2012-11-01_

使用下列其中一個程序來設定 宣告應用程式的未指派號碼範圍。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須先定義一個或多個宣告或設定 Exchange Unified Messaging (UM) 自動語音應答，才能設定未指派號碼表。</td>
</tr>
</tbody>
</table>


## 使用 Lync Server 控制台 設定未指派的電話號碼

1.  以 RTCUniversalServerAdmins 群組成員或者 CsVoiceAdministrator、CsServerAdministrator 或 CsAdministrator 角色成員的身分登入電腦。如需詳細資料，請參閱[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 \[語音功能\] 和 \[未指派的號碼\] 。

4.  在 \[未指派的號碼\] 頁面上，執行下列其中一項：
    
      - 若要建立新的號碼範圍，請按一下 \[新增\] 。在 \[名稱\] 中輸入此號碼範圍的識別名稱。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>您對資料庫認可新的未指派號碼範圍之後，就無法變更此名稱。</td>
        </tr>
        </tbody>
        </table>
    
      - 若要修改現有號碼範圍，請在搜尋欄位中輸入號碼範圍的完整或部分名稱。在產生的號碼範圍清單中，依序按一下您要的名稱、\[編輯\] 和 \[顯示詳細資料\] 。

5.  在第一個 **\[號碼範圍\]** 欄位中輸入範圍的開始號碼，在第二個 **\[號碼範圍\]** 欄位中輸入範圍的結束號碼。
    
    <table>
    <colgroup>
    <col style="width: 100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><ul>
    <li><p>該範圍的起始號碼必須小於或等於範圍的結束號碼。</p></li>
    <li><p>如果範圍的開始號碼或範圍的結束號碼包含分機號碼，則範圍的開始號碼和結束號碼都必須包含分機，且開始號碼和結束號碼的分機號碼必須相同。</p></li>
    <li><p>此號碼必須符合規則運算式 (tel:)?(\+)?[1-9]\d{0,17}(;ext=[1-9]\d{0,9})?。這表示號碼的開頭可以是字串 tel: (如果您未指定該字串，則會自動新增該字串)、一個加號 (+)，以及數字 1 到 9。電話號碼最多可達 17 位，且後面可以再加分機，格式為 ;ext= 分機號碼。</p></li>
    </ul></td>
    </tr>
    </tbody>
    </table>


6.  在 **\[宣告服務\]** 中，執行下列其中一個動作：
    
      - 按一下 **\[宣告\]** 。
    
      - 按一下 **\[Exchange UM\]** 。

7.  如果您在上一個步驟按了 **\[宣告\]** ，請執行下列動作：
    
    1.  在 \[目的地伺服器的 FQDN\] 下方按一下 \[選取\] ，按一下執行 宣告應用程式之應用程式服務的服務 ID (此服務會處理此未指派號碼範圍的來電)，然後按一下 \[確定\] 。
    
    2.  在 **\[宣告\]** 中，按一下要針對此未指派號碼範圍播放的宣告。

8.  如果您在上一個步驟按了 **\[Exchange UM\]** ，請在 **\[自動語音應答電話號碼\]** 下方按一下 **\[選取\]** ，按一下要用於此未指派號碼範圍的電話號碼，然後按一下 \[確定\] 。

9.  按一下 \[確定\] 。

10. 在 \[未指派的號碼\] 頁面上，確定未指派的號碼範圍依您想要的順序排列。若要變更表格中範圍的位置，請按一下範圍清單中一個或多個連續名稱，然後按向上或向下箭頭。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Lync Server 會從上往下搜尋未指派的號碼表格，並使用第一個符合未指派號碼的範圍。如果您有重疊範圍以及一個範圍指定的是最後不得不採取的動作，請確定該範圍位於清單底部。</td>
    </tr>
    </tbody>
    </table>


11. 依照您想要的順序排列未指派的號碼範圍之後，按一下 **\[全部認可\]** 。

## 使用 Windows PowerShell 設定未指派的電話號碼

1.  以 RTCUniversalServerAdmins 群組成員身分或使用[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)中描述的必要使用者權限，登入裝有 Lync Server 管理命令介面的電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  使用 **New-CsUnassignedNumber** 建立新的未指派號碼範圍。使用 **Set-CsUnassignedNumber** 修改現有的未指派號碼範圍。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您有重疊範圍，並想要以特定順序套用這些範圍，請包含 Priority 參數。通話將會套用具有最高優先順序的範圍。</td>
    </tr>
    </tbody>
    </table>
    
    在命令列中，執行下列其中一項：
    
      - 若要建立宣告服務的號碼範圍，請執行：
        
            New-CsUnassignedNumber -Identity <unique identifier for unassigned number range> -NumberRangeStart <first number in range> -NumberRangeEnd <last number in range> -AnnouncementName <announcement name> -AnnouncementService <FQDN or service ID of the Announcement service>
    
      - 或是要建立 Exchange UM 自動語音應答的號碼範圍，請執行：
        
            New-CsUnassignedNumber -ExUmAutoAttendantPhoneNumber <phone number> -Identity <unique identifier for unassigned number range> -NumberRangeStart <first number in range> -NumberRangeEnd <last number in range>
    
    例如：
    
        New-CsUnassignedNumber -Identity "Unassigned range 1" -NumberRangeStart "+14255551000" -NumberRangeEnd "+14255551100" -AnnouncementName "Welcome Announcement" -AnnouncementService ApplicationServer:Redmond.contoso.com
    
    或者
    
        New-CsUnassignedNumber -ExUmAutoAttendantPhoneNumber "+12065551234" -Identity "Unassigned range 1" -NumberRangeStart "+14255551000" -NumberRangeEnd "+14255551100"
    
    以下範例示範如何修改現有未指派號碼範圍中的號碼：
    
        Set-CsUnassignedNumber -Identity "Unassigned range 1" -NumberRangeStart "+14255551000" -NumberRangeEnd "+14255551900"

## 請參閱

#### 工作

[刪除未指派號碼範圍](lync-server-2013-delete-an-unassigned-number-range.md)  

#### 其他資源

[New-CsUnassignedNumber](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsUnassignedNumber)  
[Set-CsUnassignedNumber](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsUnassignedNumber)  
[Get-CsUnassignedNumber](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsUnassignedNumber)

