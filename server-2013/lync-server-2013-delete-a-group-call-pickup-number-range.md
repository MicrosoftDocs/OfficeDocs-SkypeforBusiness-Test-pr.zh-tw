---
title: 刪除群組來電接聽號碼範圍
TOCTitle: 刪除群組來電接聽號碼範圍
ms:assetid: 521891f3-7a5d-45de-92dc-d57025453159
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945629(v=OCS.15)
ms:contentKeyID: 52056109
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 刪除群組來電接聽號碼範圍

 

_**上次修改主題的時間：** 2013-01-30_

您可使用下列程序以刪除群組來電接聽號碼範圍。

## 刪除來電接聽群組號碼範圍

1.  以 RTCUniversalServerAdmins 群組成員身分或使用[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)中描述的必要使用者權限，登入裝有 Lync Server 管理命令介面的電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  在命令列中輸入：
    
        Remove-CsCallParkOrbit -Identity "<group number range name>" 
    
    例如︰
    
        Remove-CsCallParkOrbit -Identity "Redmond call pickup"
    
    > [!NOTE]  
    > 如需其他選項的詳細資訊，請參閱＜<a href="https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsCallParkOrbit">Remove-CsCallParkOrbit</a>＞。
    


## 請參閱

#### 工作

[在 Lync Server 2013 中建立或修改通話駐留軌道範圍](lync-server-2013-create-or-modify-a-call-park-orbit-range.md)  

#### 其他資源

[Remove-CsCallParkOrbit](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsCallParkOrbit)  
[Get-CsCallParkOrbit](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsCallParkOrbit)

