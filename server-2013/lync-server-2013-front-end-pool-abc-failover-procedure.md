---
title: Lync Server 2013：前端集區 ABC 容錯移轉程序
TOCTitle: 前端集區 ABC 容錯移轉程序
ms:assetid: 67763ad3-6796-45eb-a486-901f21ac1a95
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945635(v=OCS.15)
ms:contentKeyID: 52056146
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的前端集區 ABC 容錯移轉程序

 

_**上次修改主題的時間：** 2014-05-22_

使用以下步驟執行 ABC 容錯移轉程序。此程序包含每一個步驟的高階說明，後面加上命令以及要為每一個步驟執行的 Cmdlet。

若要執行 Cmdlet，請使用 \[以系統管理員身分執行\] 開啟 Lync Server 管理命令介面。

## 執行 ABC 容錯移轉

1.  檢查集區 A 是否由中央管理伺服器 (CMS) 主控。
    
      - 執行下列 Cmdlet：
        
            Get-CsService -CentralManagement
        
        如果作用中 CMS 的識別欄位指向集區 A 的完整網域名稱 (FQDN)，可使用此程序的步驟 2 和步驟 3 先對中央管理伺服器進行容錯移轉。否則，請跳至步驟 4。

2.  藉由執行以下 Cmdlet，在災害復原模式中將 CMS 容錯移轉至集區 B：
    
        Invoke-CsManagementServerFailover -BackupSqlServerFqdn <Pool B BE FQDN> -BackupSqlInstanceName <Pool B BE instance name> [-BackupMirrorSqlServerFqdn <Pool B Mirror BE FQDN> -BackupMirrorSqlInstanceName <Pool B Mirror BE Instance name>] -Force -Verbose
    
    執行此作業後，建議您對額外的恢復功能將 CMS 從集區 B 移至其他現有的配對集區。如需詳細資訊，請參閱＜ [Move-CsManagementServer](move-csmanagementserver.md)＞。

3.  如果集區 A 包含 CMS，請將 LIS 設定從集區 A 匯入集區 B 的 LIS 資料庫 (Lis.mdf)。只有在已定期備份 LIS 資料時，才會發生作用。若要匯入 LIS 設定，請執行下列 Cmdlet：
    
        Import-CsLisConfiguration -FileName <String> 
        Publish-CsLisConfiguration

4.  將備份的 Lync Server 回應群組服務工作流程從集區 A 匯入集區 B。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>目前， <strong>Import-CsRgsConfiguration</strong> Cmdlet 要求集區 A 上的佇列與工作流程名稱與集區 B 上的佇列與工作流程名稱不同。如果名稱沒有任何不同，則在執行 <strong>Import-CsRgsConfiguration</strong> Cmdlet 時會發生錯誤，而且必須先在集區 B 中重新命名佇列與工作流程，才可繼續執行 <strong>Import-CsRgsConfiguration</strong> Cmdlet。</td>
    </tr>
    </tbody>
    </table>
    
    您有兩種選擇可將回應群組設定從集區 A 匯入集區 B。使用的方法取決於您是否想以集區 A 的應用程式層級設定覆寫集區 B 的應用程式層級設定。
    
      - 如果您想要覆寫集區 B 設定，請執行包含 \[ReplaceExistingSettings\] 選項的 **Import-CsRgsConfiguration** Cmdlet：
        
            Import-CsRgsConfiguration -Destination "service:ApplicationServer:<Pool B FQDN>" -FileName "C:\RgsExportPrimary.zip"  -ReplaceExistingRgsSettings
    
      - 如果您不想覆寫集區 B 設定，請使用不含 \[ReplaceExistingSettings\] 選項的 **Import-CsRgsConfiguration** Cmdlet。
        
            Import-CsRgsConfiguration -Destination "service:ApplicationServer:<Pool B FQDN>" -FileName "C:\RgsExportPrimary.zip"
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>請謹記，如果您不想以主要集區 (集區 A) 的設定覆寫備份集區 (集區 B) 的應用程式層級設定，當集區 A 遺失時，集區 A 的應用程式層級設定也會跟著遺失，因為「回應群組」應用程式只能對每一個集區儲存一組應用程式層級設定。若已部署集區 C 以取代集區 A，則必須重新設定應用程式層級設定，包含預設的等候音樂音訊檔。</td>
    </tr>
    </tbody>
    </table>


5.  執行以下 Cmedlet 顯示匯入的回應群組，以確認成功匯入「回應群組」設定。請注意，匯入的回應群組仍屬於集區 A。
    
        Get-CsRgsWorkflow -Identity "service:ApplicationServer:<Pool B FQDN>" -Owner "service:ApplicationServer:<Pool A FQDN>"
        
        Get-CsRgsQueue -Identity "service:ApplicationServer:<Pool B FQDN>" -Owner "service:ApplicationServer:<Pool A FQDN>"
        
        Get-CsRgsAgentGroup -Identity "service:ApplicationServer:<Pool B FQDN>" -Owner "service:ApplicationServer:<Pool A FQDN>"

