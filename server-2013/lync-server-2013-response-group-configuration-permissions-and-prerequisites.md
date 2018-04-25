---
title: Lync Server 2013：回應群組設定權限和先決條件
TOCTitle: 回應群組設定權限和先決條件
ms:assetid: 4266f16a-b387-452c-a8ca-d771a3c58f0f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204840(v=OCS.15)
ms:contentKeyID: 49290739
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的回應群組設定權限和先決條件

 

_**上次修改主題的時間：** 2015-03-09_

回應群組是 企業語音的一項通話管理功能。本主題說明設定 回應群組之前需要具有的項目，以及執行設定工作所需的系統管理認證和權限。

本節假設您已閱讀與 回應群組相關的規劃文件。如需詳細資訊，請參閱規劃文件中的＜ [在 Lync Server 2013 中規劃通話管理功能](lync-server-2013-planning-for-call-management-features.md)＞。

## 設定工具與系統管理角色

您可以使用下列系統管理工具來設定 回應群組：

  - Lync Server 控制台

  - 回應群組設定工具

  - Lync Server 管理命令介面

若要設定回應群組，您至少必須是下列其中一個系統管理角色的成員：


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Active Directory 安全性群組 (1)</strong></p></td>
<td><p>建立工作流程</p></td>
<td><p>指派管理員</p></td>
<td><p>建立/指派代理人和佇列</p></td>
<td><p>建立/管理假日和營業時間</p></td>
<td><p>啟用/停用工作流程</p></td>
<td><p>設定工作流程 (IVR 或群組搜尋)</p></td>
</tr>
<tr class="even">
<td><p><strong>CsResponseGroupAdministrator</strong></p></td>
<td><p>    √    </p></td>
<td><p>    √    </p></td>
<td><p>    √    </p></td>
<td><p>    √    </p></td>
<td><p>    √    </p></td>
<td><p>    √    </p></td>
</tr>
<tr class="odd">
<td><p><strong>CsResponseGroupManager</strong></p></td>
<td> </td>
<td><p>√(2)</p></td>
<td><p>√(3)</p></td>
<td><p>√(3)</p></td>
<td><p>√(3)</p></td>
<td><p>√(3)</p></td>
</tr>
<tr class="even">
<td><p><strong>CsVoiceAdministrator</strong></p></td>
<td><p>    √    </p></td>
<td><p>    √    </p></td>
<td><p>    √    </p></td>
<td><p>    √    </p></td>
<td><p>    √    </p></td>
<td><p>    √    </p></td>
</tr>
<tr class="odd">
<td><p><strong>CsServerAdministrator</strong></p></td>
<td><p>    √    </p></td>
<td><p>    √    </p></td>
<td><p>    √    </p></td>
<td><p>    √    </p></td>
<td><p>    √    </p></td>
<td><p>    √    </p></td>
</tr>
<tr class="even">
<td><p><strong>CsAdministrator</strong></p></td>
<td><p>    √    </p></td>
<td><p>    √    </p></td>
<td><p>    √    </p></td>
<td><p>    √    </p></td>
<td><p>    √    </p></td>
<td><p>    √    </p></td>
</tr>
<tr class="odd">
<td><p><strong>CsViewOnlyAdministrator</strong></p></td>
<td><p>√(4)</p></td>
<td><p>√(4)</p></td>
<td><p>√(4)</p></td>
<td><p>√(4)</p></td>
<td><p>√(4)</p></td>
<td><p>√(4)</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>(1)</strong> Active Directory 網域服務 使用者物件必須是列出的指定 Active Directory 安全性群組成員。系統管理員或擁有適當權限可新增使用者至安全性群組 (例如系統管理員、帳戶操作員) 的其他委派的 Active Directory 群組成員，必須新增使用者物件至列出的安全性群組，或是能夠讓使用者執行所列功能的群組。 <strong>(2)</strong> 僅適用 CsResponseGroupAdministrator 已指派至 CsResponseGroupManager 的工作流程。 <strong>(3)</strong> 回應群組管理員可指派 CsResponseGroupManager 的其他成員至目前管理員所管理的工作流程。 <strong>(4)</strong> CsViewOnlyAdministrator 僅可執行動詞 &quot;Get&quot; Lync Server 管理命令介面 Cmdlet。</td>
</tr>
</tbody>
</table>


## 回應群組組態先決條件

回應群組須有以下元件：

  - 應用程式服務

  - 回應群組應用程式

  - 語言套件

  - 檔案存放區 (用於保留音訊檔案)

  - Web 服務 (包括 回應群組設定工具及代理人的登入和登出主控台)

當您部署 企業語音時，預設會安裝上述所有元件。

