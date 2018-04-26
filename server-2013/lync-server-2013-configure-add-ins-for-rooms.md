---
title: Lync Server 2013：為聊天室設定增益集
TOCTitle: 為聊天室設定增益集
ms:assetid: 4eeaf19e-8369-4f6f-af65-a283cf7daa1c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204878(v=OCS.15)
ms:contentKeyID: 49290880
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中為聊天室設定增益集

 

_**上次修改主題的時間：** 2013-02-21_

在 Lync Server 2013 控制台中，您可以使用 **\[ 常設聊天室\]** 頁面的 **\[增益集\]** 區段來建立 URL 與 常設聊天室聊天室的關聯。這些 URL 會顯示在交談擴充性窗格的聊天室的 Lync 2013 用戶端中。系統管理員必須將增益集新增至註冊增益集清單中，而聊天室管理員/建立者必須建立聊天室與其中一個註冊增益集的關聯，使用者才能在他們的 Lync 2013 用戶端中看到此升級。

增益集可擴充聊天室體驗。常見的增益集有包含指向 Silverlight 應用程式的 URL，在股票行情指示器張貼到聊天室時加以攔截，以在擴充性窗格中顯示股票行情記錄。其他範例還包括在聊天室中嵌入 OneNote 2013 URL 做為增益集，以包含一些分享內容，例如「第一印象」或「本日熱門話題」。

## 設定聊天室的增益集

1.  使用指派給 CsPersistentChatAdministrator 或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任一部電腦。

2.  從 \[開始\] 功能表選取 Lync Server 控制台或開啟瀏覽器視窗，然後輸入 Admin URL。如需各種 Lync Server 控制台啟動方法的詳細資訊，請參閱＜ [開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)＞。
    
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


3.  在左導覽列中，按一下 **\[ 常設聊天室\]** ，然後按一下 **\[增益集\]** 。
    
    如有多個 Persistent Chat Server 集區部署，則從下拉式清單中選取適當的集區。

4.  在 **\[增益集\]** 頁面上，按一下 **\[新增\]** 。

5.  在 **\[選取服務\]** 中，選取對應至需要建立增益集的 Persistent Chat Server 集區的服務。增益集不得從一個集區移動到另一個集區，或是在不同集區之間共用。

6.  在 **\[新增增益集\]** 中，執行下列動作：
    
      - 在 **\[名稱\]** 中，指定新增益集的名稱。
    
      - 在 **\[URL\]** 中，指定要與增益集建立關聯的 URL。URL 限於 http 和 https 通訊協定。

7.  按一下 \[認可\] 。

## 請參閱

#### 工作

[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)  

#### 概念

[使用 Windows PowerShell Cmdlet 設定常設聊天室伺服器](configuring-persistent-chat-server-by-using-windows-powershell-cmdlets.md)

