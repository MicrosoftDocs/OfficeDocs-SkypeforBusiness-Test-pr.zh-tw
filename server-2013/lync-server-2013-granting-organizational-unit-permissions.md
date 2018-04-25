---
title: Lync Server 2013：授與組織單位權限
TOCTitle: 授與組織單位權限
ms:assetid: 95ee5ffa-39b1-4d80-87a2-27bb364f7396
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398763(v=OCS.15)
ms:contentKeyID: 49291732
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中授與組織單位權限

 

_**上次修改主題的時間：** 2012-05-14_

您可以使用 **Grant-CsOuPermission** Cmdlet 授與指定組織單位 (OU) 中的物件權限，如此一來，由樹系準備作業建立之 RTC 萬用群組的成員不需要成為 Domain Admins 群組成員即可存取物件。新增至指定 OU 的權限即是 **Enable-CsAdDomain** Cmdlet 在網域準備期間新增至電腦和使用者容器的權限。

使用 **Test-CsOuPermission** Cmdlet，可以驗證您以 **Grant-CsOuPermission** Cmdlet 設定的權限。

您可使用 **Revoke-CsOuPermission** Cmdlet，移除您以 **Grant-CsOuPermission** Cmdlet 授與的權限。

## 若要授與 OU 權限

1.  登入網域中要授與 OU 權限的 Lync Server 2013 電腦。如果 OU 位於不同的子網域，請使用 Domain Admins 群組或 Enterprise Admins 群組成員身分的帳戶。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  執行：
    
        Grant-CsOuPermission -ObjectType <User | Computer | InetOrgPerson | Contact | AppContact | Device> -OU <DN of the OU> [-Domain <Domain FQDN>]
    
    如果不指定 Domain 參數，預設值為本機網域。

## 若要驗證 OU 權限

1.  登入網域中要驗證以 **Grant-CsOuPermission** Cmdlet 授與 OU 權限的 Lync Server 2013 電腦。如果 OU 位於不同的子網域，請使用 Domain Admins 群組或 Enterprise Admins 群組成員身分的帳戶。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  執行：
    
        Test-CsOuPermission -ObjectType <User | Computer | InetOrgPerson | Contact | AppContact | Device> -OU <DN of the OU> [-Domain <Domain FQDN>]
    
    如果不指定 Domain 參數，預設值為本機網域。

## 若要撤銷 OU 權限

1.  登入網域中要撤銷以 **Grant-CsOuPermission** Cmdlet 授與 OU 權限的 Lync Server 2013 電腦。如果 OU 位於不同的子網域，請使用 Domain Admins 群組或 Enterprise Admins 群組成員身分的帳戶。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  執行：
    
        Revoke-CsOuPermission -ObjectType <User | Computer | InetOrgPerson | Contact | AppContact | Device> -OU <DN of the OU> [-Domain <Domain FQDN>]
    
    如果不指定 Domain 參數，預設值為本機網域。