在設定 回應群組之前，您可能需要先執行下列工作：

  - 針對 Lync Server 2013 和 企業語音啟用使用者。

  - 修改組態檔，以符合美國聯邦資訊處理標準 (FIPS)。

  - 修改資料庫定序，以支援佇列名稱和代理人群組名稱中的 Yi、Meng 和 Zang 字元。

## 啟用使用者

設定 回應群組的第一步是建立代理人群組。建立代理人群組之前，必須器用即將成為代理人的使用者使用 Lync Server 2013 的 回應群組和 企業語音功能。允許使用者使用 Lync Server 2013 通常是 Enterprise Edition 伺服器或 Standard Edition 伺服器部署中的步驟。如需允許使用者使用 Lync Server 2013 的詳細資訊，請參閱＜ [停用或重新啟用 Lync Server 的使用者帳戶](lync-server-2013-disable-or-re-enable-user-account-for-lync-server.md)＞。允許使用者使用 企業語音通常是 企業語音部署中的步驟。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中為使用者啟用企業語音](lync-server-2013-enable-users-for-enterprise-voice.md)＞。

## 遵守 FIPS 要求

只有在您的組織需要遵守美國聯邦資訊處理標準 (FIPS) 時，才適用本節內容。

若要遵守 FIPS，您需要修改應用程式層級的 Web.config 檔案，以在安裝 Web 服務後使用不同的密碼編譯演算法。您需要指定 ASP.NET 使用三重資料加密標準 (3DES) 演算法來處理檢視狀態資料。對於 回應群組應用程式，此需求適用於 回應群組設定工具及代理人登入和登出主控台。如需此需求的詳細資訊，請參閱 Microsoft 知識庫文章 911722＜當您存取已啟用 ASP.NET 1.1 升級 ASP.NET 2.0 之後的 ViewState 的 ASP.NET 網頁時，可能會收到錯誤訊息＞，網址為 [http://go.microsoft.com/fwlink/?linkid=196183\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=196183%26clcid=0x404)。

若要修改 Web.config 檔案，請執行下列動作：

1.  在文字編輯器 (如 \[記事本\]) 中，開啟應用程式層級的 Web.config 檔案。

2.  在 Web.config 檔案中，找到 `<system.web>` 區段。

3.  將下列 `<machineKey>` 區段新增至 `<system.web>` 區段：
    
        <machineKey validationKey="AutoGenerate,IsolateApps" decryptionKey="AutoGenerate,IsolateApps" validation="3DES" decryption="3DES"/>

4.  儲存 Web.config 檔案。

5.  在命令提示字元中執行下列命令，以重新啟動 Internet Information Services (IIS) 服務：
    
        iisreset

## 支援 Yi、Meng 和 Zang 字元

只有在您的組織需要支援 Yi、Meng 或 Zang 字元時，才適用本節內容。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如需什麼是 Yi、Meng 及 Zang 字元，以及這些字元對部署如此重要的原因等詳細資訊，請參閱 GB18030 字元集的資訊 <a href="http://go.microsoft.com/fwlink/?linkid=240223%26clcid=0x404" class="uri">http://go.microsoft.com/fwlink/?linkid=240223&amp;clcid=0x404</a>。</td>
</tr>
</tbody>
</table>


若要支援 Yi、Meng 或 Zang 字元，您需要修改 Rgsconfig 資料庫的定序。請變更每個 Rgsconfig 資料庫中下列各資料表內 **\[名稱\]** 資料行的定序：

  - dbo.AgentGroups

  - dbo.BusinessHours

  - dbo.HolidaySets

  - dbo.Queues

  - dbo.Workflows

若是 SQL Server 2008 R2 和 SQL Server 2012，請使用 Latin\_General\_100 (區分腔調字) 定序。如果您使用此定序，則所有物件名稱都不區分大小寫。

您可以使用 Microsoft SQL Server Management Studio 來變更定序。如需使用此工具的詳細資訊，請參閱＜使用 SQL Server Management Studio＞，網址為 [http://go.microsoft.com/fwlink/?linkid=196184\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=196184%26clcid=0x404)。請遵循下列步驟來變更定序：

1.  確定 SQL Server Management Studio 已設成允許需要重建資料表的變更。如需詳細資訊，請參閱＜儲存 (不允許) 對話方塊＞，網址為 [http://go.microsoft.com/fwlink/?linkid=196186\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=196186%26clcid=0x404)。如需設定資料行定序的詳細資訊，請參閱＜如何：設定資料行定序 (Visual Database Tools)＞，網址為 [http://go.microsoft.com/fwlink/?linkid=196185\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=196185%26clcid=0x404)。

2.  使用 Microsoft SQL Server Management Studio 連線至 Rgsconfig 資料庫。

3.  在 Rgsconfig 資料庫中找到想要變更的資料表，並用滑鼠右鍵按一下資料表，然後按一下 **\[設計\]** 。

4.  變更 **\[名稱\]** 資料行的定序，然後儲存資料表。

