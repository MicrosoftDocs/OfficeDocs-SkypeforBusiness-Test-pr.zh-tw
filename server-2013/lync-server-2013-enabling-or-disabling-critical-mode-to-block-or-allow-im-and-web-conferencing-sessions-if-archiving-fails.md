---
title: 啟用或停用嚴重模式以封鎖或允許 IM 和 Web 會議工作階段 (若封存失敗)
TOCTitle: 啟用或停用嚴重模式以封鎖或允許 IM 和 Web 會議工作階段 (若封存失敗)
ms:assetid: fafdcd2e-b778-4ed5-a25f-09208aa3b699
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182609(v=OCS.15)
ms:contentKeyID: 49292897
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 啟用或停用嚴重模式以封鎖或允許 IM 和 Web 會議工作階段 (若封存失敗)

 

_**上次修改主題的時間：** 2013-02-23_

在 Lync Server 2013 控制台 中，您會使用啟用與停用關鍵模式的封存設定，包含下列：

  - 部署 Lync Server 2013 時預設建立的全域設定。

  - 您可建立並用於指定特殊網站或集區實作封存方式之網站層級與集區層級的選用設定。

您部署封存時，一開始會先配置封存設定，但部署後，還是可變更、新增以及刪除這些設定。如需實作封存設定方式的詳細資訊，包含可指定的選項以及封存設定的階層，請參閱規劃、部署或作業文件中的[在 Lync Server 2013 中封存的運作方式](lync-server-2013-how-archiving-works.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要使用封存，必須將封存原則設定為指定是否要針對隸屬於 Lync Server 2013 的使用者，啟用內部通訊、外部通訊或兩者的封存。根據預設，並未啟用內部或外部通訊的封存。啟用任何原則中的封存前，您應如本節所述，先針對部署指定適當的封存設定，以及選擇性針對特定網站與集區指定適當的封存設定。如需啟用封存的詳細資訊，請參閱部署文件的<a href="lync-server-2013-configuring-and-assigning-archiving-policies.md">設定和指派封存原則</a>。<br />
如果您在部署封存後決定想使用 Exchange Server 整合，以將封存資料與檔案儲存於 Exchange 2013 伺服器，以及所有使用者均隸屬於 Exchange 2013 伺服器，則您應從拓撲中移除 SQL Server 資料庫設定。您必須使用 拓撲產生器 來完成。如需詳細資訊，請參閱作業文件的<a href="lync-server-2013-changing-archiving-database-options.md">在 Lync Server 2013 中變更封存資料庫選項</a>。</td>
</tr>
</tbody>
</table>


## 若要在封存失敗時啟用或停用 IM 和 Web 會議工作階段的封鎖

1.  使用指派給 CsArchivingAdministrator 或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左側導覽列中，依序按一下 \[監控和封存\]及 \[封存組態\]。

4.  依序按一下封存設定清單中適當全域、網站或集區設定中的名稱、\[編輯\] 以及 \[顯示詳細資料\]，然後執行下列步驟：

5.  若要設定封存在發生失敗時的行為，請選取或清除 \[封存失敗時封鎖立即訊息 (IM) 和 Web 會議工作階段\] 核取方塊。

6.  按一下 \[認可\]。

## 使用 Lync ServerWindows PowerShell Cmdlet 啟用與停用關鍵模式

您可使用 **Set-CsArchivingConfiguration** Cmdlet 啟用與停用關鍵模式。您可從 Lync Server 2013 管理命令介面 或 Windows PowerShell 的 如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。 遠端工作階段執行此 Cmdlet。

## 啟用關鍵模式

  - 若要啟用關鍵模式，請將 BlockOnArchiveFailure 屬性值設為 True ($True)。例如：
    
        Set-CsArchivingConfiguration -Identity "site:Redmond" -BlockOnArchiveFailure $True

## 停用關鍵模式

  - 若要停用關鍵模式，請將 BlockOnArchiveFailure 屬性值設為 False ($False)。例如：
    
        Set-CsArchivingConfiguration -Identity "site:Redmond" -BlockOnArchiveFailure $False

如需詳細資訊，請參閱說明主題以了解 [Set-CsArchivingConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsArchivingConfiguration) Cmdlet。

## 請參閱

#### 工作

[在 Lync Server 2013 中變更封存資料庫選項](lync-server-2013-changing-archiving-database-options.md)  

#### 概念

[在 Lync Server 2013 中封存的運作方式](lync-server-2013-how-archiving-works.md)  

#### 其他資源

[在 Lync Server 2013 中管理組織、網站及集區的封存設定選項](lync-server-2013-managing-archiving-configuration-options-for-your-organization-sites-and-pools.md)

