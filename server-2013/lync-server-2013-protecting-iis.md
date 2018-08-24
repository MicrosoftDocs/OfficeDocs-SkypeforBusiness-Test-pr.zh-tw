---
title: Lync Server 2013：保護 IIS
TOCTitle: 在 Lync Server 2013 中保護 IIS
ms:assetid: a67171a6-6703-4e09-abb3-35d335bb674e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn518332(v=OCS.15)
ms:contentKeyID: 60471187
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中保護 IIS

 

_**上次修改主題的時間：** 2013-12-05_

在 Microsoft Office Communications Server 2007 及 Microsoft Office Communications Server 2007 R2 中，Internet Information Services (IIS) 是在標準使用者帳戶下執行。這可能會造成問題：如果密碼逾期，您可能會遺失您的 Web 服務，而此問題難以診斷。為協助避免逾期密碼的問題，Microsoft Lync Server 2013 讓您為非真實存在的電腦建立電腦帳戶，作為所有在網站中執行 IIS 之電腦的驗證主體。因為這些帳戶使用 Kerberos 驗證通訊協定，所以帳戶稱為 Kerberos 帳戶，而新的驗證處理序則稱為 Kerberos Web 驗證。 如此一來，您就能使用單一帳戶來管理所有 IIS 伺服器。

若要在此驗證主體下執行伺服器，您必須先使用 New-CsKerberosAccount Cmdlet 建立一個電腦帳戶，然後將此帳戶指派給一或多個站台。完成指派之後，可執行 Enable-CsTopology Cmdlet 來啟用帳戶與 Lync Server 2013 站台之間的關聯。除此之外，這也會在 Active Directory 網域服務 (AD DS) 中建立必要的服務主體名稱 (SPN)。SPN 可讓用戶端應用程式找到特定的服務。如需詳細資料，請參閱作業文件中的[New-CsKerberosAccount](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsKerberosAccount)。

## 最佳作法

為幫助增加 IIS 的安全性，建議您為 IIS 實作 Kerberos 帳戶。如果您不實作 Kerberos 帳戶，IIS 會在標準使用者帳戶之下執行。

