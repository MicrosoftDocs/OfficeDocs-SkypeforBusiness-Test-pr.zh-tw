---
title: 刪除現有的會議原則
TOCTitle: 刪除現有的會議原則
ms:assetid: 709ed771-790f-4bf1-a4de-b37ca5168688
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688089(v=OCS.15)
ms:contentKeyID: 49890112
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 刪除現有的會議原則

 

_**上次修改主題的時間：** 2013-02-23_

遵循這些步驟即可刪除使用者層級或網站層級會議原則。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法刪除全域會議原則。</td>
</tr>
</tbody>
</table>


## 刪除網站或使用者會議原則

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  請在左導覽列中按一下 **\[會議\]**，然後按一下 **\[會議原則\]**。

4.  在會議原則清單中，按一下要刪除的網站或使用者原則，再依序按一下 \[編輯\] 及 \[刪除\]。

## 使用 Lync Server 管理命令介面 Cmdlet 移除會議原則

亦可使用 Lync Server 管理命令介面與 **Remove-CsConferencingPolicy** Cmdlet 刪除主幹組態設定。您可從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 移除指定的會議原則

  - 下列命令可移除具有 Identity RedmondConferencingPolicy 的會議原則：
    
        Remove-CsConferencingPolicy -Identity "RedmondConferencingPolicy"

## 移除所有套用於個別使用者範圍的會議原則

  - 下列命令可移除所有設定於個別使用者範圍的會議原則：
    
        Get-CsConferencingPolicy -Filter "tag:*" | Remove-CsConferencingPolicy

## 移除所有允許外部使用者錄製的會議原則

  - 下列命令可移除任何允許外部使用者錄製會議的會議原則：
    
        Get-CsConferencingPolicy | Where-Object {$_.AllowExternalUsersToRecordMeetings -eq $True} | Remove-CsConferencingPolicy

如需詳細資訊，請參閱 [Remove-CsConferencingPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsConferencingPolicy)。

