---
title: 刪除公告
TOCTitle: 刪除公告
ms:assetid: 26ea7149-4470-4c22-9bab-8a4065aca44e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ687998(v=OCS.15)
ms:contentKeyID: 49889985
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 刪除公告

 

_**上次修改主題的時間：** 2012-11-01_

使用下列程序刪除未指派之號碼的電話所使用的宣告。

## 刪除宣告

1.  以 RTCUniversalServerAdmins 群組成員身分或使用[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)中描述的必要使用者權限，登入裝有 Lync Server 管理命令介面的電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  列出組織中的所有宣告。在命令列中執行：
    
        Get-CsAnnouncement

4.  在結果清單中，找出您要刪除的宣告，並複製 GUID。然後在命令列中執行：
    
        Remove-CsAnnouncement -Identity "<Service:service ID/guid>" 
    
    例如：
    
        Remove-CsAnnouncement -Identity "ApplicationServer:Redmond.contoso.com/1951f734-c80f-4fb2-965d-51807c792b90"
    
    > [!NOTE]  
    > 如需選項的詳細資訊，請參閱＜<a href="https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsAnnouncement">Get-CsAnnouncement</a>＞及＜<a href="https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsAnnouncement">Remove-CsAnnouncement</a>＞。
    


## 請參閱

#### 工作

[在 Lync Server 2013 中建立宣告](lync-server-2013-create-an-announcement.md)  

#### 其他資源

[Remove-CsAnnouncement](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsAnnouncement)  
[Get-CsAnnouncement](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsAnnouncement)

