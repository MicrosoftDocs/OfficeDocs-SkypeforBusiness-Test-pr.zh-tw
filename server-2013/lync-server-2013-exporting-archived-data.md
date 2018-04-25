---
title: 從 Lync Server 2013 匯出封存資料
TOCTitle: 從 Lync Server 2013 匯出封存資料
ms:assetid: 09450d54-769b-4741-924b-e390664d506f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204657(v=OCS.15)
ms:contentKeyID: 49290020
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 從 Lync Server 2013 匯出封存資料

 

_**上次修改主題的時間：** 2013-02-23_

封存在封存資料庫中的資料無法搜尋或者不是可讀格式，但是您可以使用 Export-CsArchivingData Cmdlet 從資料庫擷取記錄，並儲存為 Outlook 電子郵件 (EML) 檔案。如需匯出封存資料的詳細資訊，請參閱操作文件中的＜[Export-CsArchivingData](export-csarchivingdata.md)＞。

如果您啟用 Microsoft Exchange 整合，資料會封存在 Exchange 2013 儲存區。封存在 Exchange 2013 的資料可供搜尋及探查。如需 Exchange 2013 及 Lync Server 2013 整合的通訊支援的詳細資訊，請參閱支援文件中的＜[Lync Server 2013 中的 Exchange Server 與 SharePoint 整合支援](lync-server-2013-exchange-and-sharepoint-integration-support.md)＞。如需存取封存在 Exchange 之資料的詳細資訊，請參閱 Exchange 2013 文件。

## 使用Lync Server 管理命令介面 Cmdlet 匯出封存資料

您可以使用 Export-CSArchivingData Cmdlet 來匯出封存資料。此 Cmdlet 可從 Lync Server 2013 管理命令介面或從 Windows PowerShell 的遠端工作階段執行。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

**匯出封存資料**

  - 此命令會匯出自 2012 年 6 月 1 日起寫入封存資料庫 atl-sql-001.litwareinc.com 中的所有封存資料。所產生的輸出檔案會儲存在 C:\\ArchivingExports 資料夾中。
    
        Export-CsArchivingData -Identity "ArchivingDatabase:atl-sql-001.litwareinc.com" -StartDate 6/1/2012 -OutputFolder "C:\ArchivingExports"

**匯出單一使用者的封存資料**

  - 下列命令會匯出單一使用者 kenmyer@litwareinc.com 的封存資料。執行時需包含 UserUri 參數，後面接使用者的 SIP 位址。例如：
    
        Export-CsArchivingData -Identity "ArchivingDatabase:atl-sql-001.litwareinc.com" -StartDate 6/1/2012 -OutputFolder "C:\ArchivingExports" -UserUri "sip:kenmyer@litwareinc.com"

如需詳細資訊，請參閱 [Export-CsArchivingData](export-csarchivingdata.md) Cmdlet 的說明主題。

## 請參閱

#### 概念

[Lync Server 2013 中的 Exchange Server 與 SharePoint 整合支援](lync-server-2013-exchange-and-sharepoint-integration-support.md)  

#### 其他資源

[Export-CsArchivingData](export-csarchivingdata.md)  
[管理 Lync Server 2013 封存](lync-server-2013-managing-archiving.md)

