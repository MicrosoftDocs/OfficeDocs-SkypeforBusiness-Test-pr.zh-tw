---
title: Lync Server 2013：建立常設聊天室的網站原則
TOCTitle: 建立常設聊天室的網站原則
ms:assetid: 1327ff5c-b859-4010-a240-e0b2b084b5bd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204693(v=OCS.15)
ms:contentKeyID: 49290158
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建立常設聊天室的網站原則

 

_**上次修改主題的時間：** 2012-10-06_

您可以針對已部署的每個網站，建立網站特定的 常設聊天室原則。

網站原則中的設定會覆寫全域原則，但僅限於該網站原則所涵蓋的特定網站。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要設定和使用 常設聊天室伺服器，必須先使用 拓撲產生器將 常設聊天室伺服器 支援新增至拓撲，然後發布該拓撲。如需詳細資訊，請參閱部署文件中的＜ <a href="lync-server-2013-adding-persistent-chat-server-to-your-deployment.md">在 Lync Server 2013 中將常設聊天室伺服器新增至您的部署</a>＞。<br />
若要設定 常設聊天室伺服器 組態設定，請參閱部署文件中的＜ <a href="lync-server-2013-configure-persistent-chat-server-options-globally-or-for-persistent-chat-server-pool.md">在 Lync Server 2013 中以全域方式設定或針對常設聊天室伺服器集區設定常設聊天室伺服器選項</a>＞。</td>
</tr>
</tbody>
</table>


## 建立網站的 常設聊天室原則

1.  使用指派到 CsPersistentChatAdministrator、CsAdministrator 或 CsUserAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  從 \[開始\] 功能表選取 Lync Server 控制台或開啟瀏覽器視窗，然後輸入 Admin URL。如需各種 Lync Server 控制台啟動方法的詳細資訊，請參閱＜ [開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)＞。

3.  在左導覽列中，按一下 \[ 常設聊天室\] ，然後按一下 \[ 常設聊天室原則\] 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您也可以使用 Windows PowerShell Cmdlet。如需詳細資訊，請參閱部署移轉文件 <a href="configuring-persistent-chat-server-by-using-windows-powershell-cmdlets.md">使用 Windows PowerShell Cmdlet 設定常設聊天室伺服器</a>＞。</td>
    </tr>
    </tbody>
    </table>


4.  按一下 \[新增\] ，然後按一下 \[站台原則\] 。

5.  在 \[選取站台\] 中，按一下要套用該原則的網站。

6.  在 \[新增 常設聊天室原則\] ，執行下列動作：
    
      - 在 \[名稱\] 中，指定新網站原則的名稱 (例如，Redmond)。
    
      - 在 \[描述\] 中，提供網站原則的詳細資訊 (例如，Redmond 的聊天室原則)。
    
      - 若要控制未特別透過網站原則控制之所有網站的 常設聊天室，請選取或清除 \[啟用 常設聊天室\] 核取方塊。

7.  按一下 \[認可\] 。

