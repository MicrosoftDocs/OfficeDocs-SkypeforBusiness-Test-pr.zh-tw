---
title: Lync Server 2013：將 Kerberos 驗證帳戶指派到網站
TOCTitle: 將 Kerberos 驗證帳戶指派到網站
ms:assetid: 3d9c587c-c8b8-4f81-8ed9-1458a31fc292
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425901(v=OCS.15)
ms:contentKeyID: 49290679
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中將 Kerberos 驗證帳戶指派到網站

 

_**上次修改主題的時間：** 2012-01-16_

若要順利完成此程序，您應以 RTCUniversalServerAdmins 群組成員的使用者身分登入。

建立 Kerberos 帳戶之後，您必須將它指派給網站。這必須是 Lync Server 2013 網站，而非 Active Directory 網站。每個部署可以建立多個 Kerberos 驗證帳戶，但只能指派一個帳戶給一個網站。使用下列程序，可指派先前建立的 Kerberos 驗證帳戶給網站。如需建立 Kerberos 帳戶的詳細資訊，請參閱＜ [在 Lync Server 2013 中建立 Kerberos 驗證帳戶](lync-server-2013-create-a-kerberos-authentication-account.md)＞。

## 若要指派 Kerberos 驗證帳戶給網站

1.  以 RTCUniversalServerAdmins 群組成員身分，登入網域中執行 Lync Server 2013 的電腦，或登入已安裝系統管理工具的電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  在命令提示字元中執行下列命令：
    
        New-CsKerberosAccountAssignment -UserAccount "Domain\UserAccount" -Identity "site:SiteName"
    
        Enable-CsTopology
    
    例如：
    
        New-CsKerberosAccountAssignment -UserAccount "contoso\kerbauth" -Identity "site:redmond"
    
        Enable-CsTopology
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您必須使用 Domain\User 格式指定 UserAccount 參數。不支援以 User@Domain.extension 格式來指稱基於 Kerberos 驗證目的而建立的電腦物件。</td>
    </tr>
    </tbody>
    </table>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>對 Kerberos 驗證進行變更之後 (如新增帳戶或移除帳戶)，您必須從 Lync Server 管理命令介面 命令提示字元執行 <strong>Enable-CsTopology</strong>。</td>
    </tr>
    </tbody>
    </table>

