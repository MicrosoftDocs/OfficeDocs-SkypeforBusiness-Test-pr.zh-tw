---
title: 手動清除詳細通話記錄與經驗品質資料庫
TOCTitle: 手動清除詳細通話記錄與經驗品質資料庫
ms:assetid: 3a3a965b-b861-41a4-b9a8-27184d622c17
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204812(v=OCS.15)
ms:contentKeyID: 49290633
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 手動清除詳細通話記錄與經驗品質資料庫

 

_**上次修改主題的時間：** 2014-07-07_

如上節所述，管理員可以設定「詳細通話記錄 (CDR)」及 (或)「經驗品質 (QoE)」資料庫，以自動從資料庫清除舊記錄；如果已經在指定資料庫 (CDR 或 QoE) 啟用清除，而且資料庫中有任何記錄超過指定的時間，清除才會發生。例如，管理員可以設定系統在每天早上 1:00 從 QoE 資料庫中刪除超過 60 天的 QoE 記錄。

除了自動清除之外，Microsoft Lync Server 2013 已經加入兩個新的 Cmdlet -- Invoke-CsCdrDatabasePurge 及 Invoke-CsQoEDatbasePurge；這些 Cmdlet 讓管理員可以隨時從 CDR 及 QoE 資料庫手動清除記錄。例如，如要從 CDR 資料庫中手動清除所有超過 10 天的記錄，可使用如下的命令：

    Invoke-CsCdrDatabasePurge -Identity MonitoringDatabase:atl-sql-001.litwareinc.com -PurgeCallDetailDataOlderThanDays 10 -PurgeDiagnosticDataOlderThanDays 10

在上述命令中，將會刪除在 atl-sql-001.litwareinc.com 的監控資料庫上所有超過 10 天的詳細通話記錄及診斷資料記錄。(詳細通話記錄為使用者/工作階段報告。診斷資料記錄為用戶端應用程式，如 Lync 2013，上傳的診斷記錄檔。)

如上所示，執行 Invoke-CsCdrDatabasePurge Cmdlet 時，必須同時包括 PurgeCallDetaiDataOlderThanDays 及 PurgeDiagnosticDataOlderThanDays 參數。不過，這些參數不需要設為相同的值。例如，可以清除資料庫中超過 10 天的詳細通話記錄，但同時保留所有的診斷資料記錄。要如此做的話，請將 PurgeCallDetailDataOlderThanDays 設為 10，而 PurgeDiagnosticDataOlderThanDays 設為 0。例如：

    Invoke-CsCdrDatabasePurge -Identity MonitoringDatabase:atl-sql-001.litwareinc.com -PurgeCallDetailDataOlderThanDays 10 -PurgeDiagnosticDataOlderThanDays 0

依預設，每次執行 Invoke-CsCdrDatabasePurge 時，針對每個必須清除的資料庫都會出現類似以下的提示：

    Confirm
    Are you sure you want to perform this action?
    Performing operation "Stored procedure: RtcCleanupDiag" on Target "Target SQL Server:atl-sql-001.litwareinc.com\archinst Database: lcscdr".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All [S] Suspend  [?] Help (default is "Y"):

您必須輸入 Y (是) 或 A (全部皆是)，才會實際清除資料庫。如要隱藏這些確認提示，請在呼叫 Invoke-CsCdrDatabasePurge 的結尾新增下列參數：

    -Confirm:$False

例如：

    Invoke-CsCdrDatabasePurge -Identity MonitoringDatabase:atl-sql-001.litwareinc.com -PurgeCallDetailDataOlderThanDays 10 -PurgeDiagnosticDataOlderThanDays 10 -Confirm:$False

如此做之後，確認提示就不會顯示，將立即清除資料庫。

如要清除 QoE 資料庫，則使用 Invoke-CsQoEDatabasePurge Cmdlet，並且指定要刪除之記錄的年齡 (天數)：

    Invoke-CsQoEDatabasePurge -Identity MonitoringDatabase:atl-sql-001.litwareinc.com -PurgeQoEDataOlderThanDays 10

