---
title: 建立或修改新的用戶端版本原則
TOCTitle: 建立或修改新的用戶端版本原則
ms:assetid: 4be6e449-aa82-4b46-abb1-d31281573a72
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ898476(v=OCS.15)
ms:contentKeyID: 52056122
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 建立或修改新的用戶端版本原則

 

_**上次修改主題的時間：** 2013-02-23_

您可以使用用戶端版本原則，以指定環境中支援的用戶端版本。使用用戶端版本設定有助於降低與支援多個用戶端版本相關的成本。這也能提昇整體的使用者體驗，因為當舊版與新版的用戶端互動時，可用的功能會受限於舊版的用戶端。您可以從 Lync Server 2013 控制台或 Lync Server 2013 管理命令介面，建立或修改用戶端版本原則。

## 使用 Lync Server 控制台建立或修改用戶端版本原則

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列，按一下 \[用戶端\]。
    
    > [!NOTE]  
    > 已預設選取 [用戶端版本原則] 索引標籤。
    


4.  在「用戶端版本原則」頁面上，執行下列其中一項動作：
    
      - 若要建立用戶端版本原則，請按一下 \[新增\]，選取 \[網站原則\]、\[集區原則\] 或 \[使用者原則\]，然後按一下 \[確定\]。
    
      - 若要修改全域原則或其他現有的用戶端版本原則，請選取原則，然後依序按一下 \[編輯\] 和 \[顯示詳細資料\]。

5.  在「編輯用戶端版本原則」頁面上建立或修改規則，如[建立或修改新的用戶端版本原則規則](lync-server-2013-create-or-modify-a-new-client-version-policy-rule.md)中所述。

## 使用 Windows PowerShell Cmdlet 建立或修改用戶端版本原則

您可以使用 **New-CsClientVersionPolicy** Cmdlet 建立用戶端版本原則，或使用 **set-csclientversionpolicy** Cmdlet 進行修改。可從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段執行這些 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 建立新的網站範圍用戶端版本原則

  - 下列命令會建立套用至 Redmond 網站的新用戶端版本原則。因為未指定其他參數，新原則將會使用預設的用戶端版本設定。
    
        New-CsClientVersionPolicy -Identity "site:Redmond"

## 建立新的個別使用者用戶端版本原則

  - 若要建立個別使用者原則，請使用類似下列的命令：
    
        New-CsClientVersionPolicy -Identity "RedmondClientVersionPolicy"

如需詳細資訊，請參閱＜[New-CsClientVersionPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsClientVersionPolicy)＞ Cmdlet 和＜[set-csclientversionpolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClientVersionPolicy)＞ Cmdlet 的說明主題。

