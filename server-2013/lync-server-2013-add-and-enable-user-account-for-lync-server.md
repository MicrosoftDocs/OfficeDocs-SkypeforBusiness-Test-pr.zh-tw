---
title: 新增並啟用 Lync Server 的使用者帳戶
TOCTitle: 新增並啟用 Lync Server 的使用者帳戶
ms:assetid: 1edd1c1c-307d-450b-abea-33aaf56bdf13
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg520961(v=OCS.15)
ms:contentKeyID: 49290294
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 新增並啟用 Lync Server 的使用者帳戶

 

_**上次修改主題的時間：** 2012-11-02_

在 \[Active Directory 使用者及電腦\] 中啟用使用者帳戶之後，您可使用 Lync Server 控制台建立新的 Lync Server 2013 使用者帳戶，方法是新增 Active Directory 使用者至 Lync Server。

## 若要新增並啟用新的 Lync Server 使用者

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[使用者\]**。

4.  按一下 **\[啟用使用者\]**。

5.  在 **\[新增 Lync Server 使用者\]** 對話方塊中，按一下 **\[新增\]**。

6.  在 \[搜尋使用者\] 方塊中，輸入您要找的 Active Directory 使用者帳戶的名稱、顯示名稱、名字、姓氏、安全性帳戶管理員 (SAM) 帳戶名稱、電子郵件地址、使用者主要名稱 (UPN) 或電話號碼的全部或頭幾個字，然後按一下 \[尋找\]。

7.  在表格中，選取您要加入至 Lync Server 的帳戶，然後按一下 \[確定\]。

8.  指派使用者至集區、指定其他詳細資料，並指派原則給您要的使用者，然後按一下 **\[啟用\]**。

## 請參閱

#### 工作

[停用或重新啟用 Lync Server 的使用者帳戶](lync-server-2013-disable-or-re-enable-user-account-for-lync-server.md)  
[移除 Lync Server 的使用者帳戶](lync-server-2013-remove-a-user-account-from-lync-server.md)  

#### 其他資源

[啟用和停用 Lync Server 2013 使用者](lync-server-2013-enabling-and-disabling-users-for-lync-server.md)

