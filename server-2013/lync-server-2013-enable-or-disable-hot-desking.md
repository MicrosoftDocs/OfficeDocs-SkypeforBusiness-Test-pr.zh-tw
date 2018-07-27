---
title: 啟用或停用公用辦公桌
TOCTitle: 啟用或停用公用辦公桌
ms:assetid: 93a7fed6-f61a-4b41-9336-a8320afa87cf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994057(v=OCS.15)
ms:contentKeyID: 52056195
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 啟用或停用公用辦公桌

 

_**上次修改主題的時間：** 2013-02-20_

您可以將公用區電話設定為「公用辦公桌電話」。利用公用辦公室電話，使用者可登入本身的使用者帳戶，並且在登入之後，使用 Lync Server 功能及其本身的使用者設定檔設定。公用辦公室是透過用戶端原則來管理：若要啟用或停用公用辦公室電話，您必須修改公用區電話所使用的用戶端原則。如需如何判定已指派至公用區電話之會議原則的詳細資訊，請參閱＜[檢視公共區域電話資訊](lync-server-2013-view-common-area-phone-information.md)＞。

您使用 **New-CSClientPolicy** Cmdlet 的 EnableHotdesking 參數或 **Set-CSClientPolicy** Cmdlet，以啟用或停用公用辦公室電話，如下所示。從 Lync Server 2013 管理命令介面或 Windows PowerShell 的遠端工作階段執行這些 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。


## 啟用公用辦公室

  - 若要啟用公用區電話的公用辦公室，您必須修改已指派至該電話 (或電話集合) 的用戶端原則。
    
    已識別需要修改的原則之後，下一步請使用 **Set-CsClientPolicy** Cmdlet 以將 EnableHotdesking 參數設為 True。例如：
    
        Set-CsClientPolicy -Identity "CommonAreaPhonePolicy" - EnableHotdesking $True

  - 或者，您可以使用 **New-CsClientPolicy** Cmdlet 建立可啟用公用辦公室的新用戶端原則。例如：
    
        New-CsClientPolicy -Identity "NewCommonAreaPhonePolicy" - EnableHotdesking $True

> [!IMPORTANT]  
> 建立此原則之後，您必須將其指派給適合的公用區電話。如需詳細資訊，請參閱＜<a href="lync-server-2013-assign-policies-to-a-common-area-phone.md">指派原則給公共區域電話</a>＞。



## 停用公用辦公室

  - 若要停用公用區電話的公用辦公室，請將 **Set-CsClientPolicy** Cmdlet 的 EnableHotdesking 參數重設為預設值 False。例如：
    
        Set-CsClientPolicy -Identity "CommonAreaPhonePolicy" - EnableHotdesking $False

如需詳細資訊，請參閱＜[New-CsClientPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsClientPolicy) Cmdlet 與 [Set-CsClientPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClientPolicy)＞ Cmdlet 的說明主題。

