---
title: Address Book Server Cmdlet
TOCTitle: Address Book Server Cmdlet
ms:assetid: 33da45da-3c57-4d04-9679-f0e5a0cfd37e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg415643(v=OCS.15)
ms:contentKeyID: 49290538
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Address Book Server Cmdlet

 

_**上次修改主題的時間：** 2012-06-26_

Address Book Server 是 Active Directory 網域服務與 Microsoft Lync Server 2013 之間的媒介。Address Book Server 可確保儲存在 Lync Server 2013 的使用者資訊會與儲存在 Active Directory 的使用者資訊同步。其作法是定期將 Address Book 檔案與使用者資料庫中儲存的資訊同步化。然後，Lync Server 包含一些 Cmdlet，可用來管理 Address Book Server。

## Address Book Server Cmdlet

不能在 Lync Server 控制台中進行 Address Book Server 設定。Windows PowerShell 是用來管理這些設定的主要工具。下表列出的 Cmdlet 與管理 Address Book Server 直接相關：

**Address Book Server**

  -   
    [Get-CsAddressBookConfiguration](get-csaddressbookconfiguration.md)

  -   
    [New-CsAddressBookConfiguration](new-csaddressbookconfiguration.md)

  -   
    [Remove-CsAddressBookConfiguration](remove-csaddressbookconfiguration.md)

  -   
    [Set-CsAddressBookConfiguration](set-csaddressbookconfiguration.md)

<!-- end list -->

  -   
    [Update-CsAddressBook](update-csaddressbook.md)

  -   
    [Debug-CsAddressBookReplication](debug-csaddressbookreplication.md)

<!-- end list -->

  -   
    [Test-CsAddressBookService](test-csaddressbookservice.md)

  -   
    [Test-CsAddressBookWebQuery](test-csaddressbookwebquery.md)

## 請參閱

#### 其他資源

[Lync Server PowerShell 部落格](http://go.microsoft.com/fwlink/?linkid=203150%26clcid=0x404)

