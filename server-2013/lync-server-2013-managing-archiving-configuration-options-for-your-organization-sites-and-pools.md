---
title: 在 Lync Server 2013 中管理組織、網站及集區的封存設定選項
TOCTitle: 在 Lync Server 2013 中管理組織、網站及集區的封存設定選項
ms:assetid: 377a6f80-5f2b-4bc1-b507-e930a461fb1d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204802(v=OCS.15)
ms:contentKeyID: 49290591
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中管理組織、網站及集區的封存設定選項

 

_**上次修改主題的時間：** 2012-11-01_

在 Lync Server 2013 控制台中，您可使用封存組態來指定如何實作封存，這包括下列封存組態：

  - 部署 Lync Server 2013 時依據預設會建立的全域組態。

  - 選用的網站層級和集區層級組態，可建立及用於指定針對特定網站或集區如何實作封存。

您一開始部署封存時會設定封存組態，但是在部署後可以變更、新增及刪除組態。在 Lync Server 2013 控制台中，您可以使用 **\[封存與監控\]** 群組的 **\[封存組態\]** 頁面來管理全域層級、網站層級和集區層級的組態。如需有關如何實作封存組態，包括可以指定的選項，以及封存組態的階層，請參閱規劃文件、部署文件或作業文件中的＜[在 Lync Server 2013 中封存的運作方式](lync-server-2013-how-archiving-works.md)＞。

> [!NOTE]
> 如要使用封存，您必須設定封存原則，以指定是否針對所有主伺服器位於 Lync Server 2013 的使用者，啟用內部通訊、外部通訊或兩者的封存。依據預設，都不會啟用內部或外部通訊的封存。如果使用 Microsoft Exchange 整合，則必須啟用並設定 Exchange 2013，才可支援封存所有主伺服器位於 Exchange 2013 且信箱處於就地保留狀態的使用者。<br />
> 在啟用封存之前，應針對部署 (及選擇性針對特定網站和集區) 指定適當的封存組態，如本區段所述。如需有關啟用封存的詳細資訊，請參閱部署文件中的＜<a href="lync-server-2013-configuring-and-assigning-archiving-policies.md">設定和指派封存原則</a>＞。


**使用 Lync Server 管理命令介面 Cmdlet 檢視封存組態**

  - 您也可以使用 Lync ServerWindows PowerShell 及 **Get-CsArchivingConfiguration** Cmdlet 來檢視封存組態資訊。您可從 Lync Server 2013 管理命令介面或者從 Windows PowerShell 的遠端工作階段執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。
    
    在 Lync Server 管理命令介面中，使用下列命令以檢視所有封存組態設定的資訊：
    
        Get-CsArchivingConfiguration

## 本章節內容

  - [建立封存設定以管理特定網站或集區的封存](lync-server-2013-creating-an-archiving-configuration-to-manage-archiving-for-specific-sites-or-pools.md)

  - [啟用或停用封存 IM 或會議工作階段](lync-server-2013-enabling-or-disabling-archiving-of-im-or-conferencing-sessions.md)

  - [啟用或停用清除封存資料](lync-server-2013-enabling-or-disabling-the-purging-of-archived-data.md)

  - [啟用或停用嚴重模式以封鎖或允許 IM 和 Web 會議工作階段 (若封存失敗)](lync-server-2013-enabling-or-disabling-critical-mode-to-block-or-allow-im-and-web-conferencing-sessions-if-archiving-fails.md)

  - [在 Lync Server 2013 中啟用或停用傳送封存免責聲明至同盟合作夥伴的功能](lync-server-2013-enable-or-disable-sending-an-archiving-disclaimer-to-federated-partners.md)

  - [啟用或停用 Exchange 儲存整合](lync-server-2013-enabling-or-disabling-integration-with-exchange-storage.md)

  - [刪除封存設定](lync-server-2013-deleting-an-archiving-configuration.md)

## 請參閱

#### 其他資源

[管理 Lync Server 2013 封存](lync-server-2013-managing-archiving.md)

