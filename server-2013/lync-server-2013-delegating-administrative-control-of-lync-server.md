---
title: Lync Server 2013：委派 Lync Server 管理控制
TOCTitle: 委派 Lync Server 2013 管理控制
ms:assetid: 0f378eff-8ef4-4c60-9fd2-67d7ee259ef8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg520951(v=OCS.15)
ms:contentKeyID: 49290106
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 委派 Lync Server 2013 管理控制

 

_**上次修改主題的時間：** 2013-02-22_

在 Lync Server 2013 中，會使用新的角色型存取控制 (RBAC) 功能將系統管理工作委派給使用者。當您安裝 Lync Server 時，會為您建立數個 RBAC 角色。這些角色會對應至 Active Directory 網域服務 中的萬用安全性群組；例如，RBAC 角色 CsHelpDesk 對應至在 Active Directory 網域服務的 \[使用者\] 容器中找到的 CsHelpDesk 群組。此外，每個 RBAC 角色會與一組 Lync ServerWindows PowerShell Cmdlet 產生關聯。這些 Cmdlet 代表已被指派指定 RBAC 角色的使用者可執行的工作。例如，CsHelpDesk 角色已被指派 Lock-CsClientPin 和 UnlockCsClientPin Cmdlet。這表示已被指派 CsHelpDesk 角色的使用者可以鎖定和解除鎖定使用者 PIN 號碼。但是，CsHelpDesk 角色尚未被指派 New-CsVoicePolicy Cmdlet。這表示已被指派 CsHelpDesk 角色的使用者無法建立新的語音原則。

## 檢視 RBAC 角色的相關資訊

您可以從 Lync Server 管理命令介面中執行下列命令，以擷取有關 RBAC 角色的基本資訊：

    Get-CsAdminRole

請記住，RBAC 角色的識別 (例如，CsVoiceAdministrator) 會直接對應至在 Active Directory 網域服務的 \[使用者\] 容器中找到的安全性群組。

若要檢視已指派給某個角色的 Cmdlet 清單，請使用類似下面的命令：

    Get-CsAdminRole -Identity "CsHelpDesk" | Select-Object -ExpandProperty Cmdlets

## 將 RBAC 角色指派給使用者

為了將 RBAC 角色指派給使用者，您必須將該使用者加入至適當的 Active Directory 安全性群組。例如，若要將 CsLocationAdministrator 角色指派給使用者，您必須將該使用者加入至 CsLocationAdministrator 群組。執行下列程序即可完成該作業：

**將使用者指派給安全性群組**

1.  使用有權修改 Active Directory 群組成員資格的帳戶，登入已安裝 \[Active Directory 使用者和電腦\] 的電腦。

2.  依序按一下 **\[開始\]** 、 **\[所有程式\]** 、 **\[系統管理工具\]** 和 **\[Active Directory 使用者和電腦\]** 。

3.  在 \[Active Directory 使用者和電腦\] 中，展開網域的名稱並按一下 **\[使用者\]** 容器。

4.  用滑鼠右鍵按一下 \[CsLocationAdministrator\] 安全性群組，然後按一下 \[內容\] 。

5.  在 **\[內容\]** 對話方塊的 **\[成員\]** 索引標籤上，按一下 **\[新增\]** 。

6.  在 **\[選取使用者、電腦、連絡人或群組\]** 對話方塊中，在 **\[輸入要選取的物件名稱\]** 方塊中輸入即將加入至群組之使用者的使用者名稱或顯示名稱 (例如， **Ken Myer** )，然後按一下 **\[確定\]** 。

7.  在 **\[內容\]** 對話方塊中，按一下 **\[確定\]** 。

若要驗證是否已指派 RBAC 角色，請使用 [Get-CsAdminRoleAssignment](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsAdminRoleAssignment) Cmdlet，將使用者的 SamAccountName (Active Directory 登入名稱) 傳遞給此 Cmdlet。例如，從 Lync Server 管理命令介面中執行此命令：

    Get-CsAdminRoleAssignment  -Identity "kenmyer"

