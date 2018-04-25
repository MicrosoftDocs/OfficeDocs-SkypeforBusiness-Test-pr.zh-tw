---
title: Lync Server 2013 回應群組災害復原程序
TOCTitle: 回應群組災害復原程序
ms:assetid: b49577b7-0ca3-4f20-b614-f3a2a0046b58
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205186(v=OCS.15)
ms:contentKeyID: 49292068
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的回應群組災害復原程序

 

_**上次修改主題的時間：** 2012-11-01_

在災害復原的容錯移轉階段期間，回應群組位於多個集區中：在主要集區 (無法使用) 與備份集區。這兩個集區中的回應群組都有相同的名稱與相同的擁有者 (主要集區)，但他們有不同的父項。在此期間， 回應群組 Cmdlet 的運作方式會有些不同。請確定使用下列程序中指定的參數。如需關於在容錯移轉期間 Cmdlet 如何運作的詳細資訊，請參閱 NextHop 部落格文章＜Lync Server 2013：在災害復原期間回復回應群組＞，網址為 [http://go.microsoft.com/fwlink/?linkid=263957\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=263957%26clcid=0x404)。此部落格文章也適用於 Lync Server 2013 的正式版本。

使用下列程序中的步驟來準備與執行 Lync Server 回應群組服務的災害復原。

## 容錯移轉與容錯回復回應群組

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  定期執行備份。在命令列中輸入：
    
        Export-CsRgsConfiguration -Source "service:ApplicationServer:<primary pool FQDN>" -FileName "<backup path and file name>"
    
    例如：
    
        Export-CsRgsConfiguration -Source "service:ApplicationServer:primary.contoso.com" -FileName "C:\RgsExportPrimary.zip"

3.  在容錯移轉至備份集區後的中斷期間，將回應群組匯入備份集區。在命令列中輸入：
    
        Import-CsRgsConfiguration -Destination "service:ApplicationServer:<backup pool FQDN>" -FileName "<backup path and file name>"
    
    如果您想要將備份集區中的應用程式層級設定取代為來自主要集區的設定，請使用 ReplaceExistingSettings 參數，例如：
    
        Import-CsRgsConfiguration -Destination "service:ApplicationServer:backup.contoso.com" -FileName "C:\RgsExportPrimary.zip" -ReplaceExistingSettings
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ205186.Caution(OCS.15).gif" title="Caution" alt="Caution" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您不取代備份集區中的設定，且無法復原主要集區，則會遺失主要集區設定。如需詳細資訊，請參閱 <a href="lync-server-2013-planning-for-response-group-disaster-recovery.md">在 Lync Server 2013 中規劃回應群組災害復原</a>。</td>
    </tr>
    </tbody>
    </table>


4.  顯示匯入的回應群組，以確認匯入成功。匯入的回應群組仍為主要集區所擁有。請執行下列動作：
    
      - 顯示主要集區在備份集區中擁有的所有工作流程，並確認已包含所有主要集區工作流程。在命令列中輸入：
        
            Get-CsRgsWorkflow -Identity "service:ApplicationServer:<backup pool FQDN>" -Owner "service:ApplicationServer"<primary pool FQDN>
        
        例如：
        
            Get-CsRgsWorkflow -Identity "service:ApplicationServer:backup.contoso.com" -Owner "service:ApplicationServer:primary.contoso.com"
    
      - 顯示主要集區在備份集區中擁有的所有佇列，並確認已包含所有主要集區佇列。在命令列中輸入：
        
            Get-CsRgsQueue -Identity "service:ApplicationServer:<backup pool FQDN>" -Owner "service:ApplicationServer"<primary pool FQDN>
        
        例如：
        
            Get-CsRgsQueue -Identity "service:ApplicationServer:backup.contoso.com" -Owner "service:ApplicationServer"primary.contoso.com"
    
      - 顯示主要集區在備份集區中擁有的代理群組，並確認已包含所有主要集區代理群組。在命令列中輸入：
        
            Get-CsRgsAgentGroup -Identity "service:ApplicationServer:<backup pool FQDN>" -Owner "service:ApplicationServer"<primary pool FQDN>
        
        例如：
        
            Get-CsRgsAgentGroup -Identity "service:ApplicationServer:backup.contoso.com" -Owner "service:ApplicationServer"primary.contoso.com"
    
      - 顯示主要集區在備份集區中擁有的所有營業時間，並確認已包含所有主要集區營業時間。在命令列中輸入：
        
            Get-CsRgsHoursOfBusiness -Identity "service:ApplicationServer:<backup pool FQDN>" -Owner "service:ApplicationServer"<primary pool FQDN>
        
        例如：
        
            Get-CsRgsHoursOfBusiness -Identity "service:ApplicationServer:backup.contoso.com" -Owner "service:ApplicationServer"primary.contoso.com"
    
      - 顯示主要集區在備份集區中擁有的所有假日集，並確認已包含所有主要集區假日集。在命令列中輸入：
        
            Get-CsRgsHolidaySet -Identity "service:ApplicationServer:<backup pool FQDN>" -Owner "service:ApplicationServer"<primary pool FQDN>
        
        例如：
        
            Get-CsRgsHolidaySet -Identity "service:ApplicationServer:backup.contoso.com" -Owner "service:ApplicationServer"primary.contoso.com"
    
    或者，您可使用 –ShowAll 參數，而不使用 –Owner 參數來顯示備份集區中的所有回應群組，包含主要集區及備份集區擁有的回應群組。例如：
    
        Get-CsRgsWorkflow -Identity "service:ApplicationServer:<backup pool FQDN>" -ShowAll
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您必須使用 –ShowAll 參數或 –Owner 參數。如果您不使用這兩個參數，您匯入到備份集區的回應群組將不會列在 Cmdlet 傳回的結果中。</td>
    </tr>
    </tbody>
    </table>


5.  撥打電話到匯入的回應群組，並確認該通來電可被正確處理，以確認匯入順利。

6.  要求屬於正式代理群組之成員的代理登入其備份集區的代理群組。

7.  如常管理與修改匯入的回應群組。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>當回應群組位於備份集區時，您必須使用 Lync Server 管理命令介面來進行管理。您無法使用 Lync Server 控制台來管理您已匯入備份集區的回應群組。</td>
    </tr>
    </tbody>
    </table>


8.  還原主要集區且容錯回復完成後，將之前匯入備份集區的主要集區回應群組匯出。在命令列中輸入：
    
        Export-CsRgsConfiguration -Source ApplicationServer:<backup pool FQDN> -Owner ApplicationServer:<primary pool FQDN> -FileName "<backup path and file name>"

9.  將回應群組匯入回主要集區。在命令列中輸入：
    
        Import-CsRgsConfiguration -Destination "service:ApplicationServer:<primary pool FQDN>" -OverwriteOwner -FileName "<exported path and file name>"
    
    例如：
    
        Import-CsRgsConfiguration -Destination "service:ApplicationServer:primary.contoso.com" -OverwriteOwner -FileName "C:\RgsExportPrimaryUpdated.zip"
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您在復原期間重建集區，不管使用相同或不同的完整網域名稱 (FQDN)，您都必須使用 –OverwriteOwner 參數。根據一般規則，在您將回應群組匯入回主要集區時，一律可使用 –OverwriteOwner 參數。</td>
    </tr>
    </tbody>
    </table>
    
    如果您部署新的集區 (使用相同或不同的 FQDN) 來取代主要集區，且您想在新集區中使用來自備份集區的應用程式層級設定，請使用 –ReplaceExistingSettings 參數。請在命令列中輸入：
    
        Import-CsRgsConfiguration -Destination "service:ApplicationServer:<new primary pool FQDN>" -OverwriteOwner -FileName "<exported path and file name>" -ReplaceExistingSettings
    
    例如：
    
        Import-CsRgsConfiguration -Destination "service:ApplicationServer:newprimary.contoso.com" -OverwriteOwner -FileName "C:\RgsExportPrimaryUpdated.zip" -ReplaceExistingSettings
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您不想以來自備份集區的設定取代新集區的應用程式層級設定與預設的等候音樂音訊檔，新集區將使用預設的應用程式層級設定。</td>
    </tr>
    </tbody>
    </table>


10. 顯示匯入的回應群組設定，以確認匯入回主要集區的作業順利。請執行下列動作：
    
      - 顯示主要集區中的所有工作流程，並確認已包含所有匯入的工作流程。在命令列中輸入：
        
            Get-CsRgsWorkflow -Identity "service:ApplicationServer:<primary pool FQDN>" -ShowAll
        
        例如：
        
            Get-CsRgsWorkflow -Identity "service:ApplicationServer: primary.contoso.com" -ShowAll
    
      - 顯示主要集區中的所有佇列，並確認已包含所有匯入的佇列。在命令列中輸入：
        
            Get-CsRgsQueue -Identity "service:ApplicationServer:<primary pool FQDN>" -ShowAll
        
        例如：
        
            Get-CsRgsQueue -Identity "service:ApplicationServer:primary.contoso.com" -ShowAll
    
      - 顯示主要集區中的所有代理群組，並確認已包含所有匯入的代理群組。在命令列中輸入：
        
            Get-CsRgsAgentGroup -Identity "service:ApplicationServer: <primary pool FQDN>" -ShowAll
        
        例如：
        
            Get-CsRgsAgentGroup -Identity "service:ApplicationServer:primary.contoso.com" -ShowAll
    
      - 顯示主要集區中的所有營業時間，並確認已包含所有匯入的營業時間。在命令列中輸入：
        
            Get-CsRgsHoursOfBusiness -Identity "service:ApplicationServer:<primary pool FQDN>" -ShowAll
        
        例如：
        
            Get-CsRgsHoursOfBusiness -Identity "service:ApplicationServer:primary.contoso.com" -ShowAll
    
      - 顯示主要集區中的所有假日集，並確認已包含所有匯入的假日集。在命令列中輸入：
        
            Get-CsRgsHolidaySet -Identity "service:ApplicationServer:<primary pool FQDN>" -ShowAll
        
        例如：
        
            Get-CsRgsHolidaySet -Identity "service:ApplicationServer:primary.contoso.com" -ShowAll

11. 撥打電話到匯入的回應群組，並確認該通來電可被正確處理，以確認匯入順利。

12. 或者，從備份集區移除主要集區擁有的回應群組。在命令列中輸入：
    
        Export-CsRgsConfiguration -Source "service:ApplicationServer:<backup pool FQDN>" -Owner "service:ApplicationServer:<primary pool FQDN>" -FileName "<backup path and file name>" -RemoveExportedConfiguration
    
    例如：
    
        Export-CsRgsConfiguration -Source "service:ApplicationServer:backup.contoso.com" -Owner "service:ApplicationServer:primary.contoso.com" -FileName "C:\RgsExportPrimaryUpdated.zip" -RemoveExportedConfiguration
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>此步驟會使用匯出的設定來建立新檔案，然後將它從備份集區中移除。</td>
    </tr>
    </tbody>
    </table>

