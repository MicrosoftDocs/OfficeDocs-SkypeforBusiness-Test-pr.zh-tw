---
title: 還原 Standard Edition 伺服器
TOCTitle: 還原 Standard Edition 伺服器
ms:assetid: d1845663-3138-4fd6-b3e7-337e294d40d8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh202190(v=OCS.15)
ms:contentKeyID: 52056226
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 還原 Standard Edition 伺服器

 

_**上次修改主題的時間：** 2013-02-21_

若未執行中央管理存放區的 Standard Edition 伺服器失敗，請執行本節中的程序。若中央管理存放區失敗，請參閱＜[還原裝載中央管理存放區的伺服器](lync-server-2013-restoring-the-server-hosting-the-central-management-store.md)＞。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>建議您在還原之前，先擷取系統的影像複本，您可在還原出錯時，以此影像做為回復點。您可以在安裝作業系統及 SQL Server 之後擷取影像複本，然後再還原或重新註冊憑證。</td>
</tr>
</tbody>
</table>


## 還原 Standard Edition Server

1.  準備一部完整網域名稱 (FQDN) 與失敗電腦相同的乾淨或全新伺服器，然後安裝作業系統，再還原或重新註冊憑證。
    
    > [!NOTE]  
    > 遵循貴組織的伺服器部署程序執行此步驟。
    


2.  從 RTCUniversalServerAdmins 群組成員和本機系統管理員群組成員的使用者帳戶，登入所要還原的伺服器。

3.  將 $Backup 中適當的檔案存放區複製到伺服器上的檔案存放區位置，然後再共用該資料夾，以還原檔案存放區。
    
    > [!IMPORTANT]  
    > 還原後之檔案存放區的路徑與檔案名稱應與檔案存放區備份完全相同，如此使用該檔案的元件才可存取使用。
    


4.  執行拓撲產生器：
    
    1.  啟動拓撲產生器：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 拓撲產生器\]。
    
    2.  按一下 \[從現有部署下載拓撲\]，然後按一下 \[確定\]。
    
    3.  選取拓撲，然後按一下 \[儲存\]。按一下 \[是\] 確定您的選擇。

5.  瀏覽至 Lync Server 安裝資料夾或媒體，然後啟動 \\setup\\amd64\\Setup.exe 上的 Lync Server 部署精靈。使用 Lync Server 部署精靈執行下列作業：
    
    1.  執行 \[步驟 1: 安裝本機組態存放區\]，以安裝本機設定檔。
    
    2.  執行 \[步驟 2: 設定或移除 Lync Server 元件\]，以安裝 Lync Server 伺服器角色。
    
    3.  執行 \[步驟 3: 要求、安裝或指派憑證\]，以指派憑證。
    
    4.  執行 \[步驟 4: 啟動服務\]，以啟動伺服器上的服務。
    
    如需執行 \[部署精靈\] 的詳細資料，請參閱您要還原之伺服器角色的＜部署＞文件。

6.  執行下列動作還原使用者資料：
    
    1.  將 ExportedUserData.zip 從 $Backup\\ 複製到本機目錄。
    
    2.  還原使用者資料之前，必須先停止 Lync 服務。若要執行此項作業，請輸入：
        
            Stop-CsWindowsService
    
    3.  若要還原使用者資料，請在命令列上輸入：
        
            Import-CsUserData -PoolFqdn <Fqdn> -FileName <String>
        
        例如：
        
            Import-CsUserData -PoolFqdn "atl0cs-001.litwareinc.com" -FileName "C:\Logs\ExportedUserDatal.zip"
    
    4.  若要重新啟動 Lync 服務，請輸入︰
        
            Start-CsWindowsService

7.  若將您回應群組部署在 Standard Edition 伺服器 上，請還原回應群組設定資料。如需詳細資訊，請參閱＜[還原回應群組設定](lync-server-2013-restoring-response-group-settings.md)＞。

8.  如果您在 Standard Edition Server 上部署了常設聊天室，請還原常設聊天室資料庫 (mgc.mdf)。
    
    如果您使用 SQL Server Backup 備份常設聊天室資料庫，請使用 SQL Server 還原程序加以還原。
    
    如果您使用 Export-CsPersistentChatData Cmdlet 備份，請使用 Import-CsPersistentChatData 加以還原。

