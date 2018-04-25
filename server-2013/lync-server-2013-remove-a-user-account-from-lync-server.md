---
title: 移除 Lync Server 的使用者帳戶
TOCTitle: 移除 Lync Server 的使用者帳戶
ms:assetid: 2f512aba-e358-45ae-af58-74312ee9c514
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688008(v=OCS.15)
ms:contentKeyID: 49889999
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移除 Lync Server 的使用者帳戶

 

_**上次修改主題的時間：** 2013-02-22_

您可以使用下列程序移除先前在 Lync Server 2013 中新增的使用者帳戶。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>移除使用者會造成您遺失該使用者的所有設定。若您要改為暫時停用使用者帳戶，請參閱此主題＜<a href="lync-server-2013-disable-or-re-enable-user-account-for-lync-server.md">停用或重新啟用 Lync Server 的使用者帳戶</a>＞。</td>
</tr>
</tbody>
</table>


## 移除 Lync Server 使用者帳戶 Lync Server

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[使用者\]。

4.  在 \[搜尋使用者\] 方塊中，輸入全部或部分的顯示名稱、名字、姓氏、安全性帳戶管理員 (SAM) 帳戶名稱、SIP 位址或您想要停用或重新啟用的使用者帳戶之線路統一資源識別元 (URI)，然後按一下 \[尋找\]。

5.  在表中按一下您想要移除的使用者帳戶。

6.  選取 \[動作\] 功能表中的 \[從 Lync Server 移除\]，隨即顯示對話方塊。

7.  選取對話方塊中的 \[確定\] 以移除使用者。

## 使用 Lync Server PowerShell Cmdlet 移除使用者帳戶

您也可以使用 Disable-CsUser Cmdlet 移除使用者帳戶。您可從 Lync Server 2013 管理命令介面，或從遠端工作階段 Windows PowerShell 執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 移除使用者帳戶

  - 若要移除使用者帳戶，請使用 Disable-CsUser Cmdlet。例如：
    
        Disable-CsUser -Identity "Ken Myer"
    
    執行此命令之後，將無法再重新啟用帳戶及其設定。所以請使用 Enable-CsUser Cmdlet 為 Ken Myer 建立新帳戶。

如需詳細資訊，請參閱 [Disable-CsUser](disable-csuser.md) Cmdlet 的說明主題。

## 請參閱

#### 工作

[停用或重新啟用 Lync Server 的使用者帳戶](lync-server-2013-disable-or-re-enable-user-account-for-lync-server.md)  

#### 其他資源

[啟用和停用 Lync Server 2013 使用者](lync-server-2013-enabling-and-disabling-users-for-lync-server.md)

