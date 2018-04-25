---
title: 將封存原則套用到使用者
TOCTitle: 將封存原則套用到使用者
ms:assetid: 624a7d3e-389d-403a-97e5-f7bb17023ef3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg521004(v=OCS.15)
ms:contentKeyID: 49291102
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 將封存原則套用到使用者

 

_**上次修改主題的時間：** 2013-02-23_

如果已啟用使用者用於 Lync Server 2013，且已針對位於 Lync Server 2013 的使用者建立一項或多項封存使用者原則，則將適當的原則套用至那些使用者或使用者群組，就可以針對特定使用者實作封存支援。例如，如果建立原則來支援內部通訊的封存，則可以將它套用至最少一位使用者或最少一個使用者群組，以支援封存使用者的 Lync Server 2013 通訊。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果啟用部署的 Microsoft Exchange 整合，Exchange 就地保留原則會控制是否對位於 Exchange 2013 的使用者啟用封存，而將他們的信箱設定為就地保留狀態。如需詳細資訊，請參閱部署文件中的<a href="lync-server-2013-setting-up-policies-for-archiving-when-using-exchange-server-integration.md">設定使用 Exchange Server 整合時的封存原則</a>。<br />
啟用封存前，應在封存組態中指定所有適當的選項。如需詳細資訊，請參閱作業文件中的<a href="lync-server-2013-managing-archiving-configuration-options-for-your-organization-sites-and-pools.md">在 Lync Server 2013 中管理組織、網站及集區的封存設定選項</a>。</td>
</tr>
</tbody>
</table>


使用本主題中的程序，將先前建立的封存使用者原則套用至一或多個使用者帳戶或使用者群組。

## 將封存使用者原則套用至使用者帳戶

1.  使用指派給 CsArchivingAdministrator 或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[使用者\]**，然後搜尋想要設定的使用者帳戶。

4.  在列出搜尋結果的表格中，按一下使用者帳戶，並依序按一下 **\[編輯\]** 及 **\[顯示詳細資料\]**。

5.  在 **\[封存原則\]** 下的 **\[編輯 Lync Server 使用者\]** 中，選取想要套用的封存使用者原則。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><strong>[&lt;自動&gt;]</strong> 設定套用預設伺服器安裝設定。伺服器會自動套用這些設定。</td>
    </tr>
    </tbody>
    </table>


6.  按一下 **\[認可\]**。

## 使用 Lync Server 管理命令介面 Cmdlet 指派個別使用者封存原則

您也可以使用 Lync ServerWindows PowerShell 及 **Grant-CsArchivingPolicy** Cmdlet 來指派個別用者封存原則。您可從 Lync Server 2013 管理命令介面或者從 Windows PowerShell 的遠端工作階段執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 將個別使用者封存原則指派給單一使用者

  - 下列命令將個別使用者封存原則 RedmondArchivingPolicy 指派給使用者 Ken Myer。
    
        Grant-CsArchivingPolicy -Identity "Ken Myer" -PolicyName "RedmondArchivingPolicy"

## 將個別使用者封存原則指派給多位使用者

  - 此命令將個別使用者封存原則 RedmondArchivingPolicy 指派給帳戶位於登錄器集區 atl-cs-001.litwareinc.com 的所有使用者。如需用於此命令中篩選器參數的詳細資訊，請參閱 [Get-CsUser](get-csuser.md) Cmdlet 文件。
    
        Get-CsUser -Filter {RegistrarPool -eq "atl-cs-001.litwareinc.com"} | Grant-CsArchivingPolicy -PolicyName "RedmondArchivingPolicy"

## 解除指派個別使用者封存原則

  - 下列命令解除指派任何先前指派給 Ken Myer 的個別使用者封存原則。一旦解除指派個別使用者原則後，系統會自動使用全域原則或其本機網站原則 (如果有的話) 來管理 Ken Myer。網站原則優先順序高於全域原則。
    
        Grant-CsArchivingPolicy -Identity "Ken Myer" -PolicyName $Null

如需詳細資訊，請參閱 [Grant-CsArchivingPolicy](grant-csarchivingpolicy.md) Cmdlet 文件。

## 請參閱

#### 其他資源

[在 Lync Server 2013 中管理內部與外部通訊的封存](lync-server-2013-managing-the-archiving-of-internal-and-external-communications.md)  
[指派每位使用者的原則](lync-server-2013-assigning-per-user-policies.md)

