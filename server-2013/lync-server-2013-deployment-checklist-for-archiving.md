---
title: Lync Server 2013：封存的部署檢查單
TOCTitle: 封存的部署檢查單
ms:assetid: 7479734d-be01-40d9-ad82-320a09d19d04
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205009(v=OCS.15)
ms:contentKeyID: 49291335
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中封存的部署檢查單

 

_**上次修改主題的時間：** 2015-03-09_

封存會自動安裝於 Lync Server 2013 部署的每個前端伺服器上，但您仍需先進行設定才能使用。請依本節摘要之設定所需的步驟部署封存。

## 部署順序

如何根據所選擇的存放區選項設定封存：

  - 如果您在部署中針對所有使用者使用 Microsoft Exchange 整合，便不需要為使用者設定 Lync Server 2013 封存原則；反之，請將 Exchange 就地保留原則設定為支援 Exchange 2013 所主控的使用者封存 (連帶將信箱設定為就地保留狀態)。如需有關設定這些原則的詳細資訊，請參閱 Exchange 2013 產品文件。

  - 如果您不在部署中針對所有使用者使用 Microsoft Exchange 整合，則必須將 Lync Server 封存資料庫 ( SQL Server 資料庫) 新增至拓撲，然後予以發行，並為使用者設定原則及設定值，才能封存這些使用者的資料。您可在部署初始拓撲的同時，或者在部署至少一個前端集區或 Standard Edition Server 之後，進行部署封存資料庫。本文件描述如何透過將封存資料庫新增至現有部署來進行部署。

如果您在一個前端集區或 Standard Edition Server 啟用封存，則應在部署中針對所有其他前端集區和 Standard Edition Server 一併啟用。這是因為，需要將通訊封存的使用者可受邀至由其他集區所主控的群組 IM 交談或會議。如果封存未在主控交談或會議的所在集區啟用，可能無法封存完整的工作階段。在此情況下，包含已啟用封存之使用者的 IM 仍可進行封存，但不包含會議內容檔案以及會議加入或離開事件。

> [!IMPORTANT]  
> 如果組織基於規範理由而極重視封存作業，請務必在啟用這些 Lync Server 2013 的使用者之前部署封存、設定原則與其他適當等級的選項，以及針對所有適當的使用者啟用封存。



## 封存部署程序

下表提供在現有拓撲中部署封存之所需步驟的概觀。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>階段</th>
<th>步驟</th>
<th>角色和群組成員資格</th>
<th>文件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>安裝先決條件硬體與軟體</strong></p></td>
<td><ul>
<li><p>若要使用 Microsoft Exchange 整合 (針對部分或所有使用者使用 Exchange 2013 封存存放區)，您需要現有 Exchange 2013 部署。</p></li>
<li><p>若針對部分或所有使用者使用個別封存資料庫 (使用 SQL Server 資料庫) 封存存放區，伺服器上的 SQL Server 將會儲存封存資料。</p></li>
</ul>
<div>

> [!NOTE]  
> 封存會在 Enterprise Pool 前端伺服器與 Standard Edition Server 上執行。安裝這些伺服器除必條件外，沒有額外的硬體或軟體需求。


</div></td>
<td><p>身為本機系統管理員群組成員的網域使用者。</p></td>
<td><p>支援文件中的 <a href="lync-server-2013-supported-hardware.md">Lync Server 2013 的受支援硬體</a>。</p>
<p>支援文件中的 <a href="lync-server-2013-server-software-and-infrastructure-support.md">Lync Server 2013 中的伺服器軟體和基礎結構支援</a>。</p>
<p>規劃文件中的 <a href="lync-server-2013-technical-requirements-for-archiving.md">Lync Server 2013 中封存的技術需求</a>。</p>
<p>部署文件中的 <a href="lync-server-2013-setting-up-systems-and-infrastructure-for-archiving.md">在 Lync Server 2013 中設定系統與基礎結構以進行封存</a>。</p>
<p>支援文件中的 <a href="lync-server-2013-exchange-and-sharepoint-integration-support.md">Lync Server 2013 中的 Exchange Server 與 SharePoint 整合支援</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>建立適當的內部拓撲以支援封存 (僅適用於未在部署中針對所有使用者使用 Microsoft Exchange 整合)</strong></p></td>
<td><p>執行 拓撲產生器以將 Lync Server 2013 封存資料庫 ( SQL Server 資料庫) 新增至拓撲，然後發行該拓撲。</p></td>
<td><p>若要將拓撲定義以納入封存資料庫，帳戶須為本機使用者群組成員。</p>
<p>若要發行拓撲，帳戶須為 Domain Admins 群組及 RTCUniversalServerAdmins 群組成員，其具有檔案共用的完整控制權限 (讀取/寫入/修改)，此檔案共用是用於 Lync Server 2013 檔案存放區，以便拓撲產生器設定必要的 DACL。</p></td>
<td><p>部署文件中的 <a href="lync-server-2013-adding-archiving-databases-to-an-existing-lync-server-2013-deployment.md">將封存資料庫新增至現有的 Lync Server 2013 部署</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>設定伺服器對伺服器驗證 (僅適用於使用 Microsoft Exchange 整合)</strong></p></td>
<td><p>將伺服器設定為啟用 Lync Server 2013 與 Exchange 2013 之間的驗證。建議您執行 <strong>Test-CsExchangeStorageConnectivity testuser_sipUri –Folder Dumpster</strong>，在啟用封存之前驗證 Exchange 封存存放區連線能力。</p></td>
<td><p>具有適當權限可在伺服器上管理憑證的帳戶。</p></td>
<td><p>部署文件或作業文件中的 <a href="lync-server-2013-managing-server-to-server-authentication-oauth-and-partner-applications.md">在 Lync Server 2013 中管理伺服器對伺服器驗證 (Oauth) 與夥伴應用程式</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>設定封存原則及組態</strong></p></td>
<td><p>設定封存，包括使用 Microsoft Exchange 整合、全域原則及任何網站與使用者原則 (在不針對所有資料存放區使用 Microsoft Exchange 整合時)，以及指定封存選項，例如關鍵模式、資料匯出和清除。</p>
<p>如果使用 Microsoft Exchange 整合，請視需要將 Exchange 設定為就地保留原則。</p></td>
<td><p>RTCUniversalServerAdmins 群組 (僅限 Windows PowerShell) 或將使用者指派為 CSArchivingAdministrator 或 CSAdministrator 角色。</p></td>
<td><p>部署文件中的 <a href="lync-server-2013-configuring-support-for-archiving.md">在 Lync Server 2013 中設定封存支援</a>。</p>
<p>Exchange 產品文件 (若使用 Microsoft Exchange 整合)。</p></td>
</tr>
</tbody>
</table>


## 在不同的樹系中部署 Lync Server 和 Microsoft Exchange

如果 Microsoft Exchange Server 未與 Lync Server 部署在同一個樹系中，您必須確保下列 Exchange Active Directory 屬性已同步處理至部署 Lync Server 的樹系：

1.  msExchUserHoldPolicies

2.  proxyAddresses

此為多重值屬性。在同步處理此屬性之時，您必須將數值合併，不要予以取代，以便確保現有數值不會遺失。

