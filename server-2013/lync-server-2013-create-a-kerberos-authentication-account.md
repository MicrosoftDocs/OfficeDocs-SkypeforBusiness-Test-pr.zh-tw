---
title: Lync Server 2013：建立 Kerberos 驗證帳戶
TOCTitle: 建立 Kerberos 驗證帳戶
ms:assetid: 63f0cef6-562a-4209-ae25-71f8dc7c7295
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398449(v=OCS.15)
ms:contentKeyID: 49291123
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建立 Kerberos 驗證帳戶

 

_**上次修改主題的時間：** 2012-01-02_

若要順利完成此程序，則最少應該以 Domain Admins 群組成員的身分登入伺服器或網域。

您可以建立每個網站的 Kerberos 驗證帳戶，也可以建立單一 Kerberos 驗證帳戶，並將它用於所有網站。您可以使用 Windows PowerShell Cmdlet 來建立及管理帳戶 (包括識別指派給每個網站的帳戶)。 拓撲產生器及 Lync Server 2013 控制台不會顯示 Kerberos 驗證帳戶。使用下列程序，建立一或多個要用於進行 Kerberos 驗證的使用者帳戶。

## 建立 Kerberos 帳戶

1.  以 Domain Admins 群組成員身分，登入執行 Lync Server 2013 之網域中的電腦，或登入已安裝系統管理工具的電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  從命令列中，執行下列命令：
    
        New-CsKerberosAccount -UserAccount "Domain\UserAccount" -ContainerDN "CN=Users,DC=DomainName,DC=DomainExtension"
    
    例如：
    
        New-CsKerberosAccount -UserAccount "Contoso\KerbAuth" -ContainerDN "CN=Users,DC=contoso,DC=com"

4.  開啟 \[Active Directory 使用者和電腦\] 確認已建立 \[電腦\] 物件，並展開 **\[使用者\]** 容器，然後確認使用者帳戶的 \[電腦\] 物件位在該容器內。

