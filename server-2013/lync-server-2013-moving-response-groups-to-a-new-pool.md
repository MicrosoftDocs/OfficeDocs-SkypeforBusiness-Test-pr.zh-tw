---
title: 將回應群組移到新集區
TOCTitle: 將回應群組移到新集區
ms:assetid: da0db765-41e5-430b-b5a7-5418ec5ff2a7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205298(v=OCS.15)
ms:contentKeyID: 49292493
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 將回應群組移到新集區

 

_**上次修改主題的時間：** 2012-11-01_

Lync Server 2013 引進的新 Cmdlet 支援在集區之間移動回應群組，甚至是在完整網域名稱 (FQDN) 不同時。

使用下列程序中的步驟，可將回應群組從一個前端集區移動到有不同 FQDN 的另一個前端集區。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在共存環境中，只能在 Lync Server 2013前端集區之間移動回應群組。</td>
</tr>
</tbody>
</table>


## 將回應群組移動到有不同 FQDN 的集區

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  匯出來源集區中的回應群組。在命令列中輸入：
    
        Export-CsRgsConfiguration -Source "service:ApplicationServer:<source FQDN>" -FileName "<export file name>"
    
    例如：
    
        Export-CsRgsConfiguration -Source "service:ApplicationServer:source.contoso.com" -FileName "C:\RgsExportSource.zip"
    
    若要在匯出期間移除來源集區中的回應群組，請加上 –RemoveExportedConfiguration 參數。例如：
    
        Export-CsRgsConfiguration -Source ApplicationServer:source.contoso.com -FileName "C:\RgsExportSource.zip" -RemoveExportedConfiguration

3.  將回應群組匯入目的地集區，然後將目的地集區指派為新的擁有者。在命令列中輸入：
    
        Import-CsRgsConfiguration -Destination "service:ApplicationServer:<destination pool>" -FileName "<export file name>" -OverwriteOwner
    
    如果您也想要將回應群組應用程式層級設定從來源集區複製到目的地集區，請加上 –ReplaceExistingSettings 參數。您只能在每個集區定義一組應用程式層級設定。如果您將應用程式層級設定從來源集區複製到目的地集區，來源集區的設定就會取代目的地集區的設定。如果您不複製來源集區中的應用程式層級設定，匯入的回應群組就會套用目的地集區的現有設定。
    
    例如：
    
        Import-CsRgsConfiguration -Destination "service:ApplicationServer:destination.contoso.com" -FileName "C:\RgsExportSource.zip" -OverwriteOwner -ReplaceExistingSettings
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>應用程式層級設定包含預設的保留音樂設定、預設的保留音樂音訊檔、代理人回電寬限期及來電內容設定。若要檢視這些組態設定，請執行 <strong>Get-CsRgsConfiguration</strong> Cmdlet。如需此 Cmdlet 的詳細資訊，請參閱＜<a href="get-csrgsconfiguration.md">Get-CsRgsConfiguration</a>＞。</td>
    </tr>
    </tbody>
    </table>


4.  執行下列動作來顯示匯入的回應群組設定，確認匯入成功：
    
      - 確認所有工作流程均已匯入。在命令列輸入下列命令：
        
            Get-CsRgsWorkflow -Identity "service:ApplicationServer:<destination pool FQDN>"
    
      - 確認所有佇列均已匯入。在命令列輸入下列命令：
        
            Get-CsRgsQueue -Identity "service:ApplicationServer:<destination pool FQDN>"
    
      - 確認所有代理人群組均已匯入。在命令列輸入下列命令：
        
            Get-CsRgsAgentGroup -Identity "service:ApplicationServer:<destination pool FQDN>"
    
      - 確認所有營業時間均已匯入。在命令列輸入下列命令：
        
            Get-CsRgsHoursOfBusiness -Identity "service:ApplicationServer:<destination pool FQDN>" 
    
      - 確認所有假日集均已匯入。在命令列輸入下列命令：
        
            Get-CsRgsHolidaySet -Identity "service:ApplicationServer:<destination pool FQDN>" 

5.  撥打電話給其中一個對應群組，並確認可正確處理該通電話，以確認匯出成功。

6.  要求身為正式代理人群組成員的代理人登入其在目的地集區中的代理人群組。

7.  如果您先前並未移除來源集區中的回應群組，請從來源集區中移除回應群組。在命令列中輸入：
    
        Export-CsRgsConfiguration -Source "service:ApplicationServer:<source pool FQDN> -RemoveExportedConfiguration -FileName "<temporary export file name>"
    
    例如：
    
        Export-CsRgsConfiguration -Source "service:ApplicationServer:source.contoso.com" -RemoveExportedConfiguration -FileName "C:\TempRGsConfiguration.zip"

