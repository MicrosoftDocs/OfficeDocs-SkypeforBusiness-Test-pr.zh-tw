---
title: Lync Server 2013：設定常設聊天室的全域原則
TOCTitle: 設定常設聊天室的全域原則
ms:assetid: 6176eb5c-19de-4c07-bcc0-2e38f8965966
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204951(v=OCS.15)
ms:contentKeyID: 49291095
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定常設聊天室的全域原則

 

_**上次修改主題的時間：** 2012-10-06_

您可以單獨使用預設的全域原則，針對部署中所有的使用者啟用 常設聊天室設定。您也可以指定網站及使用者的其他原則，以控制是否啟用或停用特定使用者及網站的 常設聊天室。

您無法刪除全域原則。如果您嘗試刪除，則設定會重設為預設值。

> [!NOTE]
> 若要設定和使用 常設聊天室伺服器，必須先使用 拓撲產生器將 常設聊天室伺服器 支援新增至拓撲，然後發布該拓撲。如需詳細資訊，請參閱部署文件中的＜ <a href="lync-server-2013-adding-persistent-chat-server-to-your-deployment.md">在 Lync Server 2013 中將常設聊天室伺服器新增至您的部署</a>＞。<br />
> 若要設定 常設聊天室伺服器 組態設定，請參閱部署文件中的＜ <a href="lync-server-2013-configure-persistent-chat-server-options-globally-or-for-persistent-chat-server-pool.md">在 Lync Server 2013 中以全域方式設定或針對常設聊天室伺服器集區設定常設聊天室伺服器選項</a>＞。


## 設定 常設聊天室的全域原則

1.  使用指派到 CsPersistentChatAdministrator、CsAdministrator 或 CsUserAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  從 **\[開始\]** 功能表，選取 \[ Lync Server 控制台\] 或開啟瀏覽器視窗，然後輸入管理 URL。如需有關用於啟動 Lync Server 控制台之不同方法的詳細資訊，請參閱作業文件中的 [開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。
    
    > [!IMPORTANT]  
    > 也可以使用 Windows PowerShell Cmdlet。如需詳細資訊，請參閱部署文件中的 <a href="configuring-persistent-chat-server-by-using-windows-powershell-cmdlets.md">使用 Windows PowerShell Cmdlet 設定常設聊天室伺服器</a>。
    


3.  在 \[ Lync Server 控制台\] 中，按一下 **\[ 常設聊天室\]** ，然後按一下 **\[ 常設聊天室原則\]** 。

4.  按一下原則清單中的 **\[通用\]** ，並按一下 **\[編輯\]** ，然後按一下 **\[顯示詳細資料\]** 。

5.  在 \[編輯 常設聊天室原則 - 通用\] 中，執行下列動作：
    
      - 如果您不想要使用預設值 \[通用\]，請在 **\[名稱\]** 中指定全域原則的新名稱。
    
      - 在 \[描述\] 中，提供使用者原則的詳細資訊 (例如，*centralSiteName* 的全域原則)。
    
      - 若要控制所有未受特定網站原則或使用者原則控制之網站與使用者的 常設聊天室，請選取或清除 \[啟用 常設聊天室\] 核取方塊。

6.  按一下 \[認可\] 。

