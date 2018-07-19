---
title: 建立封存原則以針對特定網站或使用者啟用或停用封存內部或外部通訊
TOCTitle: 建立封存原則以針對特定網站或使用者啟用或停用封存內部或外部通訊
ms:assetid: 5864793a-ba72-470c-bb5b-9fb41e968896
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398385(v=OCS.15)
ms:contentKeyID: 49290990
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 建立封存原則以針對特定網站或使用者啟用或停用封存內部或外部通訊

 

_**上次修改主題的時間：** 2013-02-23_

在 Lync Server 2013 中，您可以使用原則，針對位於 Lync Server 2013 的使用者啟用和停用內部通訊和外部通訊的封存。這包括下列封存原則：

  - 當您部署 Lync Server 2013 時預設建立的全域原則。

  - 您可以選擇性建立的網站層級和使用者層級原則，並用來指定如何針對特定的網站或使用者實作封存。

您最初可以在部署封存時設定封存，但可在部署之後變更、新增及刪除原則。在 Lync Server 2013 控制台中，您可以使用 **\[封存和監控\]** 群組的 **\[封存原則\]** 頁面來管理全域層級、網站層級及使用者層級的原則。如果您將 Lync Server 儲存與 Exchange 2013 儲存整合，Exchange 使用者原則的優先順序會高於 Lync Server 2013 封存原則。

如需有關如何實作原則 (包含原則的階層) 的詳細資訊，請參閱規劃文件、部署文件或作業文件中的[在 Lync Server 2013 中封存的運作方式](lync-server-2013-how-archiving-works.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要控制封存的實作，您必須在封存設定中指定選項，例如，是否要封存 IM 或會議、使用關鍵模式及清除選項。依預設，不會在全域封存設定或是任何網站或集區封存設定中啟用任何選項。您應該先在封存設定中指定所有適當的選項，然後才能在封存原則中啟用對內部或外部通訊的封存。如需詳細資訊，請參閱作業文件中的<a href="lync-server-2013-managing-archiving-configuration-options-for-your-organization-sites-and-pools.md">在 Lync Server 2013 中管理組織、網站及集區的封存設定選項</a>。<br />
如果您針對部署啟用 Microsoft Exchange 整合，Exchange 原則便會控制是否要針對位於 Exchange 2013 且其信箱狀態為 [就地保留] 的使用者啟用封存。如需詳細資訊，請參閱部署文件中的<a href="lync-server-2013-setting-up-policies-for-archiving-when-using-exchange-server-integration.md">設定使用 Exchange Server 整合時的封存原則</a>。</td>
</tr>
</tbody>
</table>


## 建立網站或使用者的封存原則

1.  使用指派給 CsArchivingAdministrator 或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左側導覽列中，依序按一下 \[監控和封存\]及 \[封存原則\]。

4.  按一下 **\[新增\]**，然後執行下列其中一項作業：
    
      - 若要建立網站層級的封存原則，請按一下 **\[站台原則\]**，然後在 **\[選取站台\]** 中，按一下要套用原則的網站。
    
      - 若要建立使用者層級的封存原則，請按一下 **\[使用者原則\]**。

5.  在 **\[新增封存原則\]** 中，執行下列動作：
    
      - 在 **\[名稱\]** 中，指定新原則的名稱 (例如，externalContoso)。
    
      - 在 **\[描述\]** 中，提供該原則的相關詳細資料 (例如，Contoso 的外部使用者封存原則)。
    
      - 若要控制對與內部使用者通訊所進行的封存，請選取或清除 **\[封存內部通訊\]** 核取方塊。
    
      - 若要控制對與外部使用者通訊所進行的封存，請選取或清除 **\[封存外部通訊\]** 核取方塊。

6.  按一下 **\[認可\]**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>使用者原則的設定僅能套用至您套用該原則的特定使用者和使用者群組。如需詳細資訊，請參閱＜<a href="lync-server-2013-applying-an-archiving-policy-to-users.md">將封存原則套用到使用者</a>＞</td>
    </tr>
    </tbody>
    </table>


## 使用 Lync Server 管理命令介面 Cmdlet 建立封存原則

封存原則也可以使用 Windows PowerShell 和 **Remove-CsArchivingPolicy** Cmdlet 來建立。此 Cmdlet 可以從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段執行。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 在網站範圍中建立新的封存原則

  - 此命令可以建立 Redmond 網站的新封存原則：
    
        New-CsArchivingPolicy -Identity "site:Redmond"

## 在每個使用者範圍中建立新的封存原則

  - 若要在每個使用者範圍中建立新的封存原則，只需在建立原則時指定唯一的識別碼：
    
        New-CsArchivingPolicy -Identity "RedmondArchivingPolicy"

## 建立新的封存原則以啟用對內部通訊工作階段進行封存

  - 由於未在前述命令中指定任何參數 (除了必要的 Identity 參數以外)，因此新原則將針對它們的所有屬性使用預設值。若要建立使用不同屬性值的原則，只需包含適當的參數和參數值。例如，若要建立封存原則以准許對內部立即訊息工作階段進行封存，請使用如下的命令：
    
        New-CsArchivingPolicy -Identity "site:Redmond" -ArchiveInternal $True

## 建立新的封存原則以啟用對內部和外部通訊工作階段進行封存

  - 您可以藉由包含多個參數來修改多個屬性值。例如，此命令會設定新原則，來封存內部與外部立即訊息工作階段：
    
        New-CsArchivingPolicy -Identity "site:Redmond" -ArchiveInternal $True -ArchiveExternal $True

如需詳細資訊，請參閱 [New-CsArchivingPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsArchivingPolicy) Cmdlet 的說明主題。

## 請參閱

#### 其他資源

[在 Lync Server 2013 中管理內部與外部通訊的封存](lync-server-2013-managing-the-archiving-of-internal-and-external-communications.md)

