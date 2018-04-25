---
title: Lync Server 2013：委派設定權限
TOCTitle: 委派設定權限
ms:assetid: 9dca1683-4c69-4534-8ebe-6bd635cbae49
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412735(v=OCS.15)
ms:contentKeyID: 49291816
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中委派設定權限

 

_**上次修改主題的時間：** 2014-02-05_

如果您不想要將 Domain Admins 群組的成員資格授與部署 Lync Server 2013 的使用者或群組，可以讓 RTCUniversalServerAdmins 群組中的成員在執行 Lync Server 2013 的伺服器上執行 **Enable-CsTopology**  Windows PowerShell Cmdlet。根據預設，RTCUniversalServerAdmins 群組的成員不具有執行此 Cmdlet 的權限。您可以藉由使用 **Grant-CsSetupPermission** Cmdlet 並指定執行 Lync Server 2013 之伺服器的電腦物件所在的組織單位 (OU)，授與在執行 Lync Server 之伺服器上執行 **Enable-CsTopology** 的權限。

安裝 Lync Server 時會進行的網域準備無法自動新增權限，該權限可讓 RTCUniversalServerAdmins 群組成員執行 Enable-CsTopology Cmdlet。這代表根據預設，您必須是網域系統管理員才能啟用拓撲。您必須執行 Grant-CsSetupPermissions Cmdlet，才能給予 RTCUniversalServerAdmins 群組成員權限以啟用拓樸。此外，您必須針對裝載執行 Lync Server 之電腦的 Active Directory 容器，執行此 Cmdlet。

請記住，這個 Cmdlet 只會將權限授與 RTCUniversalServerAdmins 群組；您無法使用這個 Cmdlet 將權限授與其他安全性群組或個別使用者。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Enable-CsTopology</strong> 是允許 RTCUniversalServerAdmins 群組成員設定及部署 Lync Server 2013 的主要 Cmdlet。</td>
</tr>
</tbody>
</table>


## 若要將執行 Enable-CsTopology 的能力新增至 RTCUniversalServerAdmins 群組

1.  針對代理使用者要執行 **Enable-CsTopology** 的網域，以該網域之 Domain Admins 群組成員身分登入伺服器。

2.  開啟 Lync Server 2013 管理命令介面。系統隨即會自動將 Lync Server 2013 管理命令介面安裝在每部 前端伺服器上，或任何已安裝 Lync Server 2013 系統管理工具的電腦中。如需 Lync Server 2013 管理命令介面的詳細資訊，請參閱作業文件中的 [Lync Server 管理命令介面](lync-server-2013-lync-server-management-shell.md)。

3.  從 Lync Server 2013 管理命令介面執行以下 Cmdlet：
    
        Grant-CsSetupPermission -ComputerOU <DN of the OU> -Domain <Domain FQDN>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果 OU 不在頂層，則您必須提供完整網域名稱。</td>
    </tr>
    </tbody>
    </table>
    
    在以下範例中，OU 為 "Lync Servers" (位於 contoso.com 網域)。
    
        Grant-CsSetupPermission -ComputerOU "OU=Lync Servers" -Domain contoso.com

