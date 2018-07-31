---
title: Lync Server 2013 電話撥入式會議的部署檢查清單
TOCTitle: 電話撥入式會議的部署檢查清單
ms:assetid: 9c8d3ebe-0d70-4a61-9bd0-522286cddd9a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412726(v=OCS.15)
ms:contentKeyID: 49291805
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的電話撥入式會議的部署檢查清單

 

_**上次修改主題的時間：** 2015-03-09_

當您部署會議工作負載時，會連電話撥入式會議所需的元件一起部署。在設定電話撥入式會議之前，您需要先部署 企業語音或 中繼伺服器和公用交換電話網路 (PSTN) 閘道。

必須執行下表中的所有步驟，使用者才能從 PSTN 撥入來加入音訊/視訊會議。

> [!NOTE]  
> 如果您是從 Office Communications Server 2007 R2 進行移轉，必須至少將最新更新套用至 Office Communications Server 2007 R2 環境，然後才部署電話撥入式會議。



### 電話撥入式會議部署程序

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
<th>權限</th>
<th>部署文件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>建立包含會議工作負載 (包括 中繼伺服器和 PSTN 閘道) 的拓撲，並部署 前端集區或 Standard Edition 伺服器</strong></p></td>
<td><ol>
<li><p>執行 拓撲產生器來設定拓撲。設定拓撲時，選取電話撥入式會議選項。</p></li>
<li><p>發行拓撲並部署 前端集區或 Standard Edition 伺服器。</p></li>
<li><p>必要的話，建立獨立的 中繼伺服器，並將它與 PSTN 閘道建立關聯。</p>
<div class="alert">

> [!NOTE]  
> 只有當您不部署 企業語音，也不將 中繼伺服器 與 Enterprise Edition前端伺服器 或 Standard Edition 伺服器 放置在一起時，才需要此步驟。如果您部署 企業語音，即會在 企業語音 部署過程中安裝及設定 中繼伺服器 和 PSTN 閘道。如果您將 中繼伺服器 放在一起，則會在 前端集區 或 Standard Edition 伺服器 的部署過程中安裝及設定 中繼伺服器。


</div></li>
</ol></td>
<td><p>Domain Admins</p>
<p>RTCUniversalServerAdmins</p>
<p>系統管理員</p></td>
<td><ul>
<li><p><a href="lync-server-2013-deploying-lync-server.md">部署 Lync Server 2013</a></p></li>
<li><p>若要建立獨立 中繼伺服器集區： <a href="lync-server-2013-deploying-mediation-servers-and-defining-peers.md">在 Lync Server 2013 中部署中繼伺服器並定義對等項目</a></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>設定撥號對應表</strong></p></td>
<td><p>撥號對應表是一組電話號碼正規化規則，可將特定位置撥打的電話號碼轉譯成單一標準 (E.164) 格式，以便進行電話授權和電話路由。若從不同位置撥打相同電話號碼，則根據個別的撥號對應表，會解析成適用於每個位置的不同 E.164 號碼。如果您部署企業語音，您會在該部署中設定撥號對應表，且您需要確定撥號對應表也支援電話撥入式會議。如果您不部署企業語音，則需要為電話撥入式會議設定撥號對應表。</p>
<p>使用 Lync Server 2013 控制台或 Lync Server 管理命令介面來設定撥號對應表，如下所示：</p>
<ol>
<li><p>建立一個或多個撥號對應表，以便路由傳送撥入存取電話號碼。</p></li>
<li><p>將預設撥號對應表指派至每個集區。將 <strong>[電話撥入式會議區域]</strong> 設定為撥號對應表適用的地理位置。此區域會將撥號對應表與撥入存取號碼建立關聯。</p></li>
</ol></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsVoiceAdministrator</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-configure-dial-plans-for-dial-in-conferencing.md">在 Lync Server 2013 中設定電話撥入式會議的撥號對應表</a></p></td>
</tr>
<tr class="odd">
<td><p><strong>確定撥號對應表已有指派區域</strong></p></td>
<td><p>執行 <strong>Get-CsDialPlan</strong> 和 <strong>Set-CsDialPlan</strong> Cmdlet，確定所有撥號對應表都已有指派區域。</p></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsVoiceAdministrator</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-make-sure-dial-plans-have-assigned-regions.md">確定撥號對應表 Lync Server 2013 具有指派的區域</a></p></td>
</tr>
<tr class="even">
<td><p><strong>(選用) 確認或修改使用者個人識別碼 (PIN) 需求。</strong></p></td>
<td><p>使用 Lync Server 2013 控制台或 Lync Server 管理命令介面來檢視或修改會議的 [PIN 原則] 。您可以指定最小 PIN 長度、嘗試登入次數上限、PIN 到期及是否允許共同模式。</p></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-optional-verify-pin-policy-settings.md">(選用) 在 Lync Server 2013 中驗證 PIN 原則設定</a></p></td>
</tr>
<tr class="odd">
<td><p><strong>設定會議原則來支援電話撥入式會議。</strong></p></td>
<td><p>使用 Lync Server 2013 控制台或 Lync Server 管理命令介面來設定 <strong>[會議原則]</strong> 設定。指定是否：</p>
<ul>
<li><p>已啟用 PSTN 會議撥入。</p></li>
<li><p>讓使用者可以邀請匿名參與者。</p></li>
<li><p>讓未經驗證的使用者可以使用撥出電話來加入會議。撥出電話時，會議伺服器會撥打給使用者，而使用者會接聽電話來加入會議。</p></li>
</ul></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-configure-conferencing-policy-for-dial-in.md">在 Lync Server 2013 中設定電話撥入式會議的會議原則</a></p></td>
</tr>
<tr class="even">
<td><p><strong>設定撥入存取號碼</strong></p></td>
<td><p>使用 Lync Server 2013 控制台或 Lync Server 管理命令介面來設定由使用者撥打以加入會議的撥入存取號碼，並指定用來將存取號碼與適當撥號對應表建立關聯的區域。會議邀請中包含召集人的撥號對應表所指定之區域的前三個存取號碼。 電話撥入式會議設定頁面上會提供所有存取號碼。</p>
<div class="alert">