6.  對於「未指派號碼」，將使用「宣告」做為所選取宣告服務的「未指派號碼」範圍從集區 A 移至集區 B。若要執行此作業，請執行下列動作：
    
      - 在集區 B 中重新建立部署於集區 A 的所有宣告。如果在集區 A 中部署宣告時使用了任何音訊檔，則這些檔案需要在集區 B 中重新建立宣告。若要在集區 B 中重新建立宣告，請使用 **New-CsAnnouncement** Cmdlet 搭配集區 B 做為父服務。
    
      - 重新鎖定針對集區 B 新部署的宣告提供集區 A 之宣告的所有未指派號碼範圍。對每一個提供集區 A 之宣告的未指派號碼執行下列 Cmdlet：
        
            Set-CsUnassignedNumber -Identity "<Range Name>" -AnnouncementService "<Pool B FQDN>" -AnnouncementName "<New Announcement in pool B>"
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>對於使用 &quot;Exchange UM&quot; 做為所選取之宣告服務的未指派號碼範圍不需要此步驟。</td>
    </tr>
    </tbody>
    </table>


7.  執行下列 Cmdlet，在災害復原 (DR) 模式中將集區 A 容錯移轉至集區 B：
    
        Invoke-CsPoolFailover -PoolFqdn <Pool A FQDN> -DisasterMode

8.  建置集區 C，但不要啟動集區 C 的任何服務。
    
    請注意，此步驟可同時與步驟 5 和步驟 6 同時執行。

9.  執行下列 Cmdlet，強制將位於集區 A 的使用者移至集區 C：
    
        Get-csuser -Filter {RegistrarPool -eq "<Pool A FQDN>"} | Move-CsUser -Target <Pool C FQDN> -Force
    
    此時，位於集區 A 的使用者開始遇到服務中斷。此中斷會持續到步驟 16，那時候會在集區 C 啟動服務。

10. 執行下列 Cmdlet，強制將集區 A 的會議目錄移至集區 C：
    
        Move-CsConferenceDirectory -Identity <Conference Directory ID of Pool A> -TargetPool <Pool C FQDN> -Force

11. 執行下列 Cmdlet，強制將會議自動語音應答 (CAA) 連絡人物件從集區 A 移至集區 C：
    
        Move-csApplicationEndpoint -Identity "<Pool A CAA Uri>" -targetApplicationPool <Pool C FQDN> -force

12. 將會議內容從集區 B 複製到集區 C。

13. 執行下列 Cmdlet，將使用者資料從集區 B 匯出，並匯入集區 C：
    
        Export-CsUserData -PoolFqdn <Pool B Fqdn> -FileName <String>
        Import-CsUserData -PoolFqdn <Pool C Fqdn> -FileName <String>

14. 將備份的通話駐留應用程式資料從集區 A 還原至集區 C，並將集區 A 的通話駐留範圍指派至集區 C。
    
      - 您可以透過 Lync Server 控制台或 Lync Server 管理命令介面將集區 A 的通話駐留範圍重新指派至集區 C。針對 Lync Server 管理命令介面，為每一個指派給集區 A 的通話駐留範圍執行下列 Cmdlet (請注意 Identity 參數是指屬於集區 A 的通話駐留範圍)：
        
            Set-CsCallParkOrbit -Identity "<Call Park Orbit Identity>" -CallParkService "service:ApplicationServer:<Pool C FQDN>"
    
      - 如果已針對集區 A 中的通話駐留設定自訂等候音樂，會還原集區 C 中的通話駐留自訂等候音樂檔案。
        
            Xcopy <Source> <Destination: Pool C CPS File Store Path>
        
        例如：
        
            Xcopy "Source Path" "<Pool C File Store Path>\OcsFileStore\coX-ApplicationServer-X\AppServerFiles\CPS\"
    
      - 最後，使用 **Set-CsCpsConfiguration** Cmdlet 重新設定集區 C 的通話駐留設定。通話駐留應用程式對每一個集區僅可還原一組設定和一個自訂音樂保留音訊檔，而且在災害事件中不會備份或保留這些設定。

15. 如果 常設聊天室的下一個躍點集區指向集區 A，請進行並發行拓撲變更以便下一個躍點伺服器指向集區 C。
    
      - 在拓撲產生器中，將 常設聊天室集區變更為指向集區 C，以做為其下一個躍點。若要執行此作業，請以滑鼠右鍵按一下 常設聊天室集區，然後按一下 \[一般\] 索引標籤，然後在 \[下一個躍點集區\] 中輸入集區 C 的名稱。
    
      - 執行下列 Cmdlet，啟動集區 C 的服務：
        
            Start-csWindowsService
    
    此時，原本位於集區 A 的使用者服務中斷即結束。

