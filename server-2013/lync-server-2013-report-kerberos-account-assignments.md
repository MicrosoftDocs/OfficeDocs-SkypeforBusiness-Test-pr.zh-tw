---
title: Lync Server 2013：報告 Kerberos 帳戶指派
TOCTitle: 報告 Kerberos 帳戶指派
ms:assetid: 523231f6-81b3-454b-996d-663d9bd5cf83
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398343(v=OCS.15)
ms:contentKeyID: 49290916
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中報告 Kerberos 帳戶指派

 

_**上次修改主題的時間：** 2012-01-16_

若要順利完成此程序，您應以 RTCUniversalServerAdmins 群組成員的使用者身分登入。

您可以使用 **Get-CsKerberosAccountAssignment** Cmdlet 查詢 Kerberos 驗證帳戶指派項目相關資訊，並回報部署中目前指派項目相關資訊。

## 若要查詢網站的 Kerberos 驗證帳戶指派項目

1.  以 RTCUniversalServerAdmins 群組成員身分，登入網域中執行 Lync Server 2013 的電腦，或登入已安裝系統管理工具的電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  從命令列中執行下列其中一個命令：
    
      - 若要查詢組織裡所有 Kerberos 驗證帳戶指派項目，並傳回這些項目的個別指派資訊，請執行不含任何參數的 Cmdlet：
        
            Get-CsKerberosAccountAssignment
    
      - 若要查詢部署中所有 Kerberos 驗證帳戶指派項目，並傳回這些項目的個別網站指派資訊，請執行含 Identity 參數的 Cmdlet：
        
            Get-CsKerberosAccountAssignment -Identity "site:SiteName"
        
        例如：
        
            Get-CsKerberosAccountAssignment -Identity "site:Redmond"
    
      - 若要查詢單一網站中所有 Kerberos 驗證帳戶指派項目，並傳回這些項目的指派資訊，請執行含 Filter 參數的 Cmdlet：
        
            Get-CsKerberosAccountAssignment -Filter "SiteName"
        
        例如：
        
            Get-CsKerberosAccountAssignment -Filter "*Redmond"
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>指定 Filter 參數的 *SiteName 會傳回在網站識別元的任意位置包含指定網站名稱之所有網站 (例如，在網站識別元中包含 Redmond 字串的所有網站) 的相關資訊。</td>
        </tr>
        </tbody>
        </table>

