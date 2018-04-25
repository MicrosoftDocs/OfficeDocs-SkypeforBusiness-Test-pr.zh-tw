---
title: Lync Server 2013：測試和報告 Kerberos 驗證的功能整備狀態
TOCTitle: 測試和報告 Kerberos 驗證的功能整備狀態
ms:assetid: d52c39e5-747d-4f29-88aa-30fd6f26b99c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398925(v=OCS.15)
ms:contentKeyID: 49292419
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中測試和報告 Kerberos 驗證的功能整備狀態

 

_**上次修改主題的時間：** 2012-01-16_

若要順利完成此程序，您應以 RTCUniversalServerAdmins 群組成員的使用者身分登入。

您可以使用 **Test-CsKerberosAccountAssignment**  Windows PowerShell Cmdlet 測試和報告 Kerberos 驗證的網站指派功能是否就緒。此命令會查詢必要的 Identity 參數中指定的網站。選用的 Report 參數會造成 Cmdlet 將 HTML 報告寫入命令執行所在電腦的 C:\\Logs。選用的 Verbose 參數會在畫面上報告活動資訊。

## 若要測試和報告網站的 Kerberos 驗證功能是否就緒

1.  以 RTCUniversalServerAdmins 群組成員身分登入網域中執行 Lync Server 2013 的電腦，或是登入安裝系統管理工具所在的電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  從命令列中，執行下列命令：
    
        Test-CsKerberosAccountAssignment -Identity "site:SiteName" -Report "c:\logs\FileName.htm" -Verbose
    
    例如：
    
        Test-CsKerberosAccountAssignment -Identity "site:Redmond" -Report "c:\logs\KerberosReport.htm" -Verbose

