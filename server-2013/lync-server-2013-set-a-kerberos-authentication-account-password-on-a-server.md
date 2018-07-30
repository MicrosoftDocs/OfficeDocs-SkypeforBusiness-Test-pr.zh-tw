---
title: Lync Server 2013：在伺服器上設定 Kerberos 驗證帳戶密碼
TOCTitle: 在伺服器上設定 Kerberos 驗證帳戶密碼
ms:assetid: 902d3292-678d-4512-9248-586053cb638b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398734(v=OCS.15)
ms:contentKeyID: 49291655
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中於伺服器上設定 Kerberos 驗證帳戶密碼

 

_**上次修改主題的時間：** 2012-01-16_

若要順利完成此程序，您應以 RTCUniversalServerAdmins 群組成員的使用者身分登入。

您必須針對每個具有前端伺服器、Standard Edition Server 及 Director 的網站在 Kerberos 帳戶上設定密碼。您可以在網站內的伺服器 (如 前端伺服器) 上藉由執行 **Set-CsKerberosAccountPassword**  Windows PowerShell Cmdlet 來設定密碼。您必須為每個網站執行 **Set-CsKerberosAccountPassword** Cmdlet。此 Cmdlet 會為 Web 服務設定 Internet Information Services (IIS)，然後在 Active Directory 網域服務 中的電腦帳戶上設定密碼。替代方法 (須視 Cmdlet 搭配的參數而定) 是在使用已設定為 Kerberos 帳戶密碼之來源的電腦時，在另一部電腦上設定 IIS。

在使用 **Set-CsKerberosAccountPassword** Cmdlet 設定密碼時，Kerberos 會將密碼設定為隨機產生的字串。此 Cmdlet 會連絡所有 Lync Server 2013 中央網站內接受此帳戶指派的任何 IIS 執行個體。

## 若要設定 Kerberos 驗證帳戶的密碼

1.  以 RTCUniversalServerAdmins 群組成員的身分登入任一部已安裝 Lync Server 管理命令介面的網域電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  在命令提示字元中執行下列命令：
    
        Set-CsKerberosAccountPassword -UserAccount "Domain\UserAccount"
    
    例如：
    
        Set-CsKerberosAccountPassword -UserAccount "contoso\KerbAuth"
    
    > [!NOTE]  
    > 您必須使用 Domain\User 格式指定 UserAccount 參數。User@Domain.extension 格式不支援用來參考為 Kerberos 驗證程序所建立的電腦物件。
    
    
    > [!IMPORTANT]  
    > 對 Kerberos 驗證進行變更之後 (如新增帳戶或移除帳戶)，您必須從 Lync Server 管理命令介面 命令提示字元執行 <strong>Enable-CsTopology</strong>。
    

