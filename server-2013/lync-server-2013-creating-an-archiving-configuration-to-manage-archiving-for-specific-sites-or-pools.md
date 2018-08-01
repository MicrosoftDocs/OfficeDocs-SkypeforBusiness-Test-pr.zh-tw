---
title: 建立封存設定以管理特定網站或集區的封存
TOCTitle: 建立封存設定以管理特定網站或集區的封存
ms:assetid: c5c864a6-96c7-4bbb-ab7c-61eb1744246c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205251(v=OCS.15)
ms:contentKeyID: 49292262
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 建立封存設定以管理特定網站或集區的封存

 

_**上次修改主題的時間：** 2013-02-23_

在 Lync Server 2013 控制台中，可使用封存組態來控制在您的部署中實作封存的方式。這包括下列封存組態：

  - 部署 Lync Server 2013 時預設會建立的全域組態。

  - 您可建立並使用的選用網站層級與集區層級組態，以指定在特定網站或集區實作封存的方式。

您一開始在部署封存時設定封存組態，但可以在部署之後變更、新增和刪除組態。如需關於封存組態實作方式的詳細資訊，包括您可以指定的選項以及封存組態的階層，請參閱規劃文件、部署文件或作業文件中的[在 Lync Server 2013 中封存的運作方式](lync-server-2013-how-archiving-works.md)。

> [!NOTE]
> 若要使用封存，您必須設定封存原則，以指定是否針對位於 Lync Server 2013 的使用者啟用內部通訊、外部通訊或兩者的封存。預設不會啟用內部或外部通訊的封存。在任何原則中啟用封存前，應先如本節所述，為您的部署和 (選用的) 特定網站與集區指定適當的封存組態。如需關於啟用封存的詳細資訊，請參閱部署文件中的<a href="lync-server-2013-configuring-and-assigning-archiving-policies.md">設定和指派封存原則</a>。<br />
> 如果在部署封存後，您決定要使用 Microsoft Exchange 整合將封存資料與檔案存放在 Exchange 2013 伺服器上，且所有使用者都隸屬於 Exchange 2013 伺服器，則您應移除拓撲中的 SQL Server 資料庫組態。您必須使用拓撲產生器來執行這個動作。如需詳細資訊，請參閱作業文件中的<a href="lync-server-2013-changing-archiving-database-options.md">在 Lync Server 2013 中變更封存資料庫選項</a>。


## 建立網站或集區的封存組態

1.  使用指派給 CsArchivingAdministrator 或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左側導覽列中，依序按一下 \[監控和封存\]及 \[封存組態\]。

4.  在 \[封存組態\] 頁面上按一下 \[新增\]，然後執行下列其中一項操作：
    
      - 若要建立網站封存組態，請按一下 \[站台組態\]，接著在 \[選取站台\] 中選取要設定封存的網站。
    
      - 若要建立集區封存組態，請按一下 \[集區組態\]，接著在 \[選取集區\] 中選取要設定封存的集區。

5.  在 \[新增封存設定\] 的 \[封存設定\] 下拉式清單方塊中，執行下列其中一個動作：
    
      - 若只要啟用立即訊息 (IM) 工作階段的封存，請按一下 \[封存 IM 工作階段\]。
    
      - 若要同時啟用 IM 工作階段和 Web 會議的封存，請按一下 \[封存 IM 與 Web 會議工作階段\]。
    
      - 若要停用原則的封存，請按一下 \[停用封存\]。

6.  另外在 \[新增封存設定\] 中，執行下列動作：
    
      - 若要在封存無法使用時封鎖活動，請選取 \[封存失敗時封鎖立即訊息 (IM) 和 Web 會議工作階段\] 核取方塊。
    
      - 若要使用 Microsoft Exchange Server 存放封存資料，請按一下 \[Microsoft Exchange 整合\] 核取方塊。
    
      - 若要啟用資料清除，請選取 \[啟用封存資料的清除\] 核取方塊，然後執行下列其中一項：
        
          - 若要指定在特定天數後進行清除，請按一下 \[在最大持續期限 (天) 後清除匯出的封存資料和儲存的封存資料\]，然後指定天數。
        
          - 若要限制只清除已匯出的封存資料，請按一下 \[只清除匯出的封存資料\]。

7.  按一下 \[認可\]。

## 使用 Lync Server Cmdlet 建立封存組態設定

您也可以使用 Windows PowerShell Windows PowerShell 和 New-CsArchivingConfiguration Cmdlet 建立封存組態設定。您可以從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 為網站建立新的封存組態設定集合

  - 下列命令會針對 Redmond 網站，建立新的封存組態設定集合：
    
        New-CsArchivingConfiguration -Identity "site:Redmond"

## 建立僅允許 IM 封存的新封存組態設定集合

  - 由於上述的命令除了指定必要的 Identity 參數以外，並未指定任何其他參數，因此新組態設定集合的所有屬性都將使用預設值。若要建立使用不同屬性值的設定，只要加上適當的參數和參數值即可。例如，若要建立預設僅允許封存立即訊息工作階段的封存組態設定集合，請使用類似如下的命令：
    
        New-CsArchivingConfiguration -Identity "site:Redmond" -EnableArchiving "ImOnly"

## 在建立封存組態設定時指定多個屬性值

  - 您可以加上多個參數來修改多個屬性值。例如，此命令會設定新的設定，用以封存立即訊息工作階段並在封存服務無法使用時封鎖立即訊息：
    
        New-CsArchivingConfiguration -Identity "site:Redmond" -EnableArchiving "ImOnly" -BlockOnArchiveFailure $True

如需詳細資訊，請參閱 [New-CsArchivingConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsArchivingConfiguration) Cmdlet 的說明主題。

## 請參閱

#### 概念

[在 Lync Server 2013 中封存的運作方式](lync-server-2013-how-archiving-works.md)  

#### 其他資源

[在 Lync Server 2013 中管理組織、網站及集區的封存設定選項](lync-server-2013-managing-archiving-configuration-options-for-your-organization-sites-and-pools.md)

