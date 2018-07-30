---
title: 變更封存原則以啟用或停用封存組織、網站或使用者的內部或外部通訊
TOCTitle: 變更封存原則以啟用或停用封存組織、網站或使用者的內部或外部通訊
ms:assetid: b85dc3fb-8ebd-4e3c-ac90-fc79270ac867
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182576(v=OCS.15)
ms:contentKeyID: 49292112
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 變更封存原則以啟用或停用封存組織、網站或使用者的內部或外部通訊

 

_**上次修改主題的時間：** 2013-02-23_

在 Lync Server 2013 中，您可使用原則為 Lync Server 2013 上的使用者啟用與停用內部通訊與外部通訊的封存。這包含下列封存原則：

  - 部署 Lync Server 2013 時預設建立的全域原則。

  - 您可建立並用來指定如何為特定網站或使用者實作封存的選用網站層級與使用者層級原則。

您一開始會在部署封存時設定封存原則，但可在部署後變更、新增與刪除原則。在 Lync Server 2013 控制台中，您可使用 \[封存和監控\] 群組 的 \[封存原則\] 頁面來管理全域層級、網站層級與使用者層級的原則。如果您將 Lync Server 儲存整合至 Exchange 2013 儲存，Exchange 使用者原則的優先順序會高於 Lync Server 2013 封存原則。

如需關於如何實作原則的詳細資訊，包含原則的階層，請參閱規劃文件、部署文件或作業文件中的[在 Lync Server 2013 中封存的運作方式](lync-server-2013-how-archiving-works.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若您在部署中啟用 Microsoft Exchange 整合，Exchange 原則可控制是否為位於 Exchange 2013 的使用者啟用封存，並將他們的信箱就地保留。如需詳細資訊，請參閱部署文件中的<a href="lync-server-2013-setting-up-policies-for-archiving-when-using-exchange-server-integration.md">設定使用 Exchange Server 整合時的封存原則</a>。<br />
您必須先在 [封存] 組態中指定所有適當選項，才能啟用封存功能。如需詳細資訊，請參閱作業文件中的<a href="lync-server-2013-managing-archiving-configuration-options-for-your-organization-sites-and-pools.md">在 Lync Server 2013 中管理組織、網站及集區的封存設定選項</a>。</td>
</tr>
</tbody>
</table>


## 變更封存原則

1.  使用指派給 CsArchivingAdministrator 或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左側導覽列中，依序按一下 \[監控和封存\]及 \[封存原則\]。

4.  在原則清單中，執行下列其中一項：
    
      - 若要變更整個部署的原則，請按一下原則清單中的 \[全域\]、按一下 \[編輯\]，然後按一下 \[顯示詳細資料\]。
    
      - 若要變更單一網站的原則，請按一下原則清單中的網站名稱、按一下 \[編輯\]，然後按一下 \[顯示詳細資料\]。
    
      - 若要變更單一使用者或使用者群組的原則，請按一下原則清單中的使用者或使用者群組、按一下 \[編輯\]，然後按一下 \[顯示詳細資料\]。

5.  在 \[編輯封存原則\] 頁面中，執行下列動作：
    
      - 若要啟用或停用原則的內部封存，請選取或清除 \[封存內部通訊\] 核取方塊。
    
      - 若要啟用或停用原則的外部封存，請選取或清除 \[封存外部通訊\] 核取方塊。

6.  按一下 \[認可\]。
    
    > [!IMPORTANT]  
    > 使用者原則的設定只會套用到您套用該原則的特定使用者及使用者群組。如需詳細資訊，請參閱<a href="lync-server-2013-applying-an-archiving-policy-to-users.md">將封存原則套用到使用者</a>。
    


## 使用 Lync Server PowerShell Cmdlet 啟用與停用封存

也可使用 **Set-CsArchivingPolicy** Cmdlet 來啟用與停用封存 (針對內部與外部通訊工作階段)。可從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段來執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 啟用內部通訊工作階段的封存

  - 若要啟用內部通訊工作階段的封存，請將 **ArchiveInternal** 屬性值設為 True ($True)。例如：
    
        Set-CsArchivingPolicy -Identity "global" -ArchiveInternal $True

## 啟用外部通訊工作階段的封存

  - 若要啟用外部通訊工作階段的封存，請將 **Archiveexternal** 屬性值設為 True ($True)。例如：
    
        Set-CsArchivingPolicy -Identity "global" -ArchiveExternal $True

## 啟用內部與外部通訊工作階段的封存

  - 若要啟用內部與外部通訊工作階段的封存，請將 **ArchiveInternal** 與 **ArchiveExternal** 屬性設定為 True：
    
        Set-CsArchivingPolicy -Identity "global" -ArchiveInternal $True -ArchiveExternal $True

## 停用封存

  - 若要一併停用封存，請將 **ArchiveInternal** 與 **ArchiveExternal** 屬性設定為 False ($False)。例如：
    
        Set-CsArchivingPolicy -Identity "global" -ArchiveInternal $False -ArchiveExternal $False

如需詳細資訊，請參閱 [Set-CsArchivingPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsArchivingPolicy) Cmdlet 的說明主題。

## 請參閱

#### 其他資源

[在 Lync Server 2013 中管理內部與外部通訊的封存](lync-server-2013-managing-the-archiving-of-internal-and-external-communications.md)

