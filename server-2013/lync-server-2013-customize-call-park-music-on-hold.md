---
title: 在 Lync Server 2013 中自訂通話駐留等候音樂
TOCTitle: 在 Lync Server 2013 中自訂通話駐留等候音樂
ms:assetid: 3d78e6f9-a4ae-49f4-a89f-4515acb49dac
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688031(v=OCS.15)
ms:contentKeyID: 49890030
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中自訂通話駐留等候音樂

 

_**上次修改主題的時間：** 2012-09-10_

您可以指定自己的音樂檔案用於等候音樂，而不使用 Lync Server 2013 隨附的預設音樂檔案。如要自訂等候音樂，請使用 **Set-CsCallParkServiceMusicOnHoldFile** Cmdlet。

> [!NOTE]  
> 如果您自訂等候音樂並想將相同的音樂用於多個網站，則需在每個執行通話駐留應用程式的網站設定該音樂檔案。



## 自訂音樂檔案

1.  以 RTCUniversalServerAdmins 群組成員身分或使用[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)中描述的必要使用者權限，登入裝有 Lync Server 管理命令介面的電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  執行：
    
        Set-CsCallParkServiceMusicOnHoldFile -Service <ServiceID where the Call Park application resides> -Content <Byte[]>
    
    > [!TIP]
    > 使用 <strong>Get-CsService</strong> Cmdlet 來識別服務。如需詳細資訊，請參閱＜<a href="https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsService">Get-CsService</a>＞。
    
    下列範例顯示如何取得檔案 soothingmusic.wma 的位元組陣列內容，並將其指派給變數。然後將音訊檔案指派為通話駐留時的等候音樂檔案。如需詳細資訊，請參閱＜[Set-CsCallParkServiceMusicOnHoldFile](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsCallParkServiceMusicOnHoldFile)＞。
    
        $a = Get-Content -ReadCount 0 -Encoding byte "C:\MoHFiles\soothingmusic.wma"
        Set-CsCallParkServiceMusicOnHoldFile -Service Redmond1-applicationserver-1 -Content $a

## 請參閱

#### 其他資源

[Set-CsCallParkServiceMusicOnHoldFile](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsCallParkServiceMusicOnHoldFile)  
[Get-CsService](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsService)

