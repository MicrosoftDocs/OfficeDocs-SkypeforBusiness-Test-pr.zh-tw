---
title: 還原裝置更新規則
TOCTitle: 還原裝置更新規則
ms:assetid: ac490baf-c7a0-48d9-8fd0-ba5729489341
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994061(v=OCS.15)
ms:contentKeyID: 52056179
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 還原裝置更新規則

 

_**上次修改主題的時間：** 2013-02-23_

若要從部署中的裝置解除安裝裝置更新規則，請還原之。還原裝置更新規則會解除安裝更新並重新安裝上一版的規則。

您可以使用 Lync Server 控制台或 Windows PowerShell 還原裝置更新規則。

## 使用 Lync Server 控制台還原裝置更新規則

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列，按一下 \[用戶端\]，然後按一下 \[裝置更新\] 導覽按鈕。

4.  在「裝置更新」頁面中，執行下列其中一項動作：
    
      - 若要還原一個規則，請選取該規則。
    
      - 若要還原所有規則，請按一下 \[編輯\]，然後按一下 \[全選\]。

5.  按一下 \[動作\] 功能表，然後按一下 \[還原\]。

## 使用 Windows PowerShell Cmdlet 還原裝置更新規則

裝置更新規則僅可使用 Windows PowerShell 和 **Restore-CsDeviceUpdateRule** Cmdlet 來還原。可從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段執行此 Cmdlet。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：<a href="http://go.microsoft.com/fwlink/p/?linkid=255876">http://go.microsoft.com/fwlink/p/?linkId=255876</a>。</td>
</tr>
</tbody>
</table>


## 在伺服器上還原單一裝置更新規則

  - 下列命令可還原在 Web 伺服器 atl-cs-001.litwareinc.com 上的裝置更新規則 d5ce3c10-2588-420a-82ac-dc2d9b1222ff9：
    
        Restore-CsDeviceUpdateRule -Identity "service:WebServer:atl-cs-001.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9"

## 在伺服器上還原所有裝置更新規則

  - 此命令會還原 Web 伺服器 atl-cs-001.litwareinc.com 上的所有裝置更新規則：
    
        Get-CsDeviceUpdateRule -Filter "service:WebServer:atl-cs-001.litwareinc.com*" | Restore-CsDeviceUpdateRule

如需詳細資訊，請參閱＜[Restore-CsDeviceUpdateRule](restore-csdeviceupdaterule.md)＞ Cmdlet 的說明主題。