> [!NOTE]  
> 在建立撥入存取號碼之後，您可以使用 <strong>Set-CsDialInConferencingAccessNumber</strong> Cmdlet 來修改 Active Directory 連絡人物件的顯示名稱，讓使用者可以更輕鬆識別正確的存取號碼。


</div></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-configure-dial-in-conferencing-access-numbers.md">在 Lync Server 2013 中設定電話撥入式會議存取號碼</a></p></td>
</tr>
<tr class="odd">
<td><p><strong>(選用) 驗證電話撥入式會議設定</strong></p></td>
<td><p>使用 <strong>Get-CsDialinConferencingAccessNumber</strong> Cmdlet，來搜尋其電話撥入式會議區域未由任何存取號碼使用的撥號對應表，以及未指派區域的存取號碼。</p></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p>
<p>CsViewOnlyAdministrator</p>
<p>CsHelpDesk</p></td>
<td><p><a href="lync-server-2013-optional-verify-dial-in-conferencing-settings.md">(選用) 在 Lync Server 2013 中驗證電話撥入式會議設定</a></p></td>
</tr>
<tr class="even">
<td><p><strong>(選用) 修改 DTMF 命令的按鍵對應</strong></p></td>
<td><p>使用 <strong>Set-CsDialinConferencingDtmfConfiguration</strong> Cmdlet，來修改複頻式訊號 (DTMF) 命令使用的按鍵，供參與者用來控制會議設定 (例如靜音和取消靜音，或鎖定和解除鎖定)。</p></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-optional-modify-key-mapping-for-dtmf-commands.md">(選用) 在 Lync Server 2013 中修改 DTMF 命令的按鍵對應</a></p></td>
</tr>
<tr class="odd">
<td><p><strong>(選用) 修改會議加入和離開宣告行為</strong></p></td>
<td><p>使用 <strong>Set-CsDialinConferencingConfiguration</strong> 來變更參與者加入和離開會議時的宣告運作方式。</p></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-optional-enable-and-disable-conference-join-and-leave-announcements.md">(選用) 在 Lync Server 2013 中啟用和停用會議加入和離開宣告</a></p></td>
</tr>
<tr class="even">
<td><p><strong>(選用) 驗證電話撥入式會議</strong></p></td>
<td><p>使用 <strong>Test-CsDialInConferencing</strong> Cmdlet 來測試指定的集區適用的存取號碼是否正常運作。</p></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-optional-verify-dial-in-conferencing.md">Lync Server 2013 中的 (選用) 驗證電話撥入式會議</a></p></td>
</tr>
<tr class="odd">
<td><p><strong>部署 Lync 2013 的線上會議增益集</strong></p></td>
<td><p>部署 Lync 2013 的線上會議增益集，讓使用者可以排程支援電話撥入式會議的會議。當您安裝 Lync 2013 時，會自動安裝 Lync 2013 的線上會議增益集。</p></td>
<td><p>系統管理員</p></td>
<td><p><a href="lync-server-2013-deploy-the-online-meeting-add-in-for-lync-2013.md">部署 Lync 2013 的線上會議增益集</a></p></td>
</tr>
<tr class="even">
<td><p><strong>設定使用者帳戶設定</strong></p></td>
<td><p>使用 Lync Server 2013 控制台或 Lync Server 管理命令介面，來將電話語音的 [線路 URI] 設為唯一、正規化的電話號碼 (例如，tel:+14255550200)。</p></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsAdministrator</p>
<p>CsUserAdministrator</p></td>
<td><p><a href="lync-server-2013-configure-user-account-settings.md">在 Lync Server 2013 中設定使用者帳戶設定</a></p></td>
</tr>
<tr class="odd">
<td><p>(建議) 設定會議目錄</p></td>
<td><p>使用 <strong>New-CsConferenceDirectory</strong> Cmdlet 為集區中每 999 名使用者建立一個會議目錄。</p></td>
<td><p>RTCUniversalServerAdmins</p></td>
<td><p><a href="lync-server-2013-dial-in-conferencing-requirements.md">Lync Server 2013 中的電話撥入式會議需求</a> <a href="recommended-create-conference-directories.md">(建議) 建立會議目錄</a></p></td>
</tr>
<tr class="even">
<td><p><strong>(選用) 歡迎使用者加入電話撥入式會議並設定初始 PIN</strong></p></td>
<td><p>使用 <strong>Set-CsPinSendCAWelcomeMail</strong> 指令碼來設定使用者的初始 PIN，並傳送歡迎電子郵件 (內含初始 PIN 和 電話撥入式會議設定頁面的連結)。</p></td>
<td><p>RTCUniversalServerAdmins</p></td>
<td><p><a href="lync-server-2013-optional-welcome-users-to-dial-in-conferencing.md">(選用) 在 Lync Server 2013 中歡迎使用者使用電話撥入式會議</a></p></td>
</tr>
</tbody>
</table>

