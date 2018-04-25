---
title: 刪除 PIN 原則
TOCTitle: 刪除 PIN 原則
ms:assetid: 7c378927-2e41-418e-9721-327021bd2e45
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg521020(v=OCS.15)
ms:contentKeyID: 49291428
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 刪除 PIN 原則

 

_**上次修改主題的時間：** 2013-02-23_

遵循下列步驟，可刪除個人識別碼 (PIN) 原則。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法刪除全域 PIN 原則。</td>
</tr>
</tbody>
</table>


## 在 Lync Server 2013 控制台中刪除 PIN 原則

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限) 或指派給 CsServerAdministrator 或 CsAdministrator 角色的使用者帳戶，登入部署 Lync Server 2013 之網路上的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 **\[安全性\]** 和 **\[PIN 原則\]**。

4.  在 **\[PIN 原則\]** 頁面的搜尋欄位中，輸入您要刪除之原則的完整或部分名稱。

5.  在原則清單中，按一下您要的原則，再按一下 **\[編輯\]**，然後按一下 **\[刪除\]**。

6.  按一下 \[確定\] 。

## 使用 Lync Server 管理命令介面和 Cmdlet 移除 PIN 原則

您可以使用 Windows PowerShell 和 Remove-CsPinPolicy Cmdlet 刪除 PIN 原則。您可以從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段執行這個 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 移除特定 PIN 原則

  - 這個命令將移除含有 Identity RedmondPinPolicy 的 PIN 原則：
    
        Remove-CsPinPolicy -Identity "RedmondPinPolicy"

## 移除套用於網站範圍的所有 PIN 原則

  - 這個命令將移除網站範圍設定的所有 PIN 原則：
    
        Get-CsPinPolicy -Filter "site:*" | Remove-CsPinPolicy

## 移除允許使用共同模式的所有 PIN 碼原則

  - 而且，這個將移除允許使用共同模式的所有 PIN 原則：G
    
        et-CsPinPolicy | Where-Object {$_.AllowCommonPatterns -eq $True} | Remove-CsPinPolicy

如需詳細資訊，請參閱 [Remove-CsPinPolicy](remove-cspinpolicy.md) Cmdlet 的說明主題。

