---
title: Lync Server 2013：為使用者啟用主控語音信箱
TOCTitle: 為使用者啟用主控語音信箱
ms:assetid: fa559f8f-ef99-43a1-b580-9e998b95efb8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413062(v=OCS.15)
ms:contentKeyID: 49292879
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中為使用者啟用主控語音信箱

 

_**上次修改主題的時間：** 2012-09-24_

請依照程序，在主控的 Exchange 整合通訊 (UM) 服務上，為 Lync Server 2013 使用者啟用語音信箱。

如需詳細資訊，請參閱規劃文件中的＜ [Lync Server 2013 中的主控 Exchange 使用者管理](lync-server-2013-hosted-exchange-user-management.md)＞。

如需 [Set-CsUser](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsUser) Cmdlet 的詳細資訊，請參閱 Lync Server 管理命令介面文件。

> [!IMPORTANT]  
> 在您可以為 Lync Server 2013 使用者啟用裝載的語音信箱之前，必須部署套用至其使用者帳戶的裝載語音信箱原則。如需詳細資訊，請參閱<a href="lync-server-2013-hosted-voice-mail-policies.md">Lync Server 2013 中的主控語音信箱原則</a>。



## 若要啟用使用者的裝載語音信箱

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  執行 Set-CsUser Cmdlet，為使用者帳戶設定裝載的語音信箱。例如，執行：
    
        Set-CsUser -HostedVoiceMail $True -Identity "contoso\kenmyer"
    
    上述範例會設定下列參數：
    
      - **HostedVoiceMail** 可允許將使用者的語音信箱通話路由傳送到裝載的 Exchange UM。它也會以訊號通知 Microsoft Lync 2013，以亮起「撥打語音信箱」指示燈。
    
      - **Identity** 會指定要修改的使用者帳戶。Identity 值可以使用下列任何格式來指定：
        
          - 使用者的 SIP 位址
        
          - 使用者的 Active Directory 使用者主體名稱
        
          - 使用者的網域\\登入名稱 (例如，contoso\\kenmyer)
        
          - 使用者的 Active Directory 網域服務顯示名稱 (例如，Ken Myer)。如果使用顯示名稱做為 Identity 值，您可以使用星號 (\*) 萬用字元。例如，若 Identity 為 "\* Smith"，則會傳回所有顯示名稱結尾為字串值 " Smith" 的使用者。
        
        > [!NOTE]  
        > 使用者的 Active Directory SAM 帳戶名稱無法當做 Identity 值使用，因為 SAM 帳戶名稱在樹系中不一定是唯一的。
        

