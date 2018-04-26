---
title: 疑難排解 Lync Server 2013 控制台
TOCTitle: 疑難排解 Lync Server 2013 控制台
ms:assetid: 54e7ab57-34ce-4a07-bcc9-643379eb4eb7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg195689(v=OCS.15)
ms:contentKeyID: 49290948
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 疑難排解 Lync Server 2013 控制台

 

_**上次修改主題的時間：** 2013-02-21_

本主題提供可幫助您疑難排解 Lync Server 2013 控制台存取問題的資訊和程序。

## 網際網路瀏覽器需求

Lync Server 控制台需要安裝 Microsoft Silverlight 瀏覽器外掛程式 4.0.50524.0 版或最新版本。如果未安裝 Silverlight，或是安裝較舊版本，請遵循訊息中的指示來安裝所需的版本。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lync Server 控制台的其他軟體需求，取決於可安裝 Lync Server 控制台及所有其他 Lync Server 2013 系統管理工具的作業系統。如需詳細資訊，請參閱支援文件中的<a href="lync-server-2013-server-and-tools-operating-system-support.md">Lync Server 2013 中的伺服器及工具作業系統支援</a>＞。</td>
</tr>
</tbody>
</table>


如果您的網際網路瀏覽器基於安全考量而封鎖 Silverlight 的安裝，請將會開啟 Lync Server 控制台的統一資源定位器 (URL) 新增至信任網站清單。在 Internet Explorer 安全性設定中，確定已將 **\[執行 ActiveX 控制項及外掛程式\]** 設為 **\[啟用\]**。如需詳細資訊，請參閱 [http://go.microsoft.com/fwlink/?linkid=214060\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=214060%26clcid=0x404)。此外，請確定已將瀏覽器設定為使用 SSL 3.0。

如果網際網路瀏覽器設定為使用 Proxy 伺服器，請確認瀏覽器針對自動偵測為內部網站的網站，設定為略過 Proxy 伺服器。或者，在 Proxy 伺服器組態設定中，將位址新增至瀏覽器的例外清單。

## 系統管理存取 URL 的 DNS 記錄及憑證需求

如果您已設定簡單 URL 來存取 Lync Server 控制台，請確定您也設定了所需的靜態網域名稱系統 (DNS) 主機 (A) 資源記錄和憑證，以使用該系統管理存取 URL。如果您在任何時候變更基底 URL，請確定變更已反映在適當的 DNS 記錄和憑證中，而且請務必在每個 Director 和前端伺服器上執行 *Enable-CsComputer*。如需詳細資訊，請參閱規劃文件中的下列主題：

  - [在 Lync Server 2013 中規劃簡單 URL](lync-server-2013-planning-for-simple-urls.md)

  - [Lync Server 2013 中簡單 URL 的 DNS 需求](lync-server-2013-dns-requirements-for-simple-urls.md)

  - [Lync Server 2013 中內部伺服器的憑證需求](lync-server-2013-certificate-requirements-for-internal-servers.md)

如需設定系統管理存取 URL 的逐步程序，請參閱部署文件中的＜[在 Lync Server 2013 中編輯或設定簡單 URL](lync-server-2013-edit-or-configure-simple-urls.md)＞。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您的 Web 伺服器上有多個網路介面卡，則必須為每個額外的網路介面卡手動設定 DNS，DNS 解析才能正確運作。</td>
</tr>
</tbody>
</table>


## Internet Information Services (IIS) 需求

Lync Server 控制台是需要 Internet Information Services (IIS) 的 Lync Server 2013 元件之一。請特別確定 HTTP 重新導向和 Windows 驗證功能已啟用，而且 World Wide Web Publishing 服務 (W3SVC) 正在執行。

## World Wide Publishing Service (Windows 服務) 相依性

當 World Wide Web Publishing 服務停止時，您無法存取 Lync Server 控制台。您可以使用 Windows Services Microsoft Management Console (MMC) 來重新啟動服務。

**啟動 World Wide Web Publishing 服務**

1.  登入隨 Internet Information Services (IIS) 安裝 World Wide Web Publishing 服務的電腦。

2.  依序按一下 \[開始\]、\[系統管理工具\] 和 \[服務\]。

3.  用滑鼠右鍵按一下 \[World Wide Web Publishing 服務\]，然後按一下 \[啟動\]。

## 應用程式集區模式

設定 IIS，讓 CsManagementAppPool 應用程式集區使用網路服務帳戶做為其處理序模型身分識別。

## 使用者權限

您必須使用 CsAdministrator 群組成員的網域帳戶，或是具有委派使用者權限的帳戶，來登入 Lync Server 控制台。您不能使用本機電腦帳戶來登入 Lync Server 控制台。如需有關透過角色型存取控制 (RBAC) 來委派系統管理工作的詳細資訊，請參閱規劃文件中的＜[在 Lync Server 2013 中規劃角色型存取控制](lync-server-2013-planning-for-role-based-access-control.md)＞。

如果您使用簡單 URL 來存取 Lync Server 控制台，請確定 Web 伺服器已新增至 RTCUniversalServerAdmins 及 RTCUniversalUserAdmins 群組。

## 請參閱

#### 概念

[Lync Server 2013 系統管理工具](lync-server-2013-lync-server-administrative-tools.md)

