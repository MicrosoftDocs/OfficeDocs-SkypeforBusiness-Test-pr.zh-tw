---
title: Lync Server 2013：將外部使用者存取原則指派給擁有 Lync 功能的使用者
TOCTitle: 將外部使用者存取原則指派給擁有 Lync 功能的使用者
ms:assetid: 736fcaad-9f95-4896-b767-e199d86a00a4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398551(v=OCS.15)
ms:contentKeyID: 49291313
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中將外部使用者存取原則指派給擁有 Lync 功能的使用者

 

_**上次修改主題的時間：** 2013-02-22_

如果已啟用使用者的 Lync Server，則將適當的原則套用至特定使用者，就可以在 Lync Server 控制台中設定 SIP 同盟、XMPP 同盟、遠端使用者存取及公用立即訊息 (IM) 連線。例如，如果您已建立原則來支援遠端使用者存取，則必須先將它套用至一個使用者，該使用者才能從遠端位置連線至 Lync Server，以及與遠端位置的內部使用者共同作業。

> [!NOTE]  
> 若要支援外部使用者存取，您必須啟用想要支援之每種外部使用者存取類型的支援，以及設定適當原則及其他控制使用的選項。如需詳細資訊，請參閱部署文件中的 <a href="lync-server-2013-configuring-support-for-external-user-access.md">在 Lync Server 2013 中設定外部使用者存取支援</a> 或作業文件中的 <a href="lync-server-2013-managing-federation-and-external-access-to-lync-server-2013.md">管理 Lync Server 2013 的同盟與外部存取</a>。



使用本主題中的程序，將先前建立的外部使用者存取原則套用至一或多個使用者帳戶。

## 將外部使用者原則套用至使用者帳戶

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[使用者\] ，然後搜尋想要設定的使用者帳戶。

4.  在列出搜尋結果的表格中，依序按一下使用者帳戶、\[編輯\] 及 \[顯示詳細資料\] 。

5.  在 **\[外部存取原則\]** 的 **\[編輯 Lync Server 使用者\]** 下，選取想要套用的使用者原則。
    
    > [!NOTE]  
    > <strong>[&lt;自動&gt;]</strong> 設定套用預設伺服器或全域原則設定。
    


## 使用 Windows PowerShell Cmdlet 指派每個使用者的外部存取原則

可使用 Windows PowerShell 及 Grant-CsExternalAccessPolicy Cmdlet 來指派個別使用者的外部存取原則。可從 Lync Server 2013 管理命令介面 或 Windows PowerShell 遠端工作階段執行此Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 指派每個使用者外部存取原則給單一使用者

  - 此命令可將個別使用者外部存取原則 RedmondExternalAccessPolicy 指派給使用者 Ken Myer。
    
        Grant-CsExternalAccessPolicy -Identity "Ken Myer" -PolicyName "RedmondExternalAccessPolicy"

## 指派每個使用者外部存取原則給多位使用者

  - 此命令可將個別使用者外部存取原則 USAExternalAccessPolicy，指派給所有具有 Active Directory 中之 UnitedStates OUto 帳戶的使用者。如需有關此項命令之 OU 參數的詳細資訊，請參閱文件以了解 [Get-CsUser](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsUser) Cmdlet。
    
        Get-CsUser -OU "ou=UnitedStates,dc=litwareinc,dc=com" | Grant-CsExternalAccessPolicy -PolicyName "USAExternalAccessPolicy"

## 取消指派每個使用者外部存取原則

  - 此命令可將任何先前指派給 Ken Myer 的個別使用者外部存取原則予以解除指派。一旦解除指派個別使用者原則，即會自動使用全域原則或其本機網站原則 (如果存在的話) 來管理 Ken Myer。網站原則的優先順序高於全域原則。
    
        Grant-CsExternalAccessPolicy -Identity "Ken Myer" -PolicyName $Null

如需詳細資訊，請參閱 [Grant-CsExternalAccessPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Grant-CsExternalAccessPolicy) Cmdlet 的說明主題。

