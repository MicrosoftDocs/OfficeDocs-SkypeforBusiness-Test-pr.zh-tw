---
title: 檢視信任的應用程式資訊
TOCTitle: 檢視信任的應用程式資訊
ms:assetid: 7b916323-96fb-4308-bc95-c178de41a3d3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688103(v=OCS.15)
ms:contentKeyID: 49890129
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 檢視信任的應用程式資訊

 

_**上次修改主題的時間：** 2015-03-30_

使用下列程序檢視 Lync Server 管理命令介面中的 Lync Server 2013 管理命令介面信任的應用程式資訊。

## 使用 Lync Server 管理命令介面 Cmdlet 檢視信任應用程式資訊

您可以使用 Lync Server 管理命令介面和 **Get-CsTrustedApplication** Cmdlet 檢視信任應用程式的相關資訊。從 Lync Server 2013 管理命令介面或從 Windows PowerShell 可以執行這個 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 檢視信任的應用程式

  - 若要檢視所有信任的應用程式，請在 Lync Server 管理命令介面中輸入下列命令，然後按下 ENTER 鍵：
    
        Get-CsConferenceDisclaimer
    
    對於各個信任的應用程式，這個命令將傳回類似下列的資訊：
    
        Identity               : CN={5dedf4b0-a590-49b3-80cf-f16f914bbef9},CN=Application Contacts,CN=RTC
                                 Service,CN=Services,CN=Configuration,DC=litware,DC=com
        RegistrarPool          : 487279971
        HomeServer             : CN=Lc Services,CN=Microsoft,CN=co1:2,CN=Pools,CN=RTC
                                 Service,CN=Services,CN=Configuration,DC=litware,DC=com
        OwnerUrn               : urn:application:helpdesk
        SipAddress             : sip:RtcApplication-dbf5142f-2bb2-4c4f-9531-b7fea45c5000@litware.com
        DisplayName            :
        DisplayNumber          :
        LineURI                :
        PrimaryLanguage        : 0
        SecondaryLanguages     : {}
        EnterpriseVoiceEnabled : True
        ExUmEnabled            : False
        Enabled                : True

如需詳細資訊，請參閱＜[Get-CsTrustedApplication](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsTrustedApplication)＞。

