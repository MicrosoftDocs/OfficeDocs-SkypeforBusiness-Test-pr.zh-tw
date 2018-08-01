---
title: Lync Server 2013：將常設聊天室原則套用至使用者或使用者群組
TOCTitle: 將常設聊天室原則套用至使用者或使用者群組
ms:assetid: 809ef4e0-8d42-4feb-b7c0-3995f39867a7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205038(v=OCS.15)
ms:contentKeyID: 49291481
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中將常設聊天室原則套用至使用者或使用者群組

 

_**上次修改主題的時間：** 2012-10-06_

如果對於 Lync Server 2013 啟用使用者，即可將適當的原則套用於特定使用者，以便對於 常設聊天室伺服器 啟用或停用使用者。

> [!NOTE]
> 若要設定和使用 常設聊天室伺服器，必須先使用 拓撲產生器將 常設聊天室伺服器 支援新增至拓撲，然後發布該拓撲。如需詳細資訊，請參閱部署文件中的＜ <a href="lync-server-2013-adding-persistent-chat-server-to-your-deployment.md">在 Lync Server 2013 中將常設聊天室伺服器新增至您的部署</a>＞。<br />
> 若要設定 常設聊天室伺服器 組態設定，請參閱部署文件中的＜ <a href="lync-server-2013-configure-persistent-chat-server-options-globally-or-for-persistent-chat-server-pool.md">在 Lync Server 2013 中以全域方式設定或針對常設聊天室伺服器集區設定常設聊天室伺服器選項</a>＞。


使用本主題中的程序，將先前建立的 常設聊天室 使用者原則套用至一或多個使用者帳戶或使用者群組。

## 將 常設聊天室 使用者原則套用至使用者帳戶

1.  使用指派到 CsPersistentChatAdministrator、CsAdministrator 或 CsUserAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  從 \[開始\] 功能表選取 Lync Server 控制台或開啟瀏覽器視窗，然後輸入 Admin URL。如需各種 Lync Server 控制台啟動方法的詳細資訊，請參閱＜ [開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)＞。

3.  在左導覽列中，按一下 \[使用者\] ，然後搜尋想要設定的使用者帳戶。

4.  在列出搜尋結果的表格中，依序按一下使用者帳戶、\[編輯\] 及 \[顯示詳細資料\] 。

5.  在 \[ 常設聊天室原則\] 的 \[編輯 Lync Server 使用者\] 中，選取要套用的 常設聊天室使用者原則。
    
    > [!NOTE]  
    > [&lt;自動&gt;] 設定套用預設有效原則。伺服器會自動套用這些設定。
    


6.  按一下 \[認可\] 。

