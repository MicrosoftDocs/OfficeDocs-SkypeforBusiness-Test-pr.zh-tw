---
title: Lync Server 2013：檢視裝置更新組態設定
TOCTitle: 檢視裝置更新組態設定
ms:assetid: aa6a70a9-bd77-4606-b797-ea6a3bab9cf2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994059(v=OCS.15)
ms:contentKeyID: 52056175
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中檢視裝置更新組態設定

 

_**上次修改主題的時間：** 2013-02-20_

您也可以使用 Lync Server 管理命令介面 和 **Get-CsDeviceUpdateConfiguration** Cmdlet 檢視裝置更新服務組態設定。您可以從 Lync Server 2013 管理命令介面 或從 Windows PowerShell 的遠端工作階段執行此 Cmdlet。

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




  - 
    
    如果要檢視您所有語音路由的資訊，請在 Lync Server 管理命令介面 中輸入下列命令，然後按下 Enter：
    
        Get-CsDeviceUpdateConfiguration
    
    此命令會傳回與下列相似的資訊：
    
        Identity               : Global
        ValidLogFileTypes      : {Watson, Config, Diaglog, CELog}
        ValidLogFileExtensions : {.dmp, .clg, .clg1, .clg2...}
        MaxLogFileSize         : 1024000
        MaxLogCacheLimit       : 512000
        LogCleanUpInterval     : 10.00:00:00
        LogFlushInterval       : 00:05:00
        LogCleanUpTimeOfDay    :

如需此 Cmdlet 的詳細資訊，請參閱說明主題 [Get-CsDeviceUpdateConfiguration](get-csdeviceupdateconfiguration.md)。

