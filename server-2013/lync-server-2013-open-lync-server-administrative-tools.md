---
title: 開啟 Lync Server 系統管理工具
TOCTitle: 開啟 Lync Server 系統管理工具
ms:assetid: 8c58de94-9e0a-4368-9e14-9afcaa1142d0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg195741(v=OCS.15)
ms:contentKeyID: 49291599
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 開啟 Lync Server 系統管理工具

 

_**上次修改主題的時間：** 2012-06-28_

您可以使用本主題的程序開啟系統管理工具，來部署、設定或疑難排解 Lync Server 2013 拓撲。

  - 部署精靈

  - 拓撲產生器

  - Lync Server 控制台

  - Lync Server 管理命令介面

## 部署精靈

請使用下列程序，在本機啟動部署精靈，以新增或移除 Lync Server 2013 元件檔案。

## 啟動 Lync Server 2013 部署精靈

1.  以 Domain Admins 群組和 RTCUniversalServerAdmins 群組成員的身分，登入安裝了 Lync Server 部署精靈的電腦。

2.  依序按一下 \[開始\]、\[所有程式\] 及 \[Microsoft Lync Server 2013\]，然後按一下 \[Lync Server 部署精靈\]。

## 拓撲產生器

使用下列程序開啟拓撲產生器，以定義您想在 Lync Server 2013 拓撲中部署的伺服器。

## 開啟 Lync Server 2013 拓撲產生器來設計拓撲

1.  以 Domain Admins 群組與 RTCUniversalServerAdmins 群組成員的身分，登入安裝了拓撲產生器的電腦。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您可以使用屬於本機 Users 群組成員的帳戶來定義拓撲，但是若要讀取、發行或啟用拓撲 (在伺服器上安裝 Lync Server 2013 時的必要作業)，則使用的帳戶必須屬於 Domain Admins 群組及 RTCUniversalServerAdmins 群組的成員，而且具有檔案共用的完全控制權限 (即讀取、寫入及修改)，而此檔案共用是用於封存檔案存放區，讓拓撲產生器可以設定必要的判別存取控制清單 (DACL)，或者，使用的帳戶必須具有相等的使用者權限。</td>
    </tr>
    </tbody>
    </table>


2.  啟動拓撲產生器：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 拓撲產生器\]。

## Lync Server 2013 控制台

使用下列其中一個程序開啟 Lync Server 2013 控制台，以管理環境中的伺服器、使用者、用戶端和裝置的設定。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可以使用指派給 CsAdministrator 角色的使用者帳戶，在 Lync Server 2013 控制台中執行任何工作。您可以使用其他角色來登入 Lync Server 2013 控制台，根據您需要執行的工作來執行特定的系統管理工作。例如，您可以使用 CSArchivingAdministrator，管理 Lync Server 2013 控制台中的封存。如需角色的詳細資訊，請參閱規劃文件中的<a href="lync-server-2013-planning-for-role-based-access-control.md">在 Lync Server 2013 中規劃角色型存取控制</a>。如需執行特定工作可以使用之角色的詳細資訊，請參閱該工作的文件。</td>
</tr>
</tbody>
</table>


## 從組織防火牆內部的任何電腦開啟 Lync Server 2013 控制台

1.  從指派給 CsAdministrator 角色或具有要執行工作之適當使用者權限的其他角色的使用者帳戶，登入內部部署中的任何電腦，且螢幕解析度至少為 1024 x 768。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您已經設定管理簡單統一資源定位器 (URL)，則可以從組織防火牆內部任何電腦上執行的網際網路瀏覽器存取 Lync Server 2013 控制台。如需關於設定管理簡單 URL 的詳細資訊，請參閱規劃文件中的<a href="lync-server-2013-planning-for-simple-urls.md">在 Lync Server 2013 中規劃簡單 URL</a>和部署文件中的<a href="lync-server-2013-edit-or-configure-simple-urls.md">在 Lync Server 2013 中編輯或設定簡單 URL</a>。</td>
    </tr>
    </tbody>
    </table>


2.  開啟瀏覽器視窗，然後輸入組織設定的管理 URL。

## 在執行 Lync Server 2013 的電腦上開啟 Lync Server 2013 控制台

1.  從屬於 CsAdministrator 角色或具有要執行工作之適當使用者權限的其他角色之成員的使用者帳戶，登入已安裝 Lync Server 2013 的電腦，或者至少安裝 Lync Server 2013 系統管理工具的電腦。若要進行設定，此電腦的螢幕解析度必須至少為 1024 x 768。

2.  啟動 Lync Server 2013 控制台：依序按一下 \[開始\] 和 \[所有程式\]，並依序指向 \[系統管理工具\] 和 \[Microsoft Lync Server 2013\]，然後按一下 \[Lync Server 2013 控制台\]。

## Lync Server 2013 管理命令介面

使用下列程序開啟 Lync Server 2013 管理命令介面，利用命令列管理環境中的伺服器、使用者、用戶端和裝置。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可以使用指派給 CsAdministrator 角色的使用者帳戶，在 Lync Server 2013 管理命令介面中執行任何工作。您可以使用其他角色來登入，根據您需要執行的工作來執行特定的系統管理工作。例如，您可以使用 CSArchivingAdministrator 執行與封存管理有關的 Cmdlet。如需角色的詳細資訊，請參閱規劃文件中的<a href="lync-server-2013-planning-for-role-based-access-control.md">在 Lync Server 2013 中規劃角色型存取控制</a>。如需可用來執行特定 Cmdlet 之角色的詳細資訊，請參閱 Cmdlet 的文件。<br />
您也可以根據 Cmdlet，使用 RTCUniversalServerAdmins、RTCUniversalUserAdmins 或 RTCUniversalReadOnlyAdmins 群組中的使用者帳戶，執行特定的 Cmdlet。</td>
</tr>
</tbody>
</table>


## 開啟 Lync Server 2013 管理命令介面

  - 如果您開啟 Windows PowerShell 視窗，而非 Lync Server 2013 管理命令介面，則預設無法執行 Lync Server 2013 Cmdlet。若要從 Windows PowerShell 執行 Lync Server 2013 Cmdlet，請在 Windows PowerShell 命令提示字元中輸入下列命令：
    
    `Import-Module Lync`

  - 啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

## 請參閱

#### 工作

[安裝 Lync Server 2013 系統管理工具](lync-server-2013-install-lync-server-administrative-tools.md)  

#### 概念

[Lync Server 2013 系統管理工具](lync-server-2013-lync-server-administrative-tools.md)

