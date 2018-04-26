---
title: Lync Server 2013：Enterprise Voice 的安全性和組態先決條件
TOCTitle: Enterprise Voice 的安全性和組態先決條件
ms:assetid: 15354abe-733e-466b-bcd4-a6cfbf58caf8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398221(v=OCS.15)
ms:contentKeyID: 49290189
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中 Enterprise Voice 的安全性和組態先決條件

 

_**上次修改主題的時間：** 2012-10-18_

請確認您的基礎結構符合下列安全性、使用者設定和特定案例的硬體先決條件。

## 系統管理權限和憑證基礎結構

請確認在 Enterprise Voice 部署過程中，您的環境是設定為下列系統管理使用者群組以及憑證基礎結構。

  - 部署 Enterprise Voice 的系統管理員應該是 RTCUniversalServerAdmins 群組的成員。

  - 執行設定工作的系統管理員必須具備適當的權限：
    
      - **CsVoiceAdministrator：**此系統管理員角色可以執行語音設定工作、管理語音應用程式，以及指派語音原則給一般使用者。
    
      - **CsUserAdministrator：**此系統管理員角色可以管理使用者屬性，例如啟用使用者的 Enterprise Voice。此系統管理員角色也可以指派個別使用者原則，封存原則除外；移動使用者；管理公用區電話和類比裝置。
    
      - **CsAdministrator：**此系統管理員角色可以執行 CsVoiceAdministrator 和 CsUserAdministrator 的所有工作。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>委派可讓更多系統管理員參與您的 Lync Server 部署，而不需要開啟不必要的資源存取權。</td>
    </tr>
    </tbody>
    </table>


  - 已經使用 Microsoft 或協力廠商憑證授權單位 (CA) 的基礎結構，完成 Managed 金鑰基礎結構 (MKI) 的部署和設定。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如需 Lync Server 憑證需求的詳細資訊，請參閱規劃文件中的＜ <a href="lync-server-2013-certificate-infrastructure-requirements.md">Lync Server 2013 的憑證基礎結構需求</a>＞。</td>
    </tr>
    </tbody>
    </table>


## 使用者設定

如果您在部署前端時，將中繼伺服器和每個前端集區或 Standard Edition 伺服器 組合在一起，則在安裝這些伺服器角色的檔案時，會自動設定 Enterprise Voice 的必要使用者設定。

如果您此時是全新部署 Enterprise Voice 工作量，在開始部署程序前，請先為每個您計畫要啟用 Enterprise Voice 的使用者指定主要電話號碼。身為系統管理員，您要負責確認這個號碼是唯一的。在實作前，必須使用 Lync Server 控制台正規化 (正確格式化) 全部的主要電話號碼，並複製至每個使用者的 **線路 URI** 屬性。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如需 Enterprise Voice 部署所需之主要電話號碼的範例，請參閱規劃文件中＜ <a href="lync-server-2013-dial-plans-and-normalization-rules.md">Lync Server 2013 中的撥號對應表和正規化規則</a>＞的＜ <a href="lync-server-2013-dial-plans-and-normalization-rules.md">Lync Server 2013 中的撥號對應表和正規化規則</a>＞一節。</td>
</tr>
</tbody>
</table>


## 後續步驟：安裝檔案或設定 PSTN 連線

確定 Enterprise Voice 的軟體和環境先決條件後，可以遵循下列內容進行：

  - 依照＜[在 Lync Server 2013 中安裝中繼伺服器的檔案](lync-server-2013-install-the-files-for-mediation-server.md)＞的說明安裝中繼伺服器，但僅限於您在組合時，將中繼伺服器安裝為前端集區或 Standard Edition 伺服器 部署程序中的一部分，並因而想要部署獨立中繼伺服器或集區。

  - 或者，開始進行設定以路由傳送 Enterprise Voice 使用者的電話，如 ＜ [在 Lync Server 2013 中設定主幹](lync-server-2013-configuring-trunks.md)＞所述。

