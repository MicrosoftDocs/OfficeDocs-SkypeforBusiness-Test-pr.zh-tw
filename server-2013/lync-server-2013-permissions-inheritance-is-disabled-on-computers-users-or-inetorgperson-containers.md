---
title: Lync Server 2013：Computers、Users 或 InetOrgPerson 容器已停用權限繼承
TOCTitle: Computers、Users 或 InetOrgPerson 容器已停用權限繼承
ms:assetid: c472ad21-a93d-4fcb-a3d9-60a2134a87fa
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412970(v=OCS.15)
ms:contentKeyID: 49292248
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Computers、Users 或 InetOrgPerson 容器已停用權限繼承

 

_**上次修改主題的時間：** 2014-12-19_

在鎖定的 Active Directory 網域服務 中，User 及 Computer 物件經常會以停用權限繼承的方式置於特定的組織單位 (OU) 中，以保護系統管理委派的安全性，並允許使用群組原則物件 (GPO) 強制執行安全性原則。

網域準備和伺服器啟動會設定 Lync Server 2013 所需的存取控制項目 (ACE)。在停用權限繼承的情況下， Lync Server 安全性群組無法繼承這些 ACE。一旦無法繼承這些權限， Lync Server 安全性群組便無法存取設定，因此會產生下列兩個問題：

  - 若要管理 User、InetOrgPerson、Contact 並運作伺服器，則 Lync Server 安全性群組會要求每個使用者的屬性集、Real-time Communications (RTC)、RTC 使用者搜尋和公用資訊上都必須具備網域準備程序所設定的 ACE。在停用權限繼承的情況下，安全性群組無法繼承這些 ACE，因此無法管理伺服器或使用者。

  - 若要探索伺服器和集區，執行 Lync Server 的伺服器必須依賴電腦相關物件 (包括 Microsoft Container 和 Server 物件) 啟動時所設定的 ACE。在停用權限繼承的情況下，安全性群組、伺服器和集區無法繼承這些 ACE，因此無法利用這些 ACE。

為解決這些問題， Lync Server 提供 **Grant-CsOuPermission** Cmdlet。此 Cmdlet 會直接在指定的容器和組織單位以及容器或組織單位內的物件上，設定必要的 Lync Server ACE。

## 執行網域準備之後，在 User、InetOrgPerson 和 Contact 物件上設定權限

在鎖定的 Active Directory 環境中，如果已停用權限繼承，網域準備便不會針對網域內保有 User 或 InetOrgPerson 物件之容器或組織單位設定必要的 ACE。 在此情況下，您必須在每個包含 User 或 InetOrgPerson 物件的容器或 OU (其中已停用權限繼承) 上，執行 **Grant-CsOuPermission** Cmdlet。 如果您擁有中央樹系拓撲，也必須對包含 Contact 物件的容器或 OU 執行此程序。如需中央樹系拓撲的詳細資訊，請參閱＜支援能力＞文件中的 [Lync Server 2013 中支援的 Active Directory 拓撲](lync-server-2013-supported-active-directory-topologies.md)。ObjectType 參數會指定物件類型。OU 參數會指定組織單位。

這個 Cmdlet 會直接在指定的容器或 OU，以及容器內的 User 或 InetOrgPerson 物件上新增必要的 ACE。

您需要有相當於 Domain Admins 群組成員資格的使用者權限，才能執行此 Cmdlet。如果已驗證的使用者 ACE 也已經從鎖定環境中移除，您必須將樹系根網域中相關容器或 OU 的讀取存取 ACE 授與此帳戶 (如 [Lync Server 2013 中已移除已驗證使用者權限](lync-server-2013-authenticated-user-permissions-are-removed.md)中所述)，或使用屬於 Enterprise Admins 群組成員的帳戶。

**若要針對 User、InetOrgPerson 與 Contact 物件設定所需的 ACE**

