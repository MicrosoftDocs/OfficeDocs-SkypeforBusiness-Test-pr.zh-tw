---
title: Lync Server 2013：移除網站中的 Kerberos 驗證
TOCTitle: 移除網站中的 Kerberos 驗證
ms:assetid: 93171b02-bb36-42dc-943d-86d9dde45b59
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398749(v=OCS.15)
ms:contentKeyID: 49291683
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中從網站移除 Kerberos 驗證

 

_**上次修改主題的時間：** 2012-01-16_

若要順利完成此程序，您應以 RTCUniversalServerAdmins 群組成員的使用者身分登入。

如果您需要移除某個網站的 Kerberos 驗證或撤銷網站，必須使用 **Remove-CsKerberosAccountAssignment** Cmdlet 移除網站的 Kerberos 驗證帳戶指派。請使用下列程序來移除 Kerberos 驗證帳戶指派，此程序會移除網站中所有電腦的指派。

<table>
<thead>
<tr class="header">
<th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您要永久撤銷啟用 Kerberos 的帳戶，在移除指派後應使用「Active Directory 使用者和電腦」刪除 Active Directory 網域服務 中的帳戶。如果您想要在日後使用物件，不妨保留 Active Directory 物件。</td>
</tr>
</tbody>
</table>


## 若要移除網站的 Kerberos 驗證

1.  以 RTCUniversalServerAdmins 群組成員身分，登入網域中執行 Lync Server 2013 的電腦，或登入已安裝系統管理工具的電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  在命令提示字元中執行下列命令：
    
        Remove-CsKerberosAccountAssignment -Identity "site:SiteName"
    
        Enable-CsTopology
    
    例如：
    
        Remove-CsKerberosAccountAssignment -Identity "site:Redmond"
    
        Enable-CsTopology
    
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

