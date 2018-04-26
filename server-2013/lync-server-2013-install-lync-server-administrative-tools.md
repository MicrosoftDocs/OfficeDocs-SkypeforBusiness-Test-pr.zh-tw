---
title: Lync Server 2013：安裝 Lync Server 系統管理工具
TOCTitle: 安裝 Lync Server 系統管理工具
ms:assetid: 842b85e4-2eeb-464f-b1c1-ceb8cc04f8d5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398665(v=OCS.15)
ms:contentKeyID: 49291521
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 安裝 Lync Server 2013 系統管理工具

 

_**上次修改主題的時間：** 2013-02-21_

本主題說明如何安裝您需要用來部署和管理 Lync Server 2013 的系統管理工具。預設系統管理工具是安裝在每一部執行 Lync Server 2013 的伺服器上。另外，您可以在其他電腦上安裝系統管理工具，例如專用的系統管理主控台。強烈建議您在您建立的 Lync Server 2013 部署處於相同網域或樹系的電腦上安裝系統管理工具，因為這樣做可以確保已完成 Active Directory 網域服務 準備步驟，以後可以在這台電腦上使用系統管理工具發行您的拓撲。

安裝或使用 Lync Server 2013 系統管理工具之前，請先仔細閱讀基礎結構、作業系統、軟體以及系統管理員權限需求。如需基礎結構需求的詳細資訊，請參閱＜[Lync Server 2013 中的系統管理工具基礎結構需求](lync-server-2013-administrative-tools-infrastructure-requirements.md)＞。如需安裝 Lync Server 2013 系統管理工具的作業系統和軟體需求的詳細資訊，請參閱＜[Lync Server 2013 中的伺服器及工具作業系統支援](lync-server-2013-server-and-tools-operating-system-support.md)＞、＜[Lync Server 2013 的其他軟體需求](lync-server-2013-additional-software-requirements.md)＞以及＜[Lync Server 2013 中的其他伺服器支援和需求](lync-server-2013-additional-server-support-and-requirements.md)＞。如需關於安裝和使用該工具所需的使用者權限的詳細資訊，請參閱＜[設定和管理 Lync Server 2013 所需的系統管理員權限](lync-server-2013-administrator-rights-and-permissions-required-for-setup-and-administration.md)＞。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您的組織需要將 Internet Information Services (IIS) 和所有 Web 服務安裝在非系統磁碟機的磁碟機中，應在 [安裝] 對話方塊中變更 Lync Server 檔案的安裝位置路徑。如果您將安裝檔案 (包括 OCSCore.msi) 安裝到此路徑，其餘的 Lync Server 2013 檔案也會部署到此磁碟機。</td>
</tr>
</tbody>
</table>


## 安裝 Lync Server 2013 系統管理工具

1.  以本機系統管理員 (最低需求) 的身分登入要安裝系統管理工具的電腦。如果在 Windows Vista 或 Windows 7 作業系統上您以標準使用者身分登入，且使用者帳戶控制 (UAC) 已啟用，則系統會提示您輸入本機系統管理員或網域中同等身分的使用者名稱和密碼。

2.  找到電腦上的安裝媒體，然後按兩下 \\Setup\\amd64\\Setup.exe。

3.  如果系統提示您安裝 Microsoft Visual C++ 2008 可散發套件，請按一下 \[是\] 。

4.  在 \[ Microsoft Lync Server 2013 安裝位置\] 頁面上，按一下 \[確定\] 。如果您需要將檔案安裝至其他位置，請將此路徑變更為其他位置或磁碟機。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您的組織需要將 Internet Information Services (IIS) 和所有 Web 服務安裝在非系統磁碟機的磁碟機中，應在 [安裝] 對話方塊中變更 Lync Server 2013 檔案的安裝位置路徑。如果您將安裝檔案 (包括 OCSCore.msi) 安裝到此路徑，也會將其餘的 Lync Server 2013 檔案部署到此磁碟機。</td>
    </tr>
    </tbody>
    </table>


5.  在 \[使用者授權合約\] 頁面上檢閱授權條款，然後依序按一下 \[我接受\] 和 \[確定\] 。需要完成此步驟才能繼續。

6.  在 \[Microsoft Lync Server 2013 – 部署精靈\] 頁面上，按一下 \[安裝系統管理工具\]。

7.  當安裝順利完成時，按一下 \[結束\] 。

## 請參閱

#### 工作

[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)  

#### 概念

[Lync Server 2013 系統管理工具](lync-server-2013-lync-server-administrative-tools.md)