16. 執行下列 Cmdlet，從集區 A 擁有的集區 B 匯出 Lync Server 回應群組服務工作流程，以供匯入集區 C：
    
        Export-CsRgsConfiguration -Source "service:ApplicationServer:<Pool B FQDN>" -Owner "service:ApplicationServer:<Pool A FQDN>" -FileName "C:\RgsExportPrimaryUpdated.zip" 

17. 將 Lync Server 回應群組服務工作流程從集區 B 匯入集區 C。
    
    您有兩種作法可將回應群組設定從集區 B 匯入集區 C。使用的方法取決於您是否要以集區 B 中的應用程式層級設定覆寫集區 C 中的應用程式層級設定。
    
      - 如果您想要覆寫集區 C 設定，請執行包含 \[ReplaceExistingSettings\] 選項的 **Import-CsRgsConfiguration** Cmdlet：
        
            Import-CsRgsConfiguration -Destination "service:ApplicationServer:<Pool C FQDN>" -FileName "C:\RgsExportPrimary.zip"  -ReplaceExistingRgsSettings
    
      - 如果您不想覆寫集區 C 設定，請使用不含 \[ReplaceExistingSettings\] 選項的 **Import-CsRgsConfiguration** Cmdlet：
        
            Import-CsRgsConfiguration -Destination "service:ApplicationServer:<Pool B FQDN>" -FileName "C:\RgsExportPrimary.zip"
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>請謹記，如果您不想以備份集區 (集區 B) 的設定覆寫集區 C 的應用程式層級設定，則集區 B 的應用程式層級設定將會遺失，因為回應群組對每一個集區只能儲存一組應用程式層級設定。</td>
    </tr>
    </tbody>
    </table>


18. 執行下列 Cmdlet 以顯示回應群組已匯入集區 C，確認回應群組設定已匯入成功。
    
        Get-CsRgsWorkflow -Identity "service:ApplicationServer:<Pool C FQDN>" -ShowAll
         Get-CsRgsQueue -Identity "service:ApplicationServer:<Pool C FQDN>" -ShowAll
        Get-CsRgsAgentGroup -Identity "service:ApplicationServer:<Pool C FQDN>" -ShowAll

19. 當匯入的設定已在集區 C 中確認，請將主要集區擁有的回應群組從集區 B 中移除。如此可將回應群組的停機時間降至最低。
    
    此步驟會建立包含已匯出設定的新檔案，然後從集區 B 移除檔案。
    
        Export-CsRgsConfiguration -Source "service:ApplicationServer:<Pool B FQDN>" -Owner "service:ApplicationServer:<Pool A FQDN>" -FileName "C:\RgsExportPrimaryUpdated.zip" -RemoveExportedConfiguration

20. 移至未指派號碼範圍已從集區 A 移至集區 B 的集區 C。
    
      - 在集區 C 中重新建立已在集區 B 中從集區 A 重新建立的所有宣告。如果部署要移動的宣告時，會使用任何音訊檔，您需要利用這些檔案以在集區 C 重新建立宣告。若要在集區 C 中重新建立宣告，請使用 **New-CsAnnouncement** Cmdlet 搭配集區 C 做為父服務。
    
      - 重新鎖定所有未指派號碼範圍已從集區 A 重新鎖定至集區 B 的集區 C。對每一個需要重新鎖定的未指派號碼範圍執行下列 Cmdlet：
        
            Set-CsUnassignedNumber -Identity "<Range Name>" -AnnouncementService "<Pool C FQDN>" -AnnouncementName "<New Announcement in pool C>"
    
      - (選用) 如果集區 B 中不再使用這些宣告，請從集區 B 移除在集區 C 中重新建立的宣告。若要移除宣告，請使用 **Remove-CsAnnouncement** Cmdlet。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>對於使用 &quot;Exchange UM&quot; 做為宣告服務的未指派號碼範圍不需要此步驟。</td>
        </tr>
        </tbody>
        </table>


21. 執行下列 Cmdlet，在集區 B 中清除集區 A 的使用者資料：
    
        Remove-CsUserStoreBackupData -PoolFqdn <Pool B FQDN> -Verbose

