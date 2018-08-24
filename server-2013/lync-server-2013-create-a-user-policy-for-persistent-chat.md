---
title: Lync Server 2013：建立常設聊天室的使用者原則
TOCTitle: 建立常設聊天室的使用者原則
ms:assetid: aa3774af-d442-4206-8a68-2fbb9102e9d6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205170(v=OCS.15)
ms:contentKeyID: 49291968
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建立常設聊天室的使用者原則

 

_**上次修改主題的時間：** 2012-10-06_

在 Lync Server 控制台的 \[使用者\] 中，您可定義可以指派給使用者的使用者原則。

使用者原則優先於全域與網站原則，但僅限於對其指派該使用者原則的特定使用者。

> [!NOTE]
> 若要設定和使用 常設聊天室伺服器，必須先使用 拓撲產生器將 常設聊天室伺服器 支援新增至拓撲，然後發布該拓撲。如需詳細資訊，請參閱部署文件中的＜ <a href="lync-server-2013-adding-persistent-chat-server-to-your-deployment.md">在 Lync Server 2013 中將常設聊天室伺服器新增至您的部署</a>＞。<br />
> 若要設定 常設聊天室伺服器 組態設定，請參閱部署文件中的＜ <a href="lync-server-2013-configure-persistent-chat-server-options-globally-or-for-persistent-chat-server-pool.md">在 Lync Server 2013 中以全域方式設定或針對常設聊天室伺服器集區設定常設聊天室伺服器選項</a>＞。


## 建立 常設聊天室的使用者原則

1.  使用指派到 CsPersistentChatAdministrator、CsAdministrator 或 CsUserAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  從 \[開始\] 功能表選取 Lync Server 控制台或開啟瀏覽器視窗，然後輸入 Admin URL。如需各種 Lync Server 控制台啟動方法的詳細資訊，請參閱＜ [開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)＞。
    
    > [!IMPORTANT]  
    > 您也可以使用 Windows PowerShell Cmdlet。請參閱部署文件中的＜ <a href="configuring-persistent-chat-server-by-using-windows-powershell-cmdlets.md">使用 Windows PowerShell Cmdlet 設定常設聊天室伺服器</a>＞。
    


3.  在左導覽列中，按一下 \[ 常設聊天室\] ，然後按一下 \[ 常設聊天室原則\] 。

4.  按一下 \[新增\] ，然後按一下 \[使用者原則\] 。

5.  在 \[新增 常設聊天室原則\] ，執行下列動作：
    
      - 在 \[名稱\] 中，指定新使用者原則的名稱。
    
      - 在 \[描述\] 中，提供使用者原則的詳細資訊 (例如，特定使用者的 常設聊天室原則)。
    
      - 若要針對未透過使用者原則特別控制的所有使用者控制 常設聊天室，請選取或移除 \[啟用 常設聊天室\] 核取方塊。

6.  按一下 \[認可\] 。

