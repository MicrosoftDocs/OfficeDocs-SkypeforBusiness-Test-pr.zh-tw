---
title: Lync Server 2013：同步處理 Kerberos 驗證帳戶密碼至 IIS
TOCTitle: 同步處理 Kerberos 驗證帳戶密碼至 IIS
ms:assetid: 05925a66-2684-4c1b-adfa-69bd0da1bf38
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398107(v=OCS.15)
ms:contentKeyID: 49289960
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中同步處理 Kerberos 驗證帳戶密碼至 IIS

 

_**上次修改主題的時間：** 2010-11-08_

若要順利完成此程序，您應以 RTCUniversalServerAdmins 群組成員的使用者身分登入。

在網站中，前端伺服器、Standard Edition Server 和 Director 可以為了驗證 Web 服務 服務要求的目的，使用 Kerberos 驗證帳戶。這個程序會在已指派 Kerberos 帳戶的網站中尋找每一部執行 Web 服務 的伺服器，然後更新 Internet Information Services (IIS) 組態設定以使用 Kerberos 帳戶。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中於伺服器上設定 Kerberos 驗證帳戶密碼](lync-server-2013-set-a-kerberos-authentication-account-password-on-a-server.md)＞。

## 若要設定 Kerberos 驗證帳戶密碼

1.  以 RTCUniversalServerAdmins 群組成員的身分登入來源電腦 (例如 fe01.contoso.com)。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  在 Lync Server 管理命令介面 命令列中執行下列兩個命令：
    
        Set-CsKerberosAccountPassword -FromComputer SourceComputer -ToComputer DestinationComputer
    
    例如：
    
        Set-CsKerberosAccountPassword -FromComputer fe01.contoso.com -ToComputer dir01.contoso.com
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>來源電腦和目的地電腦的名稱必須是伺服器的完整網域名稱 (FQDN)。除非 FQDN 集區名稱與您作為來源電腦或目的地電腦使用的電腦名稱相同，否則您無法使用該集區 FQDN。</td>
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

