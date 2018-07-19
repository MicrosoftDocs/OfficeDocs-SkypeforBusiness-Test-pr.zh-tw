---
title: Lync Server 2013：驗證行動性部署
TOCTitle: 驗證行動性部署
ms:assetid: 72f9b4d3-57b0-4705-9480-cfdca313a70c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690024(v=OCS.15)
ms:contentKeyID: 49291318
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中驗證行動性部署

 

_**上次修改主題的時間：** 2013-02-12_

    Some information in this topic pertains to Cumulative Updates for Lync Server 2013: February 2013.

部署 Lync Server Mobility Service 和 Lync Server 自動探索服務之後，執行測試交易，以確認部署運作正確。您可以執行 **Test-CsUcwaConference** 以測試兩位使用者使用 Lync 2013 Mobile 用戶端在會議中建立、加入與通訊的能力。若要使用此測試交易，您需要兩位實際或測試使用者，以及他們的完整認證。

您可以使用 **Test-CsMcxP2PIM** 以在使用 Lync 2010 Mobile 的兩位使用者之間測試傳送立即訊息。類似 **Test-CsUcwaConference**，您可以使用兩位實際使用者或兩個預先定義的測試使用者。

## 對 Lync 2013 Mobile 用戶端測試會議

1.  以 CsAdministrator 角色成員的身分登入任一部已安裝 Lync Server 管理命令介面和 Ocscore 的電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  在命令列中輸入：
    
        Test-CsUcwaConference -TargetFqdn <FQDN of Front End pool> -Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID> -OrganizerSipAddress sip:<SIP address of test user 1> -OrganizerCredential <test user 1 credentials> -ParticipantSipAddress sip:<SIP address of test user 2> -ParticipantCredential <test user 2 credentials> -v
    
    您可以在指令碼中設定認證，並將其傳遞至測試 Cmdlet。例如：
    
        $passwd1 = ConvertTo-SecureString "Password01" -AsPlainText -Force
        $passwd2 = ConvertTo-SecureString "Password02" -AsPlainText -Force
        $testuser1 = New-Object Management.Automation.PSCredential("contoso\UserName1", $passwd1)
        $testuser2 = New-Object Management.Automation.PSCredential("contoso\UserName2", $passwd2)
        Test-CsUcwaConference -TargetFqdn pool01.contoso.com -Authentication Negotiate -OrganizerSipAddress sip:UserName1@contoso.com -OrganizerCredential $testuser1 -ParticipantSipAddress sip:UserName2@contoso.com -ParticipantCredential $testuser2 -v

## 對 Lync 2010 Mobile 測試個人對個人立即訊息 (IM)

1.  以 CsAdministrator 角色成員的身分登入任一部已安裝 Lync Server 管理命令介面和 Ocscore 的電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  在命令列中輸入：
    
        Test-CsMcxP2PIM -TargetFqdn <FQDN of Front End pool> -Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID> -SenderSipAddress sip:<SIP address of test user 1> -SenderCredential <test user 1 credentials> -ReceiverSipAddress sip:<SIP address of test user 2> -ReceiverCredential <test user 2 credentials> -v
    
    您可以在指令碼中設定認證，並將其傳遞至測試 Cmdlet。例如：
    
        $passwd1 = ConvertTo-SecureString "Password01" -AsPlainText -Force
        $passwd2 = ConvertTo-SecureString "Password02" -AsPlainText -Force
        $tuc1 = New-Object Management.Automation.PSCredential("contoso\UserName1", $passwd1)
        $tuc2 = New-Object Management.Automation.PSCredential("contoso\UserName2", $passwd2)
        Test-CsMcxP2PIM -TargetFqdn pool01.contoso.com -Authentication Negotiate -SenderSipAddress sip:UserName1@contoso.com -SenderCredential $tuc1 -ReceiverSipAddress sip:UserName2@contoso.com -ReceiverCredential $tuc2 -v

## 請參閱

#### 其他資源

[Test-CsMcxP2PIM](https://docs.microsoft.com/en-us/powershell/module/skype/Test-CsMcxP2PIM)  
[Test-CsUcwaConference](https://docs.microsoft.com/en-us/powershell/module/skype/Test-CsUcwaConference)

