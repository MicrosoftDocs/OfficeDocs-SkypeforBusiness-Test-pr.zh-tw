---
title: Lync Server 2013：準備與部署 Lync Server 混合式環境的步驟
TOCTitle: 準備與部署 Lync Server 2013 混合式環境的步驟
ms:assetid: a50d4f7b-63f4-4663-af63-56ca87e4e3e7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205157(v=OCS.15)
ms:contentKeyID: 49291892
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 準備與部署 Lync Server 2013 混合式環境的步驟

 

_**上次修改主題的時間：** 2015-03-09_

下表列出使用 Microsoft Lync Online 和 Microsoft Office 365 為混合部署準備環境所需的步驟。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>已完成？</th>
<th>步驟</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>建立 Office 365 的租用戶帳戶並啟用 Lync Online</p></td>
<td><p>了解 Office 365 與 Lync Online 的相關資訊，請參閱 <a href="http://go.microsoft.com/fwlink/?linkid=254980">Office 365</a>。</p>
<p>若要確認 Office 365 的環境是否已準備就緒，請參閱<a href="http://go.microsoft.com/fwlink/p/?linkid=401408">系統需求</a>。</p>
<p>如需設定 Office 365 的詳細資訊，請參閱 <a href="http://go.microsoft.com/fwlink/?linkid=254982">Office 365 快速入門</a>與 <a href="http://go.microsoft.com/fwlink/?linkid=254979">設定 Office 365</a>。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>新增您的網域並確認所有權</p></td>
<td><p>您的網域有時也稱為「虛名網域」 。您必須將網域新增至 Office 365 租用戶，然後透過 Office 365 依照步驟驗證網域。這是為了確認您是該網域的擁有者。</p>
<p>若要將網域新增至 Office 365 租用戶，請依照 <a href="http://go.microsoft.com/fwlink/?linkid=254983">新增網域至 Office 365</a> 中說明的步驟。</p>
<p>完成本主題中每一節的所有步驟，包含「為您的 Office 365 服務編輯 DNS 記錄」。</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>確認環境整備狀態</p></td>
<td><p>您可以使用 Office 365 設定小幫手協助您部署 Office 365。如需詳細資訊，請參閱<a href="http://go.microsoft.com/fwlink/p/?linkid=254985">使用設定小幫手判斷 Office 365 的整備狀態</a>。</p>
<p>如需使用工具與部署 Office 365 的詳細資訊，請參閱 <a href="http://go.microsoft.com/fwlink/p/?linkid=257337">Office 365 部署指南</a> (英文)。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Active Directory 同步作業的準備</p></td>
<td><p>Active Directory 同步作業會持續將內部部署 Active Directory 與 Office 365 保持同步。這可讓您建立每一個使用者帳戶與群組的同步版本，也可讓全域通訊清單 (GAL) 從本機的 Microsoft Exchange Server 環境到 Microsoft Exchange Online 保持同步。</p>
<div class="alert">

> [!IMPORTANT]  
> 您需要替組織中位於內部部署與線上 Lync 部署的所有 Lync 使用者同步處理 AD 帳戶，即使使用者並未移至 Lync Online 亦然。如果您並未同步處理所有使用者，組織中的內部部署使用者與線上使用者可能無法如預期般正常通訊。


</div>
<p>若要備妥您的環境以進行 Active Directory 同步處理，請遵循<a href="http://go.microsoft.com/fwlink/p/?linkid=254988">目錄同步處理藍圖</a>中的所述步驟操作，包括設定單一登入。</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>建立 Active Directory Federation Services (AD FS) 的憑證</p></td>
<td><p>您需要建立 Office 365 的識別同盟所使用的憑證。如需詳細資訊，請參閱 <a href="http://go.microsoft.com/fwlink/p/?linkid=285376">檢查清單：使用 AD FS 實作和管理單一登入</a>中＜規劃與部署 AD FS 以使用單一登入＞主題中的＜同盟伺服器憑證＞小節。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>指派 AD FS 的憑證</p></td>
<td><p>建立 Office 365 的識別同盟所使用的憑證之後，必須安裝並指派這些憑證。</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>將試驗使用者移至 商務用 Skype Online</p></td>
<td><p>完成步驟以準備及設定 商務用 Skype Online 的環境之後，您可以開始將試驗使用者移至 Lync Online。</p>
<p>請參閱＜ <a href="lync-server-2013-move-users-to-lync-online.md">在 Lync Server 2013 中將使用者移至 Lync Online</a>＞。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>管理混合部署中的使用者</p></td>
<td><p>如需如何在混合部署中管理使用者的詳細資訊，請參閱＜ <a href="lync-server-2013-administering-users-in-a-hybrid-deployment.md">管理 Lync Server 2013 混合部署中的使用者</a>＞。</p></td>
</tr>
</tbody>
</table>

