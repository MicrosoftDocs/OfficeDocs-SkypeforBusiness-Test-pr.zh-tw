---
title: Lync Server 2013：(選用) 啟用和停用會議加入和離開宣告
TOCTitle: (選用) 啟用和停用會議加入和離開宣告
ms:assetid: c9529568-e66c-48d8-aef2-9072f9c336ff
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398834(v=OCS.15)
ms:contentKeyID: 49292306
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# (選用) 在 Lync Server 2013 中啟用和停用會議加入和離開宣告

 

_**上次修改主題的時間：** 2012-09-30_

當撥入使用者加入或離開會議時， 會議宣告應用程式可藉由播放提示音或說出名稱的方式宣告使用者進入或離開。您可以執行 Cmdlet 來變更宣告運作的方式。這是選用步驟。

## 若要修改會議加入和離開宣告行為

1.  以 RTCUniversalServerAdmins 群組成員或 **Cs-ServerAdministrator** 、 **CsAdministrator** 角色成員的身分登入電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  在命令提示字元中執行下列命令：
    
        Get-CsDialinConferencingConfiguration
    
    此 Cmdlet 會擷取參與者加入會議時是否需要記錄其姓名的資訊，以及參與者加入或離開電話撥入式會議時 Lync Server 如何回應的資訊。

4.  在命令提示字元中執行下列命令：
    
        Set-CsDialinConferencingConfiguration -Identity <identity of dial-in conferencing settings to be modified>
        [-EnableNameRecording <$true | $false>]
        [-EntryExitAnnouncementsEnabledByDefault <$true | $false>]
        [-EntryExitAnnouncementsType <UseNames | ToneOnly]
    
    **EnableNameRecording**：判斷匿名參與者是否需要在進入會議之前記錄姓名。預設值為 "$true"，表示會提示匿名參與者在加入會議時說出其姓名 (驗證的參與者不會記錄其姓名，而是使用其顯示名稱)。
    
    **EntryExitAnnouncementsEnabledByDefault**：指出宣告預設為開啟或關閉。預設值為 "$false"，表示預設為不宣告參與者加入或離開會議。會議召集人在排程會議時可以覆寫這項設定。
    
    **EntryExitAnnouncementsType**：指出參與者加入或離開已啟用宣告的會議時，要採取的動作。預設值為 "UseNames"，表示會有類似下方的宣告：「Ken Myer 加入會議」(宣告開啟時)。
    
    您可以在全域範圍或網站範圍進行這些設定。在網站範圍進行的設定優先順序高於在全域範圍進行的設定。
    
    例如：
    
        Set-CsDialinConferencingConfiguration -Identity site:Redmond
        -EnableNameRecording $false
        -EntryExitAnnouncementsEnabledByDefault $true
        -EntryExitAnnouncementsType ToneOnly
    
    此範例中會在網站範圍進行 Redmond 的設定。宣告為開啟狀態，但是不會提示參與者在加入會議時說出自己的姓名。參與者進入或離開會議時，會播放提示音。