22. 在拓撲產生器中執行下列動作：
    
      - 解除配對集區 A 和集區 B。配對集區 B 和集區 C。然後將集區 A 從拓撲中移除並加以發行。若要執行此作業，請執行下列動作：
        
          - 在拓撲產生器中，以滑鼠右鍵按一下集區 B，然後按一下 \[編輯內容\] 。
        
          - 按一下左側窗格中的 \[恢復\] 。
        
          - 在下方 \[關聯的備份集區\] 中，選取集區 C。請注意，\[關聯的備份集區\] 選取方塊一開始會顯示集區 A，因為集區 B 先前已與此集區建立關聯。
        
          - 選取 \[語音自動容錯移轉和容錯回復\] ，然後按一下 \[確定\] 。
            
            當您檢視關於此集區的詳細資訊時，相關聯的集區會立即顯示在 \[恢復\] 之下的右側窗格中。
        
          - 在主控台樹狀目錄中，以滑鼠右鍵按一下集區 A，然後按一下 \[刪除\]。
        
          - 發行拓撲。

23. 在集區 C 中執行啟動載入應用程式以安裝備份服務應用程式，然後在集區 C 中的本機機器上，從部署資料夾執行下列動作以啟動備份服務應用程式：
    
        Run "%SYSTEMROOT%\Program Files\Microsoft Lync Server 2013\Deployment\Bootstrapper.exe"
        Start-CsWindowsService -name LyncBackup

24. 執行下列 Cmdlet，在集區 B 上重新啟動備份服務應用程式：
    
        Stop-CsWindowsService -name LyncBackup
        Start-CsWindowsService -name LyncBackup

25. 如果集區 C 是 Standard Edition (SE) 集區，且集區 B 具備 CMS，請執行下列 Cmdlet，以在集區 C 上手動安裝 CMS 資料庫：
    
        Install-CsDatabase -CentralManagementDatabase -SqlServerFqdn <Pool C FQDN> -SqlInstanceName rtc

26. 呼叫備份服務，先將舊的會議內容從集區 B 同步至產生的集區 C，然後再配對 B 和 C，接著將新的會議內容從集區 C 同步至啟動集區 C 之後產生的集區 B，然後再配對 B 和 C。若要執行此作業，請執行下列 Cmdlet：
    
        Invoke-CsBackupServiceSync -PoolFqdn <Pool C FQDN>
        Invoke-CsBackupServiceSync -PoolFqdn <Pool B FQDN>

27. 針對每一個與集區 A 相關聯的 Survivable Branch Appliance：
    
      - 執行下列 Cmdlet 以關閉 SBA X：
        
            Stop-CsWindowsService
    
      - 建立包含位於 SBA X 之使用者清單的檔案。當使用者在步驟 30 中移回 SBA X 時，將需要此清單。若要執行此作業，請執行下列 Cmdlet：
        
            Get-CsUser -Filter {RegistrarPool -eq "<SBA X FQDN>"} | Export-Csv d:\sbaxusers.txt
    
      - 執行下列 Cmdlet，強制將位於 SBA X 的使用者移至集區 C：
        
            Get-CsUser -Filter {RegistrarPool -eq "<SBA X FQDN>"} | Move-CsUser -Target <Pool C FQDN> -Force -Verbose
    
      - 先執行下列 Cmdlet 以更新這些使用者的資料：
        
            Convert-csUserData -InputFile <Data file exported from PoolB> -OutputFile c:\Logs\ExportedUserData.xml -TargetVersionLync2010 
            $a=get-csuser -Filter {RegistrarPool -eq "FQDN of SBA X"} | select SipAddress
            foreach($x in $a) {$x.SipAddress.Substring(4) >> users.txt}
        
        然後執行此指令碼：
        
            $users=gc c:\logs\users.txt
            foreach ($user in $users)
            {
            Update-CsUserData -FileName c:\logs\exportedUserDAta.xml -UserFilter $user - 
            }
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>位於與集區 A 相關聯之 SBA 的使用者會發生服務中斷，直到這些使用者移至集區 C 為止。</td>
        </tr>
        </tbody>
        </table>


28. 在拓撲產生器中，對先前與集區 A 相關聯的每一個 SBA X，執行下列動作：
    
      - 變更與集區 C 的關聯。若要執行此作業，請按一下分支網站，展開 \[Survivable Branch Appliances 或Servers\] 節點，然後按一下 \[Survivable Branch Appliance\] 。接著，選取 Survivable Branch Appliance 將連線至集區 C 的 \[前端集區\]、\[使用者服務集區\] ，然後按 \[下一步\] 。
    
      - 發行拓撲。若要執行此作業，請在主控台樹狀目錄中，以滑鼠右鍵依序按一下新的 \[Survivable Branch Appliance\] 、\[拓撲\] ，然後按一下 \[發行\] 。

29. 針對目前與集區 C 相關聯的每一個 SBA X：
    
      - 在 Survivable Branch Appliance 上執行下列 Cmdlet 以啟動 SBA X：
        
            Start-CsWindowsService
    
      - 執行下列 Cmdlet，將原位於 SBA X 的使用者從集區 C 移至 SBA X。
        
            Import-Csv d:\sbaxusers.txt | Move-CsUser -Target <SBA X FQDN> -Force

