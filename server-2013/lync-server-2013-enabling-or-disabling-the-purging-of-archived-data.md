---
title: 啟用或停用清除封存資料
TOCTitle: 啟用或停用清除封存資料
ms:assetid: 28cef09f-0970-4fc3-8315-f26689e3e187
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg520968(v=OCS.15)
ms:contentKeyID: 49290396
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 啟用或停用清除封存資料

 

_**上次修改主題的時間：** 2013-02-23_

在 Lync Server 2013 控制台中，您可以使用封存組態啟用及停用清除，並設定實作清除的方式。這包含下列封存組態：

  - 當您部署 Lync Server 2013 時，預設會建立全域組態。

  - 選用的網站層級與集區層級組態，是您可加以建立及用於指定如何實作特定網站或集區的封存。

您會在部署封存時，先設定封存組態，但您可以在部署之後進行變更、新增及刪除組態。如需如何實作封存組態的詳細資訊，包括您可以指定哪些選項以及封存組態的階層，請參閱規劃文件、部署文件或作業文件中的＜[在 Lync Server 2013 中封存的運作方式](lync-server-2013-how-archiving-works.md)＞。

> [!NOTE]
> 若要針對位於 Lync Server 2013 的使用者使用封存，必須設定封存原則以指定是否要啟用內部或外部通訊的封存，或是兩者皆啟用。預設並沒有啟用內部或外部通訊的封存。以任何原則啟用封存之前，您應先為部署指定適用的封存組態，然後如上一節中所述，選用地針對網站與集區指定封存組態。如需啟用封存的詳細資訊，請參閱部署文件中的＜<a href="lync-server-2013-configuring-and-assigning-archiving-policies.md">設定和指派封存原則</a>＞。<br />
> 若您決定在部署封存之後要使用 Microsoft Exchange 整合以將封存資料及檔案儲存在 Exchange 2013 伺服器，且您的所有使用者均位於 Exchange 2013 伺服器，則您應從拓撲移除 SQL Server 資料庫組態。您必須使用拓撲產生器執行此動作。如需詳細資訊，請參閱作業文件中的＜<a href="lync-server-2013-changing-archiving-database-options.md">在 Lync Server 2013 中變更封存資料庫選項</a>＞。


## 啟用或停用封存的清除功能

1.  使用指派給 CsArchivingAdministrator 或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左側導覽列中，依序按一下 \[監控和封存\]及 \[封存組態\]。

4.  按一下封存組態清單中適當的全域、網站或集區組態名稱，再依序按一下 \[編輯\] 和 \[顯示詳細資料\]，然後執行下列作業：
    
      - 若要啟用清除，請選取 **\[啟用封存資料的清除\]** 核取方塊，然後執行下列其中一項：
        
          - 若要清除所有記錄，請按一下 **\[在最大持續期限 (天) 後清除匯出的封存資料和儲存的封存資料\]**，然後指定天數。
        
          - 若只要清除已匯出的資料，請按一下 **\[只清除匯出的封存資料\]**。
    
      - 若要停用清除，請清除 **\[啟用封存資料的清除\]** 核取方塊。

5.  按一下 **\[認可\]**。

## 使用 Lync Server 管理命令介面 Cmdlet 啟用及停用封存資料的清除

您也可以使用 Windows PowerShell 及 **Set-CsArchivingConfiguration** Cmdlet 管理啟用及停用封存資料的自動清除。此 Cmdlet 可從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段執行。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 啟用所有封存資料的清除

  - 若要啟用所有封存資料的清除，請將 **EnablePurging** 屬性設為 true ($True)。例如：
    
        Set-CsArchivingConfiguration -Identity "site:Redmond" -EnablePurging $True
    
    執行此命令之後，Lync Server 就會每天清除比 **KeepArchivingDataForDays** 屬性所指定之值更舊的所有封存記錄。

## 僅啟用匯出封存資料的清除

  - 若要限制只清除已匯出至資料檔案 (藉由使用 [Export-CsArchivingData](https://docs.microsoft.com/en-us/powershell/module/skype/Export-CsArchivingData) Cmdlet) 的封存記錄，您也必須將 PurgeExportedArchivesOnly 屬性設為 True ($True)。例如：
    
        Set-CsArchivingConfiguration -Identity "site:Redmond" -EnablePurging $True -PurgeExportedArchivesOnly $True
    
    執行此命令之後，Lync Server 將僅會清除符合這兩項條件的封存記錄：1) 比 **KeepArchivingDataForDays** 屬性所指定之值更舊；2) 已使用 **Export-CsArchivingData** Cmdlet 加以匯出。

## 停用所有封存資料的清除

  - 若要停用封存記錄的自動清除，請將 **EnablePurging** 屬性設為 False ($False)。例如：
    
        Set-CsArchivingConfiguration -Identity "site:Redmond" -EnablePurging $False

如需包含清除封存資料之其他選項的詳細資訊，請參閱說明主題中的 [Set-CsArchivingConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsArchivingConfiguration) Cmdlet。

## 請參閱

#### 概念

[在 Lync Server 2013 中封存的運作方式](lync-server-2013-how-archiving-works.md)  

#### 其他資源

[設定和指派封存原則](lync-server-2013-configuring-and-assigning-archiving-policies.md)  
[在 Lync Server 2013 中管理組織、網站及集區的封存設定選項](lync-server-2013-managing-archiving-configuration-options-for-your-organization-sites-and-pools.md)

