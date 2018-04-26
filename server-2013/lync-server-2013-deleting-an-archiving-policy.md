---
title: 刪除封存原則
TOCTitle: 刪除封存原則
ms:assetid: 4739a691-41cc-4128-8bb8-6d5a4c02107a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg520989(v=OCS.15)
ms:contentKeyID: 49290788
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 刪除封存原則

 

_**上次修改主題的時間：** 2013-02-23_

您可以刪除使用者原則或網站原則。無法移除全域原則。如果您刪除全域原則，Lync Server 2013會自動將原則重設為預設值。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您針對部署啟用 Microsoft Exchange 整合，Exchange 原則會控制是否為隸屬於 Exchange 2013 的使用者啟用封存，並保留他們的信箱。如需詳細資訊，請參閱部署文件中的<a href="lync-server-2013-setting-up-policies-for-archiving-when-using-exchange-server-integration.md">設定使用 Exchange Server 整合時的封存原則</a>。</td>
</tr>
</tbody>
</table>


## 若要刪除使用者或網站原則進行封存

1.  使用指派給 CsArchivingAdministrator 或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左側導覽列中，依序按一下 \[監控和封存\]及 \[封存原則\]。

4.  在封存原則清單中，依序按一下您要刪除的使用者或網站原則、**\[編輯\]** 和 **\[刪除\]**。

5.  按一下 **\[認可\]**。

## 使用 Lync Server 管理命令介面 Cmdlet 移除封存原則

您也可以使用 Windows PowerShell 和 **Remove-CsArchivingPolicy** Cmdlet 來刪除封存原則。這個 Cmdlet 可以從 Lync Server 2013 管理命令介面或 Windows PowerShell 的遠端工作階段來執行。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 移除指定的封存原則

  - 例如，**Remove-CsArchivingPolicy** 會刪除 Identity 為 site:Redmond 的原則。請注意，刪除在網站範圍設定的原則時，先前由該網站原則管理的使用者會自動改由全域封存原則管理。下列命令會移除套用至 Redmond 網站的封存。
    
        Remove-CsArchivingPolicy -Identity site:Redmond

## 移除所有套用至個別使用者範圍的封存原則

  - 這個命令會移除所有套用至個別使用者範圍的封存原則：
    
        Get-CsArchivingPolicy -Filter "tag:*" | Remove-CsArchivingPolicy

## 移除停用內部封存的封存原則

  - 這個命令會移除所有已停用內部封存的封存原則：
    
        Get-CsArchivingPolicy | Where-Object {$_.ArchiveInternal -eq $False} | Remove-CsArchivingPolicy

如需詳細資訊，請參閱 [Remove-CsArchivingPolicy](remove-csarchivingpolicy.md) Cmdlet 的說明主題。

## 請參閱

#### 其他資源

[在 Lync Server 2013 中管理內部與外部通訊的封存](lync-server-2013-managing-the-archiving-of-internal-and-external-communications.md)

