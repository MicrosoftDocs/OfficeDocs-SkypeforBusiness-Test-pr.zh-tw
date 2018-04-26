---
title: ABC 集區容錯移轉的備份先決條件
TOCTitle: ABC 集區容錯移轉的備份先決條件
ms:assetid: 652046f5-6086-4592-902d-d5789581977d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945634(v=OCS.15)
ms:contentKeyID: 52056141
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# ABC 集區容錯移轉的備份先決條件

 

_**上次修改主題的時間：** 2013-03-26_

若要利用 ABC 集區容錯移轉程序獲得最大的效益，您必須在發生災害與容錯移轉之前，先執行某些備份：

  - 您必須使用 **Export-CsLISConfiguration** Cmdlet 從集區 A 定期備份「位置資訊服務」(LIS) 設定資料。
    
        Export-csLisConfiguration -FileName <C:\LISExportPrimary.zip>

  - 您必須使用 **Export-CsRgsConfiguration** Cmdlet 從集區 A 定期備份「回應群組」設定資料。
    
        Export-CsRgsConfiguration -Source "service:ApplicationServer:<Pool A FQDN>" -FileName "C:\RgsExportPrimary.zip"
    
    一般而言，建議您執行每日備份，如果您有大量變更，可能會想排定更頻繁的備份。在這次災害事件中遺失的資訊量，取決於備份的頻率，以及變更的頻率和數量而定。
    
    「回應群組」應用程式每一個集區僅可儲存一組應用程式層級設定。這些設定可透過 **Get-CsRgsConfiguration** Cmdlet 存取。設定包含預設的等候音樂設定、預設的等候音樂音訊檔、代理人回電寬限期及來電內容設定。這些設定可利用 **ReplaceExistingSettings** 參數，透過 **Import-CsRgsConfiguration** Cmdlet 從一個集區傳輸至另一個集區，但是此作業會置換目的地集區中的任何應用程式層級設定。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在單獨的位置中，保留已用於設定「回應群組」應用程式 (也就是任何錄音檔案或等候音樂檔案) 之所有原始音訊檔的備份複本。</td>
    </tr>
    </tbody>
    </table>
    
    如果您有任何針對集區中「通話駐留」上傳之自訂的音樂保留檔案，應該將這些的複本保留在其他位置中。這些檔案未備份為 Lync Server 2013 災害復原程序的一部分，且如果上傳至集區的檔案毀壞、受損或遭到清除，就會遺失。
    
        Xcopy  <Source: Pool A CPS File Store Path>  <Destination>
        Example: Xcopy  "<Pool A File Store Path>\LyncFileStore\coX-ApplicationServer-X\AppServerFiles\CPS\"  "<Destination:  Backup location 1>"
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>「通話駐留」應用程式每一個集區僅可以儲存一組設定與一個自訂等候音樂音訊檔。這些設定可透過 <strong>Get-CsCpsConfiguration</strong> Cmdlet 存取。因為「通話駐留」的災害復原機制仰賴備份集區的「通話駐留」應用程式，如果發生災害，則不會備份或保留主要集區的設定。如果遺失主要集區，則無法復原這些設定，當部署新的集區以取代主要集區時，需要設定「通話駐留」設定與任何自訂等候音樂音訊檔。</td>
    </tr>
    </tbody>
    </table>


  - 如果您將任何宣告設定為「未指派號碼語音功能」的一部分，建議您將初始組態期間所使用的任何原始音訊檔副本保留在其他位置。如果不這麼做，您可以在要匯入音訊檔之伺服器或集區的檔案存放區中，取得已設定音訊檔的副本。這些檔案未備份為 Lync Server 2013 災害復原程序的一部分，且如果上傳至集區的檔案毀壞、受損或遭到清除，就會遺失。若要從伺服器或集區的檔案存放區中複製用於設定「未指派號碼語音功能」的所有音訊檔，請使用：
    
        Use: Xcopy  <Source: Pool A Announcement Service File Store Path>  <Destination>
        Example Usage:  Xcopy  "<Pool A File Store Path>\X-ApplicationServer-X\AppServerFiles\RGS\AS"  "<Destination: Backup location>"

  - 如果集區中有監控和封存資料庫，您應該使用 SQL Server 管理工具將其備份。在 ABC 容錯移轉程序中，如果監控和封存資料庫未在集區 A 中組合，則不會保留這些資料庫，因為這些資料庫未透過 Lync Server Backup Service 進行備份。

