---
title: Lync Server 2013：授與設定權限
TOCTitle: 授與設定權限
ms:assetid: 15982bfe-6844-44f6-815a-72dcaf0e4d21
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398225(v=OCS.15)
ms:contentKeyID: 49290190
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中授與設定權限

 

_**上次修改主題的時間：** 2012-08-27_

您可使用 **Grant-CsSetupPermission** Cmdlet，新增 Read、Write、ReadSPN 和 WriteSPN 權限給特定 Active Directory 組織單位 (OU) 的 RTCUniversalServerAdmins 群組。接著，該 OU 的 RTCUniversalServerAdmins 群組成員可以將執行 Lync Server 2013 的伺服器安裝至指定網域，而不需要具備 Domain Admins 群組成員身分。

使用 **Test-CsSetupPermission** Cmdlet，可以驗證您以 **Grant-CsSetupPermission** Cmdlet 設定的權限。

您可使用 **Revoke-CsSetupPermission** Cmdlet，移除您以 **Grant-CsSetupPermission** Cmdlet 授與的權限。

## 授與安裝程式權限

1.  登入網域中您要授與安裝程式權限的 Lync Server 2013 電腦。如果 OU 位於不同的子網域，請使用 Domain Admins 群組或 Enterprise Admins 群組成員身分的帳戶。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  執行：
    
        Grant-CsSetupPermission -ComputerOu <DN of the OU or container where the computer objects that will run Lync Server reside > [-Domain <Domain FQDN>]
    
    您可將 ComputerOu 參數指定為相對於指定網域的預設命名內容 (例如 CN=computers)。或者，也可以將此參數指定為完整的 OU 辨別名稱 (DN) (例如 "CN=computers,DC=Contoso,DC=com")。若為後者，您指定的 OU DN 必須與所指定網域維持一致。
    
    如果不指定 Domain 參數，預設值為本機網域。

## 確認安裝程式權限

1.  登入網域中執行 Lync Server 2013 的電腦，您要確認這部電腦上先前使用 **Grant-CsSetupPermission** Cmdlet 授與的安裝程式權限。如果 OU 位於不同的子網域，請使用 Domain Admins 群組或 Enterprise Admins 群組成員身分的帳戶。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  執行：
    
        Test-CsSetupPermission -ComputerOu <DN of the OU or container where the computer objects that will run Lync Server reside> [-Domain <Domain FQDN>]
    
    您可將 ComputerOu 參數指定為相對於指定網域的預設命名內容 (例如 CN=computers)。或者，也可以將此參數指定為完整的 OU 辨別名稱 (DN) (例如 "CN=computers,DC=Contoso,DC=com")。若為後者，您指定的 OU DN 必須與所指定網域維持一致。
    
    如果不指定 Domain 參數，預設值為本機網域。

## 撤銷安裝程式權限

1.  登入網域中執行 Lync Server 2013 的電腦，您要撤銷這部電腦上先前使用 **Grant-CsSetupPermission** Cmdlet 授與的安裝程式權限。如果 OU 位於不同的子網域，請使用 Domain Admins 群組或 Enterprise Admins 群組成員身分的帳戶。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  執行：
    
        Revoke-CsSetupPermission -ComputerOu <DN of the OU or container where the computer objects that will run Lync Server reside > [-Domain <Domain FQDN>]
    
    您可將 ComputerOu 參數指定為相對於指定網域的預設命名內容 (例如 CN=computers)。或者，也可以將此參數指定為完整的 OU 辨別名稱 (DN) (例如 "CN=computers,DC=Contoso,DC=com")。若為後者，您指定的 OU DN 必須與所指定網域維持一致。
    
    如果不指定 Domain 參數，預設值為本機網域。

