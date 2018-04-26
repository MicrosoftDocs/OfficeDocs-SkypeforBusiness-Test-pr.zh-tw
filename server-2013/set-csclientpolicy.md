---
title: Set-CsClientPolicy
TOCTitle: Set-CsClientPolicy
ms:assetid: 4b7eac0c-50e9-443a-b474-5c4e0c286028
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398300(v=OCS.15)
ms:contentKeyID: 49290842
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsClientPolicy

 

_**上次修改主題的時間：** 2015-05-01_

修改現有用戶端原則的屬性值。用戶端原則可用於指定使用者所能使用的 Lync Server 功能。例如，您可能會在授權某些使用者可以傳輸檔案的同時，也拒絕讓某些使用者執行此作業。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsClientPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsClientPolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AddressBookAvailability <WebSearchAndFileDownload | WebSearchOnly | FileDownloadOnly>] [-AttendantSafeTransfer <$true | $false>] [-AutoDiscoveryRetryInterval <TimeSpan>] [-BlockConversationFromFederatedContacts <$true | $false>] [-CalendarStatePublicationInterval <UInt32>] [-ConferenceIMIdleTimeout <TimeSpan>] [-Confirm [<SwitchParameter>]] [-CustomizedHelpUrl <String>] [-CustomLinkInErrorMessages <String>] [-CustomStateUrl <String>] [-Description <String>] [-DGRefreshInterval <TimeSpan>] [-DisableCalendarPresence <$true | $false>] [-DisableContactCardOrganizationTab <$true | $false>] [-DisableEmailComparisonCheck <$true | $false>] [-DisableEmoticons <$true | $false>] [-DisableFederatedPromptDisplayName <$true | $false>] [-DisableFeedsTab <$true | $false>] [-DisableFreeBusyInfo <$true | $false>] [-DisableHandsetOnLockedMachine <$true | $false>] [-DisableHtmlIm <$true | $false>] [-DisableInkIM <$true | $false>] [-DisableMeetingSubjectAndLocation <$true | $false>] [-DisableOneNote12Integration <$true | $false>] [-DisableOnlineContextualSearch <$true | $false>] [-DisablePhonePresence <$true | $false>] [-DisablePICPromptDisplayName <$true | $false>] [-DisablePoorDeviceWarnings <$true | $false>] [-DisablePoorNetworkWarnings <$true | $false>] [-DisablePresenceNote <$true | $false>] [-DisableRTFIM <$true | $false>] [-DisableSavingIM <$true | $false>] [-DisplayPhoto <NoPhoto | PhotosFromADOnly | AllPhotos>] [-EnableAppearOffline <$true | $false>] [-EnableCallLogAutoArchiving <$true | $false>] [-EnableClientMusicOnHold <$true | $false>] [-EnableConversationWindowTabs <$true | $false>] [-EnableEnterpriseCustomizedHelp <$true | $false>] [-EnableEventLogging <$true | $false>] [-EnableExchangeContactSync <$true | $false>] [-EnableExchangeDelegateSync <$true | $false>] [-EnableFullScreenVideo <$true | $false>] [-EnableHighPerformanceConferencingAppSharing <$true | $false>] [-EnableHighPerformanceP2PAppSharing <$true | $false>] [-EnableHotdesking <$true | $false>] [-EnableIMAutoArchiving <$true | $false>] [-EnableMediaRedirection <$true | $false>] [-EnableNotificationForNewSubscribers <$true | $false>] [-EnableSQMData <$true | $false>] [-EnableTracing <$true | $false>] [-EnableUnencryptedFileTransfer <$true | $false>] [-EnableURL <$true | $false>] [-EnableVOIPCallDefault <$true | $false>] [-ExcludedContactFolders <String>] [-Force <SwitchParameter>] [-HelpEnvironment <String>] [-HotdeskingTimeout <TimeSpan>] [-IMWarning <String>] [-MAPIPollInterval <TimeSpan>] [-MaximumDGsAllowedInContactList <UInt32>] [-MaximumNumberOfContacts <UInt16>] [-MaxPhotoSizeKB <UInt32>] [-MusicOnHoldAudioFile <String>] [-P2PAppSharingEncryption <Supported | Enforced | NotSupported>] [-PlayAbbreviatedDialTone <$true | $false>] [-PolicyEntry <PSListModifier>] [-SearchPrefixFlags <UInt16>] [-ShowManagePrivacyRelationships <$true | $false>] [-ShowRecentContacts <$true | $false>] [-ShowSharepointPhotoEditLink <$true | $false>] [-SPSearchCenterExternalURL <String>] [-SPSearchCenterInternalURL <String>] [-SPSearchExternalURL <String>] [-SPSearchInternalURL <String>] [-TabURL <String>] [-TracingLevel <Off | Light | Full>] [-WebServicePollInterval <TimeSpan>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會修改用戶端原則 RedmondClientPolicy。在此範例中，WebServicePollInterval 屬性設為 15 分鐘 (00 小時：15 分鐘：00 秒) 的 A/V Edge 組態設定。

    Set-CsClientPolicy -Identity RedmondClientPolicy -WebServicePollInterval "00:15:00"

## 範例 2

範例 2 會修改用戶端原則 RedmondClientPolicy 的三個不同屬性值：DisableEmoticons、DisableHtmlIm 和 DisableRTFIm 屬性全都設為 True。

    Set-CsClientPolicy -Identity RedmondClientPolicy -DisableEmoticons $True -DisableHtmlIm $True -DisableRTFIm $True

## 範例 3

範例 3 也會修改 DisableEmoticons、DisableHtmlIm 和 DisableRTFIm 屬性。但此範例會修改網站範圍所設定的所有用戶端原則。為達成此目的，命令會先使用 **Get-CsClientPolicy** Cmdlet 和 Filter 屬性，傳回 Identity 開頭字元為 "site:" 的所有用戶端原則；根據定義，這些是在網站範圍設定的原則。然後再將篩選後的集合管線傳送到 **Set-CsClientPolicy** Cmdlet，以取得集合中的每一個原則，並修改 DisableEmoticons、DisableHtmlIm 和 DisableRTFIm 的值。

    Get-CsClientPolicy -Filter "*site:*" | Set-CsClientPolicy -DisableEmoticons $True -DisableHtmlIm $True -DisableRTFIm $True

## 範例 4

在範例 4 中，允許相片大於 10 KB 的所有用戶端原則都會經過修改；修改後，這些原則的相片大小上限為 10 KB。為達成此目的，會先呼叫不含任何參數的 **Get-CsClientPolicy** Cmdlet，以傳回設定供組織使用之所有用戶端原則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 MaxPhotoSizeKb 屬性大於 (-gt) 10 KB 的原則。接著將篩選後的集合管線傳送到 **Set-CsClientPolicy** Cmdlet，以將集合中每個原則的 MaxPhotoSizeKb 屬性值設為 10 KB。

    Get-CsClientPolicy | Where-Object {$_.MaxPhotoSizeKb -gt 10} | Set-CsClientPolicy -MaxPhotoSizeKb 10

## 詳細描述

在 Lync Server 中，用戶端原則取代了舊版產品中所使用的「群組原則」設定。在 Microsoft Office Communicator 2007 和 Microsoft Office Communicator 2007 R2 中，可使用「群組原則」協助決定使用者可以用 Communicator 及其他用戶端做些什麼；例如，「群組原則」設定決定使用者是否可以儲存其立即訊息交談的記錄、來自 Microsoft Outlook 的資訊是否整合到他們的目前狀態資訊，以及使用者是否可以在立即訊息中加入表情或格式化文字。

儘管「群組原則」如此有用，它在技術上仍有限制，尤其是在套用到 Lync Server 時。首先，「群組原則」的設計是根據個別網域或個別 OU 而套用原則；這使得它很難將原則套用到更精確選取的使用者群組 (例如，在特定部門工作的所有使用者，或是所有有特定工作職稱的使用者)。另一方面，「群組原則」只會套用到登入網域的使用者，以及使用電腦登入的使用者；「群組原則」不會套用到透過網際網路存取 Lync Server 的使用者，或使用行動電話存取系統的使用者。這就表示，同一名使用者隨著登入裝置以及登入位置的不同，就會有不同的使用經驗。

為了解決這些不一致的問題， Lync Server 使用用戶端管理原則而不是「群組原則」。用戶端原則會在使用者每一次存取系統時套用，不管使用者從何處登入以及使用何種裝置登入。此外，用戶端原則 (如同其他 Lync Server 原則) 很容易便可套用到選取的使用者群組。您甚至可以建立指派給單一使用者的自訂原則。

用戶端原則可以在全域、網站和個別使用者範圍設定 **Set-CsClientPolicy** Cmdlet 可讓您修改已設定為在組織中使用的任何 (或所有) 用戶端原則。

請記住，用戶端原則與其他許多原則都不同，因為大多數原則設定都沒有預設值。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsClientPolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsClientPolicy"}

## 參數


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>必要</th>
<th>類型</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AddressBookAvailability</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Client.AddressBookAvailability</p></td>
<td><p>表示如何讓使用者存取 Address Book Server 中的資訊 (亦即，使用 通訊錄 Web 查詢服務和/或將通訊錄複本下載到其本機電腦)。AddressBookAvailability 必須設為下列其中一個值：</p>
<p>WebSearchAndFileDownload</p>
<p>WebSearchOnly</p>
<p>FileDownloadOnly</p></td>
</tr>
<tr class="even">
<td><p><em>AttendantSafeTransfer</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 True 時， Lync 服務員會在「安全轉接」模式下運作；也就是說未連絡到預期接聽者的轉接通話將會重新出現在來電區域，並且附上「轉接失敗」通知。設為 False 時，無法連絡到預期接聽者的轉接通話將不會重新出現在來電區域。</p></td>
</tr>
<tr class="odd">
<td><p><em>AutoDiscoveryRetryInterval</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>嘗試連線失敗後，指定 Lync 再次嘗試連線到 Lync Server 之前要等待的時間。AutoDiscoveryRetryInterval 可以設定為 1 秒 和 60 分鐘 (1 小時) (含) 之間的值。</p>
<p>當指定 AutoDiscoveryRetryInterval 時，您必須使用時:分:秒的格式表示。例如，使用下列語法，將間隔設定為 25 分鐘：</p>
<p>- AutoDiscoveryRetryInterval 00:25:00</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [重試自動尋找的時間間隔] 群組原則設定。</p></td>
</tr>
<tr class="even">
<td><p><em>BlockConversationFromFederatedContacts</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，組織外部的連絡人將無法與適用此原則的任何使用者起始立即訊息交談。不過，只要內部使用者起始該交談，外部使用者將能夠參與交談。設為 False 時，外部連絡人可以將未經同意的立即訊息傳送給組織中的使用者。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [封鎖來自聯盟連絡人的交談] 群組原則設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>CalendarStatePublicationInterval</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>指定 Lync 在從 Microsoft Outlook 擷取行事曆資訊，並將此資料新增到目前狀態資訊之前所等待的秒數。</p>
<p>例如，使用下列語法，將 CalendarStatePublicationInterval 設定為 10 分鐘 (600 秒)：</p>
<p>- CalendarStatePublicationInterval 600</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [發佈行事曆資料至目前狀態的時間間隔] 群組原則設定。</p></td>
</tr>
<tr class="even">
<td><p><em>ConferenceIMIdleTimeout</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>表示使用者可以持續在立即訊息工作階段中，而不傳送或接收立即訊息的分鐘數。</p>
<p>ConferenceIMIdleTimeout 必須小於或等於 1 小時，而且必須使用時:分:秒的格式指定。例如，下列語法將逾時值設定為 45 分鐘：</p>
<p>-ConferenceIMIdleTimeout 00:45:00</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>CustomizedHelpUrl</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>組織所設定之自訂 Lync 說明的 URL。每當使用者按一下 Lync 中的 [說明] 功能表時，都會顯示此說明，而不會顯示預設的產品說明。此參數已被淘汰，無法再於 Lync Server 2013中使用。</p>
<p>除非您也將 EnableEnterpriseCustomizedHelp 設為 True，否則將無法使用自訂說明。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [說明功能表] 群組原則設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>CustomLinkInErrorMessages</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可以新增到出現在 Lync 中之錯誤訊息的網站 URL。如果有指定 URL，該 URL 將會出現在 Lync 中所發生之任何錯誤訊息的底部。然後，在使用者按一下該連結之後，就會前往包含其他資訊、疑難排解秘訣等等的自訂網站。</p></td>
</tr>
<tr class="even">
<td><p><em>CustomStateUrl</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>指定將自訂目前狀態新增至 Lync 所使用之 XML 檔案的位置 (除了「線上」、「忙碌」和「請勿打擾」等內建狀態之外， Lync 還允許最多再自訂四個目前狀態)。XML 檔案的位置應該使用 HTTPS 通訊協定指定。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [自訂目前狀態 URL] 群組原則設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓系統管理員提供關於原則的其他資訊。例如，「描述」可以指出被指派原則的使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>DGRefreshInterval</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>表示 Lync 在自動重新整理已在連絡人清單中「展開」之任何通訊群組成員資格清單前所等待的時間 (展開通訊群組表示顯示該群組中的所有成員)。DGRefreshInterval 可以設定為 30 和 28,800 秒 (8 小時) (含) 之間的任何整數值。預設值為 28,800 秒。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [重新整理每個通訊群組成員的時間間隔] 群組原則設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>DisableCalendarPresence</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，從 Microsoft Outlook 所取得的行事曆資料將不會包含在目前狀態資訊中。設為 False 時，行事曆資料將會包含在目前狀態資訊中。例如，連絡人卡片中會報告空閒/忙碌資訊；同樣地，只要 Outlook 在任何時候顯示您在會議中，就會將您的狀態自動設為「忙碌」。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [停用行事曆目前狀態] 群組原則設定。</p></td>
</tr>
<tr class="even">
<td><p><em>DisableContactCardOrganizationTab</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 True 時，在 Lync 使用者介面中看不到連絡人卡片的 [組織] 索引標籤。設為 False 時，在 Lync 中可以使用連絡人卡片的 [組織] 索引標籤。</p></td>
</tr>
<tr class="odd">
<td><p><em>DisableEmailComparisonCheck</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，Lync 將不會嘗試確認目前正在執行的任何 Microsoft Outlook 執行個體是否都屬於執行 Lync 的同一個使用者；例如，此軟體將不會確認 Outlook 和 Lync 是否都使用 Ken Myer 的使用者帳戶執行。該軟體會假設這兩個應用程式都由同一個帳戶執行，而且會依序地將 Outlook 連絡人和行事曆資料加入 Lync 中。</p>
<p>設為 False 時， Lync 將會使用 SMTP 位址確認 Outlook 和 Lync 是否以同一個帳戶執行。如果 SMTP 位址不符，則 Outlook 中的連絡人和行事曆資料將不會納入 Lync 中。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>DisableEmoticons</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，使用者將無法傳送或接收其立即訊息中的表情符號，但是他們可以看到這些表情符號的相對應文字。例如，使用者看不到圖形的「笑臉」，但是會看到相對應文字：</p>
<p>: )</p>
<p>設為 False 時，使用者將可以在其立即訊息中加入表情符號，並在所收到的立即訊息中看到表情符號。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [在立即訊息中停用表情符號] 群組原則設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>DisableFederatedPromptDisplayName</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，將您新增至同盟使用者之連絡人清單時產生的任何通知對話方塊將會使用同盟使用者的 SIP 位址 (例如，sip:kenmyer@fabrikam.com)。設為 False 時，通知對話方塊將會改用同盟使用者的顯示名稱 (例如，Ken Myer)。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [防止在通知對話方塊中顯示非 PIC 的同盟連絡人的顯示名稱] 群組原則設定。</p></td>
</tr>
<tr class="even">
<td><p><em>DisableFeedsTab</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 True 時，[活動摘要] 索引標籤將不會顯示在 Lync 中。設為 False 時，[摘要] 索引標籤將可以在 Lync 中使用。</p></td>
</tr>
<tr class="odd">
<td><p><em>DisableFreeBusyInfo</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，從 Microsoft Outlook 擷取的空閒/忙碌資訊將不會顯示在連絡人卡片中。設為 False 時，空閒/忙碌資訊會顯示在連絡人卡片中。例如，您的連絡人卡片可能會加入類似如下的記事：</p>
<p>行事曆: 在 2:00 PM 之前皆為空閒</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [停用發佈空閒/忙碌資訊] 群組原則設定。</p></td>
</tr>
<tr class="even">
<td><p><em>DisableHandsetOnLockedMachine</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若設為 True，當電話所連接的電腦為鎖定時，使用者將無法使用其 Polycom 電話。若要使用該電話，必須先解除鎖定電腦。</p>
<p>若設為 False，即使電話所連接的電腦為鎖定，使用者仍可使用其電話。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [設定鎖定電腦上的話筒使用方式] 群組原則設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>DisableHtmlIm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，從網頁複製的任何 HTML 文字都會在貼入立即訊息後，轉換為純文字。設為 False 時，則會在貼入立即訊息後，將 HTML 格式 (例如字型大小和色彩、下拉式清單和按鈕等等) 保留下來。</p>
<p>請注意，即使在設為 False 時，指令碼及其他可能的惡意項目 (例如，播放音效的標記) 都不會複製到立即訊息中。您可以複製按鈕與其他控制項並將其貼入訊息中，但是附加到這些控制項的所有指令碼，則會自動遭到移除。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [防止立即訊息中的 HTML 文字] 群組原則設定。</p></td>
</tr>
<tr class="even">
<td><p><em>DisableInkIM</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，使用者將無法接收包含 Tablet PC 筆跡的立即訊息 (「筆跡」是一種技術，可讓您將手寫記事插入到文件中)。設為 False 時，使用者將可以接收包含 Tablet PC 筆跡的訊息。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [防止立即訊息中的筆跡] 群組原則設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>DisableMeetingSubjectAndLocation</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 False 時，如果您檢視連絡人卡片中的空閒/忙碌資訊，會議的詳細資訊 (即會議主旨和會議舉辦的地點) 將會顯示為工具提示。設為 True 時，將不會顯示這個詳細資訊。若要完全防止顯示會議相關資訊，還必須將 DisableCalendarPresence 設為 True。</p>
<p>此設定相當於 Communications Server 2007 R2 的 [停用發佈面談主題和位置資訊] 群組原則設定。</p></td>
</tr>
<tr class="even">
<td><p><em>DisableOneNote12Integration</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 True 時，會停用從 Lync 中啟動 Microsoft OneNote 的功能 (以及自動連結立即訊息工作階段與 OneNote 筆記的功能)。設為 False 時，會在 Lync 中啟用 [使用 OneNote 記錄筆記] 選項。此外，如果您在 Microsoft Outlook 的 [交談記錄] 中找到立即訊息文字記錄，只要按一下 [編輯交談記事] 按鈕，就可以擷取與該交談相關聯的所有 OneNote 筆記。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [停用 OneNote 12 整合] 群組原則設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>DisableOnlineContextualSearch</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，停用以滑鼠右鍵按一下連絡人清單中的使用者時出現的 [尋找先前的交談] 功能表選項 (此選項可讓您搜尋 Microsoft Outlook [交談記錄] 資料夾中，包含上述使用者的舊立即訊息工作階段)。設為 False 時，如果以滑鼠右鍵按一下連絡人清單中的使用者，就可以使用 [尋找先前的交談] 選項。</p>
<p>請注意，此設定僅適用於沒有在快取模式下執行 Microsoft Outlook 的使用者。那是因為這些使用者所執行的任何搜尋都必須在 Exchange 伺服器上進行，而且系統管理員可能會想要限制這些搜尋所造成的網路流量。如果您是在快取模式下執行 Outlook，搜尋就會在使用者收件匣的本機快取複本上進行。快取搜尋不會受到此設定的影響。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [停用線上內容相關式搜尋] 群組原則設定。</p></td>
</tr>
<tr class="even">
<td><p><em>DisablePhonePresence</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 True 時，如果要判斷您目前的狀態， Lync 不會將電話列入考量。設為 False 時，如果要判斷您的狀態，則會將電話列入考量。例如，您在電話中的任何時候，都會將您的狀態自動設為「忙碌」。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [停用電話目前狀態] 群組原則設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>DisablePICPromptDisplayName</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，如果具有公用立即訊息服務帳戶 (例如 MSN) 的使用者將您新增至其連絡人清單，此時產生的任何通知對話方塊會顯示該使用者的 SIP 位址 (例如，sip:kenmyer@litwareinc.com)。設為 False 時，通知對話方塊將會改用該使用者的顯示名稱 (例如，Ken Myer)。</p>
<p>此設定相當於 Communications Server 2007 R2 的 [防止在通知對話方塊中顯示 PIC 連絡人的顯示名稱] 群組原則設定。</p></td>
</tr>
<tr class="even">
<td><p><em>DisablePoorDeviceWarnings</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 True 時，如果音訊或視訊裝置沒有正確運作， Lync 將不會發出警告 (啟動後、在「微調精靈」中、在 [交談] 視窗中等等)。設為 False 時，將會發出這些警告。</p></td>
</tr>
<tr class="odd">
<td><p><em>DisablePoorNetworkWarnings</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時， Lync 將不會顯示網路品質不良的相關警告。</p></td>
</tr>
<tr class="even">
<td><p><em>DisablePresenceNote</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，您在 Microsoft Outlook 中設定的任何「不在辦公室」訊息，都不會顯示為目前狀態資訊的一部分。設為 False 時，每次使用者將滑鼠停留在其連絡人清單中您的名稱上時，就會顯示您的「不在辦公室」訊息。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [停用目前狀態記事] 群組原則設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>DisableRTFIM</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>當此設定與 DisableHtmlIm 設定都設為 True 時，將無法在立即訊息中使用 RTF 格式 (例如，不同的字型、字型大小和字型色彩)；傳送與接收的所有訊息都會轉換成純文字格式。設為 False 時，允許在立即訊息中使用 RTF 格式。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [防止在立即訊息中使用 RTF 文字] 群組原則設定。</p></td>
</tr>
<tr class="even">
<td><p><em>DisableSavingIM</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 True 時，用於儲存立即訊息工作階段的選項都會從 [ Lync 交談] 視窗的功能表列中移除。設為 False 時，則可在 [交談] 視窗中使用這些選項。</p>
<p>請注意，將此值設為 True 時，會移除可讓使用者輕鬆儲存立即訊息文字記錄的功能表選項。不過，使用者可以將文字記錄中的所有文字複製到剪貼簿、將該文字貼入其他應用程式，然後以此種方式儲存文字記錄。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [防止使用者儲存立即訊息] 群組原則設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayPhoto</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Client.DisplayPhoto</p></td>
<td><p>決定是否要在 Lync 中顯示相片 (使用者及其連絡人的相片)。有效的設定為：</p>
<p>NoPhoto - 在 Lync 中不會顯示相片。</p>
<p>PhotosFromADOnly - 只能顯示已經在 Active Directory 網域服務 中發佈的相片。</p>
<p>AllPhotos - 可以顯示 Active Directory 相片或自訂相片。</p>
<p>預設值為 AllPhotos。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableAppearOffline</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 True 時，在 Lync 中可以使用其他目前狀態，也就是「顯示為離線」。即使使用者離線，此狀態都可以使其出現，不過，使用者實際上將是連線狀態，而且可以接聽電話、回應立即訊息等等。設為 False 時，在 Lync 中將無法使用「顯示為離線」目前狀態。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [啟用顯示為離線狀態] 群組原則設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableCallLogAutoArchiving</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，來電與撥出電話的資訊又會自動儲存到 Microsoft Outlook 的 [交談記錄] 資料夾中 (系統不會記錄實際通話本身。所記錄的資訊包括參與通話者、通話長度，以及這是來電或撥出電話等等)。設為 False 時，這項資訊不會儲存到 Outlook。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [啟用/停用將電話記錄自動封存至 Outlook 信箱] 群組原則設定。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableClientMusicOnHold</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，如果來電者處於保留狀態，就會播放音樂。設為 False 時，如果來電者處於保留狀態，將不會播放音樂。預設值為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableConversationWindowTabs</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，與立即訊息工作階段相關的補充資訊將會顯示在另一個瀏覽器視窗中。此類型的資訊僅適用於使用 Microsoft Unified Communications Managed API (UCMA) 的自訂應用程式。例如，客戶服務或服務台人員在與他人交談的同時，可以自動存取相關的資訊。</p>
<p>設為 False 時，補充資訊將不會顯示在另一個瀏覽器視窗中。雖然使用者仍然可以參與立即訊息工作階段，但無法存取該工作階段所隨附的其他任何資訊。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的群組原則設定 [啟用交談視窗索引標籤]。 Lync Server 2013已淘汰此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableEnterpriseCustomizedHelp</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 True 時，在 Lync 中按一下 [說明] 功能表的使用者將會獲得組織所設定的自訂說明。設為 False 時，按一下 [說明] 功能表的使用者將會獲得預設的 Lync 產品說明。</p>
<p>當您啟用自訂說明時，也必須指定自訂說明網站的 URL；這是使用 CustomizedHelpUrl 參數完成的。若未指定此參數，或者 URL 無效，則當使用者嘗試排程或加入會議時，可能會發生錯誤。</p>
<p>Lync Server 2013已淘汰此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableEventLogging</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 True 時， Lync 的詳細資訊將會記錄在應用程式事件記錄檔中。設為 False 時，只有主要的事件 (例如，連線到 Lync Server 失敗) 會記錄在事件記錄檔中。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [開啟 Communicator 2007 的事件記錄] 群組原則設定。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableExchangeContactSync</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 True (預設值) 時， Lync 會針對使用者的 [ Lync 連絡人] 清單中的每個人，在 Microsoft Outlook 中建立對應的個人連絡人。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableExchangeDelegateSync</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，使用者已經在 Microsoft Exchange 中設定的代理人將可以針對該使用者排程線上會議。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableFullScreenVideo</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 True 時，會進行兩件事：1) 啟用 Lync 通話的全螢幕視訊 (具有正確外觀比例)；以及 2) 停用 Lync 通話的視訊預覽。設為 False 時，則無法在 Lync 中使用全螢幕視訊，但可以使用視訊預覽。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [啟用全螢幕視訊，並停用所有 OC 視訊撥號的視訊預覽] 群組原則設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableHighPerformanceConferencingAppSharing</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若設為 True，就能提升螢幕重新整理頻率高的應用程式 (如 CAD/CAM 應用程式) 效能。不過，效能如果提升，其他應用程式可用的系統資源和網路頻寬就會減少。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableHighPerformanceP2PAppSharing</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，允許對等應用程式共用工作階段超過最大畫面速率 (每秒 2.5 個畫面)。預設值為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableHotdesking</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 True 時，讓使用者使用其 Lync Phone Edition 帳戶登入共用工作區中執行 Lync Server 的電話 (除此之外，這可讓使用者存取其連絡人)。設為 False 時，使用者無法使用其專屬認證登入共用工作區中的電話。</p>
<p>請注意，此設定僅適用於公共區域 (共用工作區) 帳戶，不適用於使用者帳戶。設為 True 且套用至共用工作區中電話的公共區域帳戶時，任何使用者都能使用其認證登入該電話。設為 False 時，將不允許任何人登入該電話。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>EnableIMAutoArchiving</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，使用者所參與之每個立即訊息工作階段的文字記錄都會儲存到 Microsoft Outlook 的 [交談記錄] 資料夾中。設為 False 時，則不會自動儲存這些文字記錄 (不過，使用者可以選擇手動儲存立即訊息文字記錄)。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [啟用/停用將 IM 對話自動封存至 Outlook 信箱] 群組原則設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableMediaRedirection</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True ($True) 時，可讓音訊及視訊資料流與其他網路流量分開；如此可讓用戶端裝置在本機執行音訊及視訊的編碼和解碼作業。與裝置遠端處理或轉碼器壓縮等類似的技術相較，媒體重新導向通常會使頻寬使用較低、伺服器擴充性較高，且使用者經驗較佳。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableNotificationForNewSubscribers</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 True 時，當您被新增到別人的 [連絡人] 清單時，將會收到通知。此外，[通知] 對話方塊將會讓您選擇將該人員新增至您的 [連絡人] 清單，或封鎖此人員，不讓他檢視您的目前狀態資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableSQMData</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>注意： Lync Server 2013已不再使用此設定。</p>
<p>客戶經驗改進計畫 (CEIP) 是為了幫助 Mirosoft 收集 Lync 的實際使用情形而設計。當使用者加入 CEIP 時，每次使用者執行 Lync 時，就會將該使用者所執行的動作、多久執行該動作等相關資訊傳送回 Microsoft、存入資料庫，然後加以分析，以協助識別使用趨勢。</p>
<p>當 EnableSQMData 設為 True 時，不會自動將使用者加入客戶經驗改進計劃。但是， Lync 會提供使用者加入該計畫的選項。</p>
<p>設為 False 時，使用者不會在客戶經驗改進計畫 (CEIP) 中註冊。此外， Lync 也不會提供使用者加入該計畫的選項。使用者加入 CEIP 計畫的唯一方法，就是將 EnableSQMData 設為 True，然後由使用者手動選擇加入該計畫。</p>
<p>請注意，系統不會將個人識別資訊傳送到 CEIP。CEIP 不會追蹤您傳送立即訊息給誰，以及誰傳送立即訊息給您之類的事情。但是，此程式會追蹤使用者使用 Lync 傳輸檔案的頻率，或使用者的 [連絡人清單] 上所擁有之平均連絡人數目之類的資訊。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [指定檢測設備] 群組原則設定。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableTracing</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 True 時，將會在 Lync 中啟用軟體追蹤；設為 False 時，則會停用軟體追蹤。軟體追蹤包含保留程式所進行之所有事項的詳細記錄 (包括追蹤 API 呼叫)。因此，這類追蹤對於開發人員以及應用程式支援人員而言多半非常重要。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [開啟 Communicator 2007 的追蹤功能] 群組原則設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableUnencryptedFileTransfer</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，使用者可以與其立即訊息軟體不支援加密檔案傳輸的外部使用者交換檔案。設為 False 時，使用者只能與具備支援加密檔案傳輸之軟體的外部使用者交換檔案。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [允許傳輸未加密的檔案] 群組原則設定。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableURL</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，內嵌在立即訊息中的超連結將是「可點選的」，也就是說，使用者按一下該連結，其網頁瀏覽器便會開啟到指定的位置。設為 False 時，超連結在立即訊息中會以純文字顯示。若要瀏覽到該位置，使用者必須複製連結文字，然後將其貼到網頁瀏覽器中。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [允許立即訊息中有超連結] 群組原則設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableVOIPCallDefault</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 True 時，如果使用者採用按一下撥打功能，就會撥打 Lync 電話。</p>
<p>此原則設定僅會影響按一下撥打功能的初始狀態。如果使用者修改按一下撥打設定的值，則使用者選取的值將覆寫此原則設定。使用者修改按一下撥打設定的值後，將繼續使用該設定，而且不會受到 EnableVOIPCallDefault 原則的影響。</p></td>
</tr>
<tr class="even">
<td><p><em>ExcludedContactFolders</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>表示每次 Lync 搜尋新連絡人時，不應該搜尋哪些 Microsoft Outlook 連絡人資料夾 (如果有的話)。使用分號分隔資料夾名稱可以指定多個資料夾，例如：-ExcludedContactFolders &quot;SenderPhotoContacts;OtherContacts&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>HelpEnvironment</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此參數設為 &quot;Office 365&quot; 時，會向使用者顯示 Lync Server 2013的 Office 365 用戶端說明文件，而不是根據預設顯示的內部部署說明。您可以將 HelpEnvironment 設為 &quot;Office 365&quot; 或 Null 值 ($Null)。如果設為 Null 值 (預設值)，就會向使用者顯示內部部署說明。</p></td>
</tr>
<tr class="odd">
<td><p><em>HotdeskingTimeout</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>使用者登入「公用辦公桌」電話的時間間隔 (公用辦公桌的電話是一種執行 Lync Phone Edition 的電話，位於共用工作區，而且使用者可以使用其 Lync Server 帳戶登入)。公用辦公桌逾時會指定使用者自動登出公用辦公桌電話前所經過的分鐘數。當指定公用辦公桌逾時值時，必須使用時:分:秒的格式表示。例如，下列語法會將公用辦公桌逾時間隔設定為 45 分鐘：</p>
<p>-HotdeskingTimeout 00:45:00</p>
<p>請注意，此原則設定僅適用於公共區域電話，而不適用於使用者。預設值為 5 分鐘 (00:05:00)，最小值為 30 秒 (00:00:30)。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>指派給新原則的唯一識別碼。若要參照全域原則，請使用下列語法：-Identity global。若要參照網站原則，請使用首碼 &quot;site:&quot;並使用網站名稱做為 Identity。例如：-Identity site:Redmond。若要參照個別使用者原則，請使用類似下列的語法：-Identity SalesClientPolicy。</p></td>
</tr>
<tr class="odd">
<td><p><em>IMWarning</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>如果有設定，每次使用者參與立即訊息工作階段時，指定的訊息就會出現在 [交談] 視窗中。例如，如果 IMWarning 設為 &quot;All information is the property of Litwareinc&quot; (所有資訊均為 Litwareinc 的財產)，則每次使用者參與立即訊息工作階段時，該訊息就會出現在 [交談] 視窗中。</p>
<p>您的警告訊息長度上限為 256 個字元，且只能包含純文字。您不能使用任何格式 (例如粗體或斜體)，或在文字內包含可點選的 URL。</p>
<p>如果設為 Null 值 ($Null)，則交談視窗中不會出現任何訊息。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [警告文字] 群組原則設定。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>ClientPolicy</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>MAPIPollInterval</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>重要：此參數已被淘汰，無法再於 Lync Server 2013中使用。</p>
<p>對於 Microsoft Exchange Server 2003 的使用者，MAPIPollInterval 會指定 Lync 從 Exchange 公用資料夾擷取行事曆資料的頻率。MAPIPollInterval 可以設定為 1 秒 和 1 小時 (含) 之間的任何值。若要設定 MAPI 輪詢間隔，需使用時:分:秒的格式表示。例如，下列命令會將 MAPI 輪詢間隔設定為 45 分鐘：</p>
<p>-MapiPollInterval 00:45:00</p>
<p>請注意，此設定不適用於其電子郵件帳戶位於 Microsoft Exchange Server 2010 或 Microsoft Exchange Server 2007 的使用者。對於這些使用者，行事曆擷取是使用 WebServicePollInterval 進行管理。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [從 MAPI 提供者載入行事曆資料的時間間隔] 群組原則設定。</p></td>
</tr>
<tr class="even">
<td><p><em>MaximumDGsAllowedInContactList</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>表示使用者可以設定為連絡人之通訊群組的數目上限。MaximumDGsAllowedInContactList 可以設為 0 和 64 (含) 之間的任何整數值。預設值為 10。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaximumNumberOfContacts</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>表示允許一個使用者擁有的連絡人數目上限。連絡人上限可以設為 0 和 1000 (含) 之間的任何整數值。設為 0 時，使用者無法擁有任何連絡人。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [允許的連絡人最大數量] 群組原則設定。</p></td>
</tr>
<tr class="even">
<td><p><em>MaxPhotoSizeKB</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>表示在 Lync 中顯示之相片的大小上限 (KB)。</p>
<p>預設值為 30 KB。</p></td>
</tr>
<tr class="odd">
<td><p><em>MusicOnHoldAudioFile</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>來電者處於保留狀態時播放之音訊檔案的路徑。如果針對此屬性設定值，將會啟用保留音樂，而且使用者將無法停用此功能。如果未針對此屬性設定值，則使用者可以假設 EnableClientMusicOnHold 設為 True，以指定自己的保留音樂檔案。</p></td>
</tr>
<tr class="even">
<td><p><em>P2PAppSharingEncryption</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Client.P2PAppSharingEncryption</p></td>
<td><p>表示是否加密對等交談期間交換的桌面和應用程式共用資料。允許的值為：</p>
<p>Supported。如果可能，將會加密桌面和應用程式共用資料。</p>
<p>Enforced。必須加密桌面和應用程式共用資料。如果無法加密資料，則不會為交談啟用桌面和應用程式共用。</p>
<p>NotSupported。將不加密桌面和應用程式共用資料。</p></td>
</tr>
<tr class="odd">
<td><p><em>PlayAbbreviatedDialTone</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 True 時，只要拿起 Lync 相容話筒撥號，就會播放 3 秒鐘撥號聲 ( Lync 相容話筒的外觀就像是標準電話，但是插入電腦上的 USB 連接埠，而且是用來撥打 Lync 電話，而不是「一般」電話)。設為 False 時，只要拿起 Lync 相容話筒撥號，就會播放 30 秒鐘撥號聲。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [播放簡短撥號聲] 群組原則設定。</p></td>
</tr>
<tr class="even">
<td><p><em>PolicyEntry</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>提供新增預設參數未涵蓋之設定的一種方式。例如，在測試 Microsoft Lync Server 2010 的前版本時，可以將 [傳送意見反應] 選項新增到 Microsoft Lync 2010。作法是使用類似下列的程式碼：</p>
<p>$x = New-CsClientPolicyEntry -Name &quot;OnlineFeedbackURL&quot; -Value &quot;http://www.litwareinc.com/feedback&quot;Set-CsClientPolicy -Identity global -PolicyEntry @{Add=$x}</p>
<p>如需詳細資訊和範例，請參閱 <a href="new-csclientpolicyentry.md">New-CsClientPolicyEntry</a> Cmdlet 說明主題。</p></td>
</tr>
<tr class="odd">
<td><p><em>SearchPrefixFlags</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>表示每次使用者搜尋新連絡人時應該使用的 [通訊錄] 屬性。搜尋首碼旗標會建構為類似二進位數字 (例如 11101111)，其中 1 表示應該搜尋屬性，而 0 表示不應該搜尋屬性。二進位值中的屬性為 (從右到左)：</p>
<p>主要電子郵件地址</p>
<p>電子郵件別名</p>
<p>所有電子郵件地址</p>
<p>公司</p>
<p>顯示名稱</p>
<p>名字</p>
<p>姓氏</p>
<p>二進位值 1110111 表示除了屬性 4 之外，應該搜尋所有屬性：公司。若要只搜尋顯示名稱、名字和姓氏，您需要建構此值：</p>
<p>1110000</p>
<p>二進位值建構完成之後，必須先轉換為十進位值，才能指派給 SearchPrefixFlags。若要將二進位數字轉換為十進位數字，您可以使用下列 Windows PowerShell 命令：</p>
<p>[Convert]::ToInt32(&quot;1110111&quot;, 2)</p></td>
</tr>
<tr class="even">
<td><p><em>ShowManagePrivacyRelationships</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 True 時，會在 [ Lync 連絡人清單] 視窗中顯示 [關聯] 選項。設為 False 時，則會隱藏 [關聯] 選項。</p>
<p>請注意，此設定僅會套用至 Lync 2010。即使 ShowManagePrivacyRelationships 設為 True， Lync 2013 也不會顯示這些關聯。</p>
<p>預設值為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>ShowRecentContacts</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數在用戶端上沒有作用。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>ShowSharepointPhotoEditLink</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數如果設為 True， Lync 將會包含一個連結，讓使用者編輯儲存在其 SharePoint MySite 上的個人相片。預設值為 False，表示 Lync 將不會包含指向 SharePoint MySite 的連結。</p></td>
</tr>
<tr class="odd">
<td><p><em>SPSearchCenterExternalURL</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>用於關鍵字搜尋 (亦稱為專家搜尋) 之 SharePoint 網站的外部 URL。此 URL 將會出現在 Lync 中所顯示之任何關鍵字搜尋結果的底部。如果使用者按一下此 URL，使用者的網頁瀏覽器將會開啟到 SharePoint 網站，讓他們有機會使用 SharePoint 的搜尋功能進行搜尋 (SharePoint 比 Lync 提供更多搜尋選項)。</p>
<p>SPSearchCenterExternalURL 代表用於外部使用者的 URL；亦即，從組織防火牆外部登入的使用者。SPSearchCenterInternalURL 參數用於從防火牆內部登入的使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>SPSearchCenterInternalURL</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>用於關鍵字搜尋 (亦稱為專家搜尋) 之 SharePoint 網站的內部 URL。此 URL 將會出現在 Lync 中所顯示之任何關鍵字搜尋結果的底部。如果使用者按一下此 URL，使用者的網頁瀏覽器將會開啟到 SharePoint 網站，讓他們有機會使用 SharePoint 的搜尋功能進行搜尋 (SharePoint 比 Lync 提供更多搜尋選項)。</p>
<p>SPSearchCenterInternalURL 代表用於內部使用者的 URL；亦即，從組織防火牆內部登入的使用者。SPSearchCenterExternalURL 參數用於從防火牆外部登入的使用者。</p></td>
</tr>
<tr class="odd">
<td><p><em>SPSearchExternalURL</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>用於關鍵字搜尋 (亦稱為專家搜尋) 之 SharePoint 網站的外部 URL。每次外部使用者 (亦即，從組織防火牆外部存取系統的使用者) 進行關鍵字搜尋時， Lync 將會使用位於此 URL 的 SharePoint 網站。</p></td>
</tr>
<tr class="even">
<td><p><em>SPSearchInternalURL</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>用於關鍵字搜尋 (亦稱為專家搜尋) 之 SharePoint 網站的內部 URL。每次內部使用者 (亦即，從組織防火牆內部登入的使用者) 進行關鍵字搜尋時， Lync 將會使用位於此 URL 的 SharePoint 網站。</p></td>
</tr>
<tr class="odd">
<td><p><em>TabURL</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>指定建立 [ Lync 連絡人清單] 視窗底部之自訂索引標籤所需之 XML 檔案的位置。自訂索引標籤可讓使用者從 Lync 中存取網頁 (例如服務台網頁)。 Lync Server 2013已淘汰此參數。</p>
<p>此設定相當於 Office Communications Server 2007 R2 的 [索引標籤 URL] 群組原則設定。</p></td>
</tr>
<tr class="even">
<td><p><em>TracingLevel</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Client.TracingLevel</p></td>
<td><p>可讓系統管理員管理 Lync 2013 中的事件追蹤及記錄。允許的值為：</p>
<p>* Off – 停用追蹤，使用者無法變更此設定。</p>
<p>* Light – 執行最基本的追蹤，使用者無法變更此設定。</p>
<p>* Full – 執行詳細資訊追蹤，使用者無法變更此設定。</p>
<p>根據預設，TracingLevel 設為 Light。</p></td>
</tr>
<tr class="odd">
<td><p><em>WebServicePollInterval</em></p></td>
<td><p>選用</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>對於 Microsoft Exchange Server 2007 和更新版本的使用者，WebServicePollInterval 會指定 Lync 從 Microsoft Exchange Server Web 服務擷取行事曆資料的頻率。WebServicePollInterval 可以設定為 1 秒和 1 小時 (含) 之間的任何值。若要設定 Web 服務輪詢間隔，需使用時:分:秒的格式表示。例如，下列命令會將 Web 服務輪詢間隔設定為 45 分鐘：</p>
<p>-WebServicePollInterval 00:45:00</p>
<p>請注意，此設定不適用於其電子郵件帳戶位於 Exchange 2003 的使用者。對於這些使用者，行事曆擷取是使用 MAPIPollInterval 進行管理。</p>
<p>此設定相當於 Communications Server 2007 R2 的 [從 Web 服務提供者載入行事曆資料的時間間隔] 群組原則設定。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Policy.Client.ClientPolicy 物件。 **Set-CsClientPolicy** Cmdlet 接受管線傳送的用戶端原則物件執行個體。

## 傳回類型

**Set-CsClientPolicy** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Policy.Client.ClientPolicy 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsClientPolicy](get-csclientpolicy.md)  
[Grant-CsClientPolicy](grant-csclientpolicy.md)  
[New-CsClientPolicy](new-csclientpolicy.md)  
[Remove-CsClientPolicy](remove-csclientpolicy.md)

