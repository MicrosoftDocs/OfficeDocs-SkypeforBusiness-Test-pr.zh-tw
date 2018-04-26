---
title: Lync Server 2013：Active Directory 基礎結構需求
TOCTitle: Active Directory 基礎結構需求
ms:assetid: c2086f7b-662f-4179-ab99-2c0311ebd903
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412955(v=OCS.15)
ms:contentKeyID: 49292209
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 的 Active Directory 基礎結構需求

 

_**上次修改主題的時間：** 2013-11-07_

在開始為 Lync Server 2013 準備 Active Directory 網域服務 的程序之前，請先確定您的 Active Directory 基礎結構符合下列先決條件：

  - 在您部署 Lync Server 的樹系中，所有網域控制站 (包括所有通用類別目錄伺服器) 都執行下列其中一個作業系統：
    
      - Windows Server 2012 R2 作業系統
    
      - Windows Server 2012 作業系統
    
      - Windows Server 2008 R2 作業系統
    
      - Windows Server 2008 作業系統
    
      - Windows Server 2008 Enterprise 32 位元
    
      - 32 位元或 64 位元版本的 Windows Server 2003 R2 作業系統
    
      - 32 位元或 64 位元版本的 Windows Server 2003 作業系統

  - 部署 Lync Server 的所有網域都提高到 Windows Server 2012 R2、 Windows Server 2012、 Windows Server 2008 R2、 Windows Server 2008，或至少 Windows Server 2003 的網域功能等級。

  - 部署 Lync Server 的樹系提高到 Windows Server 2012 R2、 Windows Server 2012、 Windows Server 2008 R2、 Windows Server 2008，或至少 Windows Server 2003 的樹系功能等級。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若要變更網域或樹系功能等級，請參閱 TechNet Library 中的＜提高網域與樹系功能等級＞，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=263775" class="uri">http://go.microsoft.com/fwlink/?linkid=263775</a>。</td>
    </tr>
    </tbody>
    </table>


  - 通用類別目錄會在您部署 Lync Server 電腦或使用者的每個網域中部署。

Lync Server 2013 支援 Windows Server 2012 R2、 Windows Server 2012、 Windows Server 2008 R2、 Windows Server 2008 和 Windows Server 2003 作業系統中的萬用群組。萬用群組的成員可以包括網域樹或樹系中任何網域的其他群組和帳戶，而且可以在網域樹狀目錄或樹系中的任何網域內獲指派權限。萬用群組支援加上系統管理員委派，可以簡化 Lync Server 部署的管理。例如，不需要為了讓系統管理員能夠同時管理兩個網域，而將一個網域新增至另一個網域。

