---
title: 檢視會議組態設定
TOCTitle: 檢視會議組態設定
ms:assetid: d03a4684-9d8b-4728-917d-5b5c91511e2c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721894(v=OCS.15)
ms:contentKeyID: 49890324
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 檢視會議組態設定

 

_**上次修改主題的時間：** 2013-02-23_

在 Lync Server 2013 控制台 中，您可以使用會議組態設定，控制如何在部署中實作會議。這包括下列會議設定：

  - 當您部署 Lync Server 2013 時，預設會建立全域設定。

  - 選用的網站層級與使用者層級設定可讓您建立和用以指定特定網站或使用者如何實作會議。

## 檢視會議組態設定

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 \[會議\]，然後按一下 \[會議設定\]。

4.  在 \[會議設定\] 頁面上，按一下您要檢視的會議設定。

5.  在 \[編輯檔案篩選器\] 中，選取 \[顯示詳細資料...\] 核取方塊。
    
    \[編輯會議設定 - \<原則\>\] 隨即開啟，顯示選取原則的設定。如需進行設定的詳細資訊，請參閱＜[建立或修改會議的組態設定集合](lync-server-2013-create-or-modify-a-collection-of-meeting-configuration-settings.md)＞。

## 使用 Lync Server PowerShell Cmdlet 檢視會議設定資訊

您也可以使用 Lync Server PowerShell 與 Get-CsMeetingConfiguration Cmdlet 來檢視會議組態設定。此 Cmdlet 可以從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段執行。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 檢視會議設定資訊

  - 若要檢視所有會議組態設定的相關資訊，請在 Lync Server 管理命令介面輸入下列命令，然後按 ENTER：
    
        Get-CsMeetingConfiguration
    
    將會傳回類似如下的資訊：
    
        Identity                        : Global
        PstnCallersBypassLobby          : True
        EnableAssignedConferenceType    : True
        DesignateAsPresenter            : Company
        AssignedConferenceTypeByDefault : True
        AdmitAnonymousUsersByDefault    : True
        RequireRoomSystemsAuthorization : False
        LogoURL                         :
        LegalURL                        :
        HelpURL                         :
        CustomFooterText                :
        AllowConferenceRecording        : True

如需詳細資訊，請參閱 [Get-CsMeetingConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsMeetingConfiguration) Cmdlet 的說明主題。

