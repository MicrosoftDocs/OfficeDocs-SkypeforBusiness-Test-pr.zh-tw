---
title: 修改確定不受支援或不受限的用戶端的預設動作
TOCTitle: 修改確定不受支援或不受限的用戶端的預設動作
ms:assetid: 548dd0f5-62fe-4c3f-8952-2b9fd4c5fff3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg520994(v=OCS.15)
ms:contentKeyID: 49290942
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 修改確定不受支援或不受限的用戶端的預設動作

 

_**上次修改主題的時間：** 2013-02-23_

除了指定您希望自己的 Lync Server 2013 環境能夠支援的用戶端版本，您還可以針對尚未定義版本原則的用戶端指定預設動作。如此一來，您就可以限制自己的 Lync Server 環境中要使用哪些用戶端版本，以協助您控制支援多重用戶端版本的相關成本。

## 若要針對沒有明確支援或限制的用戶端修改其預設動作

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 **\[用戶端\]**、**\[用戶端版本設定\]**。

4.  在 **\[用戶端版本設定\]** 頁面上，按兩下清單裡的 **\[通用\]** 組態。

5.  在 **\[編輯用戶端版本設定\]** 對話方塊中，確認 **\[啟用版本控制\]** 核取方塊已經選取，然後在 **\[預設動作\]** 下方，選取下列其中一項：
    
      - **允許**   當用戶端版本與 **\[用戶端版本原則\]** 清單中的任何篩選條件不符時，允許用戶端登入。
    
      - **封鎖**   當用戶端版本與 **\[用戶端版本原則\]** 清單中的任何篩選條件不符時，防止用戶端登入。
    
      - **以 URL 封鎖**   當用戶端版本與 **\[用戶端版本原則\]** 清單中的任何篩選條件不符時，防止用戶端登入，並顯示一則錯誤訊息，內含可下載新版用戶端的 URL。
    
      - **以 URL 允許**   當用戶端版本與 **\[用戶端版本原則\]** 清單中的任何篩選條件不符時，允許用戶端登入，並顯示一則錯誤訊息，內含可下載新版用戶端的 URL。

6.  如果您選取 **\[以 URL 封鎖\]**，請輸入要包含在錯誤訊息中 **\[URL\]** 方塊的用戶端下載 URL。

7.  按一下 **\[認可\]**。

## 若要停用用戶端版本控制

  - 若要停用版本控制以允許所有用戶端使用任何用戶端版本登入，請清除 **\[啟用版本控制\]** 核取方塊，然後按一下 **\[認可\]**。

## 使用 Lync Server PowerShell Cmdlet 修改預設動作

當使用者嘗試使用用戶端版本原則並未明確支援或限制的用戶端進行登入時所採取的預設動作，也可以使用 Windows PowerShell 命令列介面和 **Set-CsClientVersionPolicy** Cmdlet 來管理。此 Cmdlet 可以從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段執行。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 將預設動作設定為封鎖存取

  - 下列命令會將 Redmond 網站的預設動作設定為 \[封鎖\]。這將會封鎖任何未包含用戶端版本設定規則之用戶端的登錄。
    
        Set-CsClientVersionConfiguration -Identity "site:Redmond" -DefaultAction Block

## 將預設動作設定為允許存取

  - 在此範例中，會將 Redmond 網站的預設動作設定為 \[允許\]。這將會允許任何未包含用戶端版本設定規則之用戶端的登錄。
    
        Set-CsClientVersionConfiguration -Identity "site:Redmond" -DefaultAction Allow

如需詳細資訊，請參閱 [Set-CsClientVersionPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClientVersionPolicy) Cmdlet 的說明主題。

## 請參閱

#### 其他資源

[在 Lync Server 2013 中管理裝置、電話及用戶端應用程式](lync-server-2013-managing-devices-phones-and-client-applications.md)

