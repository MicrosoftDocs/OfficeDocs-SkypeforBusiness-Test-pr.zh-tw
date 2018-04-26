---
title: 停用 Enterprise Voice 的使用者
TOCTitle: 停用 Enterprise Voice 的使用者
ms:assetid: 462002d8-21df-4d77-bf7f-4d059d6a4bb2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688043(v=OCS.15)
ms:contentKeyID: 49890043
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 停用 Enterprise Voice 的使用者

 

_**上次修改主題的時間：** 2012-09-21_

請使用下列程序停用已啟用 Lync Server 2013 的使用者帳戶的企業語音。

## 停用企業語音的使用者帳戶

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[使用者\]**。

4.  在 **\[搜尋使用者\]** 方塊中，輸入全部或部分的顯示名稱、名字、姓氏、安全性帳戶管理員 (SAM) 帳戶名稱、SIP 位址或您想要啟用的使用者帳戶的線路統一資源識別元 (URI)，然後按一下 **\[尋找\]**。

5.  在表格中，按一下您想要啟用企業語音的使用者帳戶。

6.  在 **\[編輯\]** 功能表上，按一下 **\[顯示詳細資料\]**。

7.  在 **\[編輯 Lync Server 使用者\]** 頁面的 **\[電話語音\]** 下，按一下 **\[企業語音\]** 以外的任何選項。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果要限制使用者使用 Lync 撥打音訊或視訊電話，在 <strong>[電話語音]</strong> 下按一下 <strong>[音訊/視訊已停用]</strong>。</td>
    </tr>
    </tbody>
    </table>


8.  按一下 **\[認可\]**。

使用者現在無法使用企業語音功能。

## 請參閱

#### 工作

[在 Lync Server 2013 中為使用者啟用企業語音](lync-server-2013-enable-users-for-enterprise-voice.md)  

#### 其他資源

[管理使用者的 Enterprise Voice](lync-server-2013-managing-enterprise-voice-for-users.md)  
[Lync Server 管理命令介面](lync-server-2013-lync-server-management-shell.md)

