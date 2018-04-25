---
title: Lync Server 2013：準備 Active Directory 結構描述
TOCTitle: 準備 Active Directory 結構描述
ms:assetid: 067726ae-fd3f-4133-a32f-26d2603ac674
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398119(v=OCS.15)
ms:contentKeyID: 49289971
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中準備 Active Directory 結構描述

 

_**上次修改主題的時間：** 2012-08-27_

在您開始準備 Active Directory 網域服務 之前，您可以使用文字編輯器 (如 Windows 記事本) 開啟架構檔案，或參閱＜ [Lync Server 2013 使用的 Active Directory 結構描述擴充功能、類別及屬性](lync-server-2013-active-directory-schema-extensions-classes-and-attributes-used-by-lync-server.md)＞檢閱將針對 Lync Server 2013 修改的所有 Active Directory 網域服務 架構延伸。 Lync Server 使用下列四種架構檔案：

  - ExternalSchema.ldf，這個檔案用於提供與 Microsoft Exchange Server 的互通性

  - ServerSchema.ldf，這是主要的 Lync Server 2013 架構檔案

  - BackCompatSchema.ldf，這個檔案用於提供與任何舊版元件的互通性

  - VersionSchema.ldf，這個檔案用於提供預備架構的版本資訊

不論您是從舊版進行移轉或執行全新安裝，所有 .ldf 檔案都是在架構準備期間進行安裝。這些架構檔案會依上述清單顯示的順序進行安裝，並位於安裝媒體的 \\Support\\schema 資料夾中。

Lync Server 架構延伸模組會在整個網域中進行複寫，因此會影響網路流量。請在網路使用率較低時執行架構準備作業。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您需要將 MicrosoftR Office Communicator Mobile 2007 R2 for Java 與適用於 Nokia 1.0 行動用戶端的 MicrosoftR Office Communicator Mobile 的支援新增至 Lync Server 2013 部署，則需要在 Lync Server 2013 的安裝期間為 Microsoft Office Communications Server 2007 R2 準備 Active Directory 架構。如需必要軟體和文件，請參閱 <a href="http://go.microsoft.com/fwlink/?linkid=207172%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=207172&amp;clcid=0x404</a>。</td>
</tr>
</tbody>
</table>


## ADSI 編輯器

Active Directory 服務介面編輯器 (ADSI 編輯器) 是您可以用於驗證架構準備和複寫的 AD DS 系統管理工具。

當您安裝 AD DS 角色以使伺服器成為網域控制站時，預設會安裝 ADSI 編輯器。如果是 Windows Server 2008 和 Windows Server 2008 R2，ADSI 編輯器 (adsiedit.msc) 會包含在遠端伺服器管理工具 (RSAT) 中。您也可以在網域成員伺服器或獨立伺服器上安裝 RSAT。RSAT 套件預設會在您安裝 Windows 時複製到這些伺服器，但並不會進行安裝。您可以使用伺服器管理員來安裝個別的工具。「ADSI 編輯器」包含在 **\[角色管理工具\]** 、 **\[Active Directory 網域服務工具\]** 、 **\[Active Directory 網域控制站工具\]** 之下。

如果是 Windows Server 2003，ADSI 編輯器包含在支援工具中。您可以從 Windows Server 2003 光碟的 \\SUPPORT\\TOOLS 資料夾中取得支援工具，或者從＜Windows Server 2003 Service Pack 2 32 位元支援工具＞(網址為 [http://go.microsoft.com/fwlink/?linkid=125770\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=125770%26clcid=0x404)) 下載。您可以從＜安裝 Windows 支援工具＞(網址為 [http://go.microsoft.com/fwlink/?linkid=125771\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=125771%26clcid=0x404)) 取得從產品光碟安裝支援工具的相關指示。當您安裝支援工具時，就會自動登錄 Adsiedit.dll。不過，若您將檔案複製到電腦，則必須先執行 **regsvr32** 命令來登錄 adsiedit.dll 檔案，才能執行該工具。

## 本節內容

  - [在 Lync Server 2013 中執行 Active Directory 架構準備](lync-server-2013-running-schema-preparation.md)

  - [在 Lync Server 2013 中驗證 Active Directory 結構描述複寫](lync-server-2013-verifying-schema-replication.md)

## 請參閱

#### 其他資源

[為 Lync Server 2013 準備樹系](lync-server-2013-preparing-the-forest.md)  
[針對 Lync Server 2013 準備網域](lync-server-2013-preparing-domains.md)

