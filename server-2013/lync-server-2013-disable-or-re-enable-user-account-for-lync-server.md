---
title: 停用或重新啟用 Lync Server 的使用者帳戶
TOCTitle: 停用或重新啟用 Lync Server 的使用者帳戶
ms:assetid: 12497d00-f665-4a97-be68-854c5a8be4fc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg429696(v=OCS.15)
ms:contentKeyID: 49290143
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 停用或重新啟用 Lync Server 的使用者帳戶

 

_**上次修改主題的時間：** 2013-02-22_

您可以使用下列程序來停用先前在 Lync Server 2013 中啟用的使用者帳戶，而不會失去您為使用者帳戶設定的 Lync Server 設定。由於您並不會遺失 Lync Server 使用者帳戶設定，因此可以再次啟用先前啟用的使用者帳戶，而不需重新設定使用者帳戶。

## 停用或重新啟用先前啟用的 Lync Server 使用者帳戶

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[使用者\]**。

4.  在 **\[搜尋使用者\]** 方塊中，輸入全部或部分的顯示名稱、名字、姓氏、安全性帳戶管理員 (SAM) 帳戶名稱、SIP 位址或您想要停用或重新啟用的使用者帳戶之線路統一資源識別元 (URI)，然後按一下 **\[尋找\]**。

5.  按一下表中您想要停用或重新啟用的使用者帳戶。

6.  在 **\[動作\]** 功能表上，執行下列其中一項：
    
      - 若要暫時停用 Lync Server 2013 使用者帳戶，按一下 \[暫時停用 Lync Server\]。
    
      - 若要啟用 Lync Server 2013 使用者帳戶，按一下 \[重新啟用 Lync Server\]。

## 使用 Windows PowerShell Cmdlet 來停用及重新啟用使用者帳戶

使用者帳戶也可以利用 **Set-CsUser** Cmdlet 來暫時停用，然後再重新啟用。此 Cmdlet 可從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段執行。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 停用使用者帳戶

  - 若要暫時停用使用者帳戶，請將 Enabled 內容值設為 False ($False)。例如：
    
        Set-CsUser -Identity "Ken Myer" -Enabled $False

## 重新啟用使用者帳戶

  - 若要重新啟用已停用的使用者帳戶，請將 Enabled 內容值設為 True ($True)。例如：
    
        Set-CsUser -Identity "Ken Myer" -Enabled $True

如需詳細資訊，請參閱＜[Set-CsUser](set-csuser.md)＞Cmdlet 的說明主題。

## 請參閱

#### 工作

[新增並啟用 Lync Server 的使用者帳戶](lync-server-2013-add-and-enable-user-account-for-lync-server.md)  

#### 其他資源

[啟用和停用 Lync Server 2013 使用者](lync-server-2013-enabling-and-disabling-users-for-lync-server.md)

