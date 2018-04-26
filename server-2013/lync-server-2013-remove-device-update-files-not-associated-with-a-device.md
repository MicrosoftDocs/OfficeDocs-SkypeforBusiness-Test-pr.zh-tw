---
title: 移除未與裝置關聯的裝置更新檔案
TOCTitle: 移除未與裝置關聯的裝置更新檔案
ms:assetid: ecebbf73-b456-4990-a91d-308b84d39404
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994084(v=OCS.15)
ms:contentKeyID: 52056251
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移除未與裝置關聯的裝置更新檔案

 

_**上次修改主題的時間：** 2013-02-20_

每次將新裝置更新上傳至系統時，就會建立對應的裝置更新規則。根據預設，這些新裝置更新規則會被指派為「擱置」狀態；也就是說，您可以將規則下載並安裝在測試裝置上，但無法下載並安裝在生產裝置 (可讓您在將更新提供給使用者之前先進行測試) 上。您可以根據這些測試接受並部署或拒絕並刪除更新。拒絕更新時，裝置更新會解除與其裝置更新規則的關聯。


可使用 Windows PowerShell 和 **Clear-CsDeviceUpdateFile** Cmdlet 移除不再與裝置相關聯的裝置更新檔案。可從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段執行此 Cmdlet。

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



  - 例如，下列命令可移除 Web 伺服器 atl-cs-001.litwareinc.com 上不再與裝置相關聯的裝置更新規則：
    
        Clear-CsDeviceUpdateFile -Identity "service:WebServer:atl-cs-001.litwareinc.com"

如需詳細資訊，請參閱＜[Clear-CsDeviceUpdateFile](clear-csdeviceupdatefile.md)＞ Cmdlet 的主題說明。

