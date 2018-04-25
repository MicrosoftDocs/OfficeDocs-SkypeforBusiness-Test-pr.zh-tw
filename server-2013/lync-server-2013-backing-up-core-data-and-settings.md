---
title: 備份核心資料和設定
TOCTitle: 備份核心資料和設定
ms:assetid: 278bc95a-7b8d-4e01-a872-a844830459de
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh202170(v=OCS.15)
ms:contentKeyID: 52056075
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 備份核心資料和設定

 

_**上次修改主題的時間：** 2014-04-23_

下列程序會使用 Lync Server 管理命令介面 Cmdlet 來建立核心服務之設定和資料的備份檔。如需本節所使用工具的詳細資訊，包括其所在位置，請參閱＜[備份和還原需求：工具和權限](lync-server-2013-backup-and-restoration-requirements-tools-and-permissions.md)＞。如需備份封存和監控資料的詳細資訊，請參閱＜[備份封存資料庫和監控資料庫](lync-server-2013-backing-up-archiving-and-monitoring-databases.md)＞。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本節的步驟主要是備份中央管理存放區，包括封存和監控的設定及組態。</td>
</tr>
</tbody>
</table>


您可以本機或遠端執行本節中說明的 Cmdlet。

## 若要備份核心資料與設定

1.  以屬於 RTCUniversalServerAdmins 群組成員身分的使用者帳戶，登入內部部署中的任何電腦。

2.  若要儲存您在下列步驟中所建立的備份，請建立新的共用資料夾，並將 **$Backup** 所參照的路徑更新為新的共用資料夾。

3.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

4.  備份中央管理存放區設定檔。在命令列輸入下列命令：
    
        Export-CsConfiguration -FileName <path and file name for backup>
    
    例如：
    
        Export-CsConfiguration -FileName "C:\Config.zip"
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>此步驟會將您的 Lync Server 拓撲、原則及組態設定匯出至檔案。在備份拓撲資料部分，無需其他步驟。</td>
    </tr>
    </tbody>
    </table>


5.  將中央管理存放區設定檔備份複製到 $Backup\\。

6.  備份位置資訊服務資料。在命令列輸入下列命令：
    
        Export-CsLisConfiguration -FileName <path and file name for backup>
    
    例如：
    
        Export-CsLisConfiguration -FileName "C:\E911Config.zip"

7.  將位置資訊服務設定檔的備份複製到 $Backup\\。

8.  備份前端集區與每個 Standard Edition 伺服器 後端資料庫上的使用者資料。在命令列輸入下列命令：
    
        Export-CsUserData -PoolFQDN <Fqdn> -FileName <String>
    
    例如：
    
        Export-CsUserData -PoolFQDN "atl-cs-001.litwareinc.com" -FileName "C:\Logs\ExportedUserData.zip"

9.  將使用者檔案的備份複製到 $Backup\\。

10. 在每個執行回應群組應用程式的集區上，備份回應群組設定。請執行下列步驟：
    
    1.  在命令列中輸入：
        
            Export-CsRgsConfiguration -Source "service:ApplicationServer:<pool FQDN>" -FileName <path and file name for backup>
        
        例如：
        
            Export-CsRgsConfiguration -Source ApplicationServer:pool01.contoso.com -FileName C:\RgsConfiguration.zip

11. 將回應群組設定檔的備份複製到 $Backup\\。