1.  以屬於 Domain Admins 群組成員的帳戶或具備同等使用者權限的帳戶，登入已加入網域的電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  執行：
    
        Grant-CsOuPermission -ObjectType <User | Computer | InetOrgPerson | Contact | AppContact | Device> 
        -OU <DN name for the OU container relative to the domain root container DN> [-Domain <Domain FQDN>]
    
    如果不指定 Domain 參數，預設值為本機網域。
    
    例如：
    
        Grant-CsOuPermission -ObjectType "User" -OU "cn=Redmond,dc=contoso,dc=net" -Domain "contoso.net"

4.  在記錄檔中，尋找每個工作結尾的 **\<成功\>** \[執行結果\]，以確認權限已設定，然後關閉記錄視窗。或者，您可以執行下列命令，來判斷是否已經設定權限：
    
        Test-CsOuPermission -ObjectType <type of object> 
        -OU <DN name for the OU container relative to the domain root container DN> 
        [-Domain <Domain FQDN>] [-Report <fully qualified path and name of file to create>]
    
    例如：
    
        Test-CsOuPermission -ObjectType "User" -OU "cn=Redmond,dc=contoso,dc=net" -Domain "contoso.net" -Report "C:\Log\OUPermissionsTest.html"

## 執行網域準備之後，設定 Computer 物件的權限

在鎖定的 Active Directory 環境中，如果停用權限繼承，網域準備便不會針對網域內保有 Computer 物件之容器或 OU 設定必要的 ACE。在此情況下，您必須在每個包含執行 Lync Server 之電腦的容器或 OU (其中已停用權限繼承) 上，執行 **Grant-CsOuPermission** Cmdlet。ObjectType 參數會指定物件類型。

此程序會直接在指定容器上新增必要的 ACE。

您需要有相當於 Domain Admins 群組成員資格的使用者權限，才能執行此 Cmdlet。如果已驗證的使用者 ACE 也已經移除，您必須將樹系根網域中相關容器的讀取存取 ACE 授與此帳戶 (如 [Lync Server 2013 中已移除已驗證使用者權限](lync-server-2013-authenticated-user-permissions-are-removed.md)中所述)，或使用屬於 Enterprise Admins 群組成員的帳戶。

**若要針對 Computer 物件設定所需的 ACE**

1.  以屬於 Domain Admins 群組成員的帳戶或具備同等使用者權限的帳戶，登入網域電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  執行：
    
        Grant-CsOuPermission -ObjectType <Computer> 
        -OU <DN name for the computer OU container relative to the domain root container DN> 
        [-Domain <Domain FQDN>][-Report <fully qualified path and name of output report>]
    
    如果不指定 Domain 參數，預設值為本機網域。
    
    例如：
    
        Grant-CsOuPermission -ObjectType "Computer" -OU "ou=Lync Servers,dc=litwareinc,dc=com" -Report "C:\Logs\OUPermissions.xml"

4.  在範例記錄檔 C:\\Logs\\OUPermissions.xml 中，尋找每個工作結尾的 **\<成功\>** \[執行結果\]，並確認沒有錯誤，然後關閉記錄。您可以執行下列 Cmdlet 來測試權限：
    
        Test-CsOuPermission -ObjectType <type of object> 
        -OU <DN name for the OU container relative to the domain root container DN> [-Domain <Domain FQDN>]
    
    例如：
    
        Test-CsOuPermission -ObjectType "user","contact" -OU "cn=Bellevue,dc=contoso,dc=net" -Domain "contoso.net"
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果在已鎖定 Active Directory 的環境中，於樹系根網域上執行網域準備，請記住 Lync Server 要求存取 Active Directory 架構和設定容器。<br />
    如果預設的已驗證使用者權限已從 AD DS 的架構或設定容器中移除，則只允許 (架構容器的) Schema Admins 群組或 (設定容器的) Enterprise Admins 群組的成員存取指定的容器。因為 Setup.exe、 Lync Server 管理命令介面 Cmdlet 和 Lync Server 控制台需要有這些容器的存取權，因此，除非執行安裝的使用者擁有相當於 Schema Admins 及 Enterprise Admins 群組成員資格的使用者權限，否則無法設定及安裝系統管理工具。<br />
    若要補救這種狀況，您必須將 RTCUniversalGlobalWriteGroup 群組的讀取和寫入權限授與架構和設定容器。</td>
    </tr>
    </tbody>
    </table>

