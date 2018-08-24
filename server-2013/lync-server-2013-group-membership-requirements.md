---
title: Lync Server 2013：群組成員資格需求
TOCTitle: 群組成員資格需求
ms:assetid: 01876843-8717-4e72-baf5-866ac8cceee6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204623(v=OCS.15)
ms:contentKeyID: 49289897
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 的群組成員資格需求

 

_**上次修改主題的時間：** 2015-03-09_

下表摘要說明人員成功安裝、管理以及疑難排解 Lync Server 2013 時應具備的群組身分。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Lync Server 2013 可執行檔</th>
<th>需要的群組成員資格</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Setup.exe</strong> – 啟動 Lync Server 2013 系統管理工具安裝程序的可執行檔。</p></td>
<td><p>電腦上執行可執行檔的 Local Administrators 群組成員。讀取 Active Directory 網域服務 中資訊的 Domain Users 群組成員。此層級權限是必要權限，因為在本機電腦上自動安裝必要的 MSI 套件時，需要允許在受保護的本機電腦資源 (例如 Program Files 目錄) 以及受保護登錄 (例如 Local Machine Hive) 上讀取和寫入的權限。</p>
<div>

> [!TIP]  
> 您也可以委派安裝權限給您不想授予 Domain Admins 群組成員資格的使用者或群組。如需詳細資訊，請參閱部署文件中的＜ <a href="lync-server-2013-granting-setup-permissions.md">在 Lync Server 2013 中授與設定權限</a>＞。

</div></td>
</tr>
<tr class="even">
<td><p><strong>Deploy.exe</strong> – 由 setup.exe 呼叫，deploy.exe 負責部署伺服器角色的軟體元件。</p></td>
<td><p>電腦上執行可執行檔的 Local Administrators 群組成員。讀取 AD DS 中資訊的 Domain Users 群組成員。此層級權限是必要權限，因為在本機電腦上自動安裝必要的 MSI 套件時，需要允許在受保護的本機電腦資源 (例如 Program Files 目錄) 以及受保護登錄 (例如 Local Machine Hive) 上讀取和寫入的權限。必須有讀取 中央管理存放區的 RtcUniversalReadOnlyAdmins 群組成員資格。</p>
<div>

> [!NOTE]  
> 如果您是執行 Windows Vista 作業系統 或 Windows 7 作業系統，使用者帳戶控制 (UAC) 會提示您繼續安裝。如果您是用標準使用者帳戶登入，則在出現具有安裝軟體權限的帳戶提示時，您會需要身為 Local Administrators 群組成員的某個人提供憑證。


</div></td>
</tr>
<tr class="odd">
<td><p><strong>Bootstrapper.exe</strong> – 由 setup.exe 呼叫，bootstrapper.exe 負責部署和設定伺服器角色。</p></td>
<td><p>電腦上執行可執行檔的 Local Administrators 群組成員。執行 Bootstrapper.exe 的 RTCUniversalServerAdmins 群組成員。讀取 AD DS 中資訊的 Domain Users 群組成員。此層級權限是必要權限，因為在本機電腦上自動安裝必要的 MSI 套件時，需要允許在受保護的本機電腦資源 (例如 Program Files 目錄) 以及受保護登錄 (例如 Local Machine Hive) 上讀取和寫入的權限。</p></td>
</tr>
<tr class="even">
<td><p><strong>TopologyBuilder</strong> – 精靈驅動的使用者介面，用來建立、檢視、調整以及驗證 Lync Server 2013 拓撲。</p></td>
<td><p>電腦上執行可執行檔以檢視拓撲的 Local Administrators 群組成員。變更組態設定的 RTCUniversalServerAdmins 群組成員。發行拓撲的 RTCUniversalServerAdmins 群組和 Domain Admins 群組成員，或 RTCUniversalServerAdmins 群組成員 (僅限於群組被授予委派安裝權限時)。如需委派安裝權限以允許 RTCUniversalServerAdmins 群組成員發行拓撲 (不需是 Domain Admins 群組成員) 的詳細資訊，請參閱部署文件中的＜ <a href="lync-server-2013-granting-setup-permissions.md">在 Lync Server 2013 中授與設定權限</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>AdminUIHost</strong> – 管理 Lync Server 2013 的 Web 型圖形使用者介面。</p></td>
<td><p>CsAdministrator 群組成員，或指派了特定系統管理工作的其他角色型存取控制 (RBAC) 角色成員。 Lync Server 2013 控制台透過執行 Lync Server 2013 管理命令介面 Cmdlet 的方式實作設定變更。如需預先定義角色以及允許成員執行之 Cmdlet 的清單，請參閱規劃文件中的＜ <a href="lync-server-2013-planning-for-role-based-access-control.md">在 Lync Server 2013 中規劃角色型存取控制</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>已載入 Lync Server 2013 模組的 PowerShell.exe</strong> – 包含管理 Lync Server 2013 專用之 Cmdlet 的命令列系統管理工具。</p></td>
<td><p>CsAdministrator 群組成員，或指派特定 Cmdlet 的其他 RBAC 角色成員。如需預先定義角色以及允許成員執行之 Cmdlet 的清單，請參閱規劃文件中的＜ <a href="lync-server-2013-planning-for-role-based-access-control.md">在 Lync Server 2013 中規劃角色型存取控制</a>＞。</p>
<p>或者，下列一或多個群組成員 (視 Cmdlet 而定)：</p>
<ul>
<li><p>RTCUniversalServerAdmins</p></li>
<li><p>RTCUniversalUserAdmins</p></li>
<li><p>RTCUniversalReadOnlyAdmins</p></li>
</ul></td>
</tr>
</tbody>
</table>

