---
title: 刪除裝置更新記錄檔
TOCTitle: 刪除裝置更新記錄檔
ms:assetid: 58d4097f-5bbf-4824-a04d-2a6555cd93c3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994039(v=OCS.15)
ms:contentKeyID: 52056112
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 刪除裝置更新記錄檔

 

_**上次修改主題的時間：** 2013-02-23_

裝置更新 Web 服務保有大量的記錄檔集合。此集合包括服務本身執行的稽核記錄檔，以及用戶端裝置上傳的記錄檔。為了防止裝置更新 Web 服務的服務記錄填滿伺服器，建議您清除伺服器上已經存在一定天數的記錄檔。請根據更新活動和組織中用戶端裝置的數目以設定此天數，並使用 Lync Server 控制台或 Lync Server 管理命令介面。

## 使用 Lync Server 控制台清除裝置更新記錄檔

1.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

2.  在左導覽列中，依序按一下 \[用戶端\] 和 \[裝置記錄檔設定\]。

3.  在「裝置記錄檔設定」頁面上，按兩下要變更的設定。

4.  在 \[編輯記錄檔設定\] 對話方塊中，於 \[記錄檔保留天數 (1-365)\] 中指定天數。

5.  按一下 \[認可\]。所有在伺服器上超過指定天數的檔案都會刪除。此設定會一直套用至這個組態，直到您改變設定為止。

## 使用 Windows PowerShell Cmdlet 清除裝置更新記錄檔

您可以使用 Windows PowerShell 和 **Clear-CsDeviceUpdateLog** Cmdlet，清除裝置更新記錄檔。可從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段執行此 Cmdlet。

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


## 清除單一伺服器上的裝置更新記錄檔

  - 下列命令會清除 Web 伺服器 atl-cs-001.litwareinc.com 上的裝置更新記錄檔。所有超過 10 天 (DaysBack 參數所指定的值) 的記錄項目將會從記錄檔中移除。
    
        Clear-CsDeviceUpdateLog -Identity "service:WebServer:atl-cs-001.litwareinc.com" -DaysBack 10

## 清除所有的裝置更新記錄檔

  - 此命令會從組織中所有目前使用中的裝置更新記錄檔，移除過期的項目 (此範例中，為超過 10 天的項目)。
    
        Get-CsService -WebServer | Foreach-Object {Clear-CsDeviceUpdateLog -Identity $_.Identity -DaysBack 10}

如需詳細資訊，請參閱＜[Clear-CsDeviceUpdateLog](https://docs.microsoft.com/en-us/powershell/module/skype/Clear-CsDeviceUpdateLog)＞ Cmdlet 的說明主題。

