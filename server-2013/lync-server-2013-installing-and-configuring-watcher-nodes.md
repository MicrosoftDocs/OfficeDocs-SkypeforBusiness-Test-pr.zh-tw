---
title: 安裝和設定監看員節點
TOCTitle: 安裝和設定監看員節點
ms:assetid: 61f6deea-e3ef-4468-9be8-a65705815ebb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204943(v=OCS.15)
ms:contentKeyID: 49291098
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 安裝和設定監看員節點

 

_**上次修改主題的時間：** 2015-03-09_

*「監看員節點」*為定時執行 Lync Server 綜合交易的電腦。*「綜合交易」*為 Windows PowerShell Cmdlet，用於驗證一般使用者的主要案例 (例如是否能登入系統，或是否能交換立即訊息) 是否運作如常。針對 Lync Server 2013，System Center Operations Manager 可以執行下表中顯示的綜合交易。表中顯示三種不同綜合交易類型：

  - **預設**。這些是監看員節點預設會執行的綜合交易。建立新的監看員節點時，可以選擇指定節點會執行的綜合交易。(此為 **New-CsWatcherNodeConfiguration** Cmdlet 使用 Tests 參數的目的。) 若在建立監看員節點時未使用 Tests 參數，則監看員節點會自動執行所有的預設綜合交易，而不會執行任何的非預設綜合交易。舉例而言，這表示監看員節點會設定執行 Test-CsAddressBookService 測試，但是不會設定執行 Test-CsExumConnectivity 測試。

  - **非預設**。如名稱所指，非預設綜合交易為監看員節點依預設不會執行的測試。不過，可以啟用監看員節點來執行任何非預設綜合交易。您可以在建立監看員節點時 (透過使用 **New-CsWatcherNodeConfiguration** Cmdlet)，或在建立後的任何時點進行啟用。許多非預設綜合交易需要額外的設定步驟。如需詳細資訊，請參閱＜[綜合交易的特殊設定指示](lync-server-2013-special-setup-instructions-for-synthetic-transactions.md)＞。

  - **延伸**。延伸測試為非預設綜合交易的特別類型。與其他綜合交易不同的是，延伸測試在每個行程中可以執行多次。在驗證如集區的多重公用電話交換網路 (PSTN) 語音路由時，這就非常有用。只要在監看員節點中新增延伸測試的多個執行個體，即可設定。

如需有關新增其他綜合交易至監看員節點之程序的詳細資訊，請參閱＜[管理監看員節點](lync-server-2013-managing-watcher-nodes.md)＞。您可以使用 Lync Server 管理命令介面，從監看員節點移除綜合交易。

監看員節點可用的綜合交易包括下列：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet 名稱 (測試名稱)</th>
<th>說明</th>
<th>綜合交易類型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Test-CsAddressBookService (ABS)</p></td>
<td><p>確認使用者可以查詢不在其連絡人清單中的使用者。</p></td>
<td><p>預設</p></td>
</tr>
<tr class="even">
<td><p>Test-CsAddressBookWebQuery (ABWQ)</p></td>
<td><p>確認使用者可以透過 HTTP 查詢不在其連絡人清單中的使用者。</p></td>
<td><p>預設</p></td>
</tr>
<tr class="odd">
<td><p>Test-CsIM (IM)</p></td>
<td><p>確認使用者可以傳送對等立即訊息。</p></td>
<td><p>預設</p></td>
</tr>
<tr class="even">
<td><p>Test-CsP2PAV (P2PAV)</p></td>
<td><p>確認使用者可以撥出對等音訊通話 (僅訊號)。</p></td>
<td><p>預設</p></td>
</tr>
<tr class="odd">
<td><p>Test-CsPresence (Presence)</p></td>
<td><p>確認使用者可以檢視其他使用者的目前狀態。</p></td>
<td><p>預設</p></td>
</tr>
<tr class="even">
<td><p>Test-CsRegistration (Registration)</p></td>
<td><p>確認使用者可以登入 Lync。</p></td>
<td><p>預設</p></td>
</tr>
<tr class="odd">
<td><p>Test-CsAudioConferencingProvider (ACP)</p></td>
<td><p>不使用 Lync Server 2013 的內部部署版本。</p></td>
<td><p>延伸</p></td>
</tr>
<tr class="even">
<td><p>Test-CsPstnPeerToPeerCall (PSTN)</p></td>
<td><p>確認使用者可以對企業外人員 (PSTN 號碼) 撥出及接聽通話。</p></td>
<td><p>非預設、延伸</p></td>
</tr>
<tr class="odd">
<td><p>Test-CsAVConference (AvConference)</p></td>
<td><p>確認使用者可以建立並參與音訊/視訊會議。</p></td>
<td><p>預設</p></td>
</tr>
<tr class="even">
<td><p>Test-CsAVEdgeConnectivity (AVEdgeConnectivity)</p></td>
<td><p>確認 A/V Edge Server 可以接受對等通話及電話會議的連線。</p></td>
<td><p>非預設</p></td>
</tr>
<tr class="odd">
<td><p>Test-CsDataConference (DataConference)</p></td>
<td><p>確認使用者可以參與資料共同作業會議 (包含如白板及投票等活動的線上會議)。</p></td>
<td><p>非預設</p></td>
</tr>
<tr class="even">
<td><p>Test-CsExumConnectivity (ExumConnectivity)</p></td>
<td><p>確認使用者可以連線至 Exchange 整合通訊 (UM)。</p></td>
<td><p>非預設</p></td>
</tr>
<tr class="odd">
<td><p>Test-CsGroupIM (GroupIM)</p></td>
<td><p>確認使用者可以在會議中傳送立即訊息，並參與有三位或更多位人員的立即訊息交談。</p></td>
<td><p>預設</p></td>
</tr>
<tr class="even">
<td><p>Test-CsGroupIM \endash TestJoinLauncher (JoinLauncher)</p></td>
<td><p>確認使用者可以透過網址連結建立並加入排程會議。</p></td>
<td><p>非預設</p></td>
</tr>
<tr class="odd">
<td><p>Test-CsMCXP2PIM (MCXP2PIM)</p></td>
<td><p>確認行動裝置使用者可以註冊並傳送立即訊息。</p></td>
<td><p>非預設</p></td>
</tr>
<tr class="even">
<td><p>Test-CsPersistentChatMessage (PersistentChatMessage)</p></td>
<td><p>確認使用者可以透過使用常設聊天室服務來交換訊息。</p></td>
<td><p>非預設</p></td>
</tr>
<tr class="odd">
<td><p>Test-CsUnifiedContactStore (UnifiedContactStore)</p></td>
<td><p>確認可以透過整合連絡人存放區來存取使用者的連絡人。整合連絡人存放區讓使用者可以維護單一組連絡人，而使用 Lync 2013、Outlook 及/或 Outlook Web Access 都可以存取。</p></td>
<td><p>非預設</p></td>
</tr>
<tr class="even">
<td><p>Test-CsXmppIM (XmppIM)</p></td>
<td><p>確認立即訊息可以跨 XMPP (Extensible Messaging and Presence Protocol) 閘道傳送。</p></td>
<td><p>非預設</p></td>
</tr>
</tbody>
</table>


您不需要為了使用 System Center Operations Manager 而安裝監看員節點。如果未安裝這些節點，當問題發生時，還是可以從 Lync Server 2013 元件取得即時警示。(「元件和使用者管理套件」不使用監看員節點。) 不過，如果要使用「主動式監控管理套件」監控端對端案例，就需要監看員節點。

> [!NOTE]  
> 系統管理員也不需要使用或安裝 Operations Manager，就可以手動執行綜合交易。如需有關各個 Test-Cs Cmdlet 的詳細資訊，請參閱＜<a href="https://docs.microsoft.com/en-us/powershell/module/skype/?view=skype-ps">Lync Server 2013 Cmdlet 索引</a>＞。



視部署大小而定，綜合交易可能會佔用大量電腦記憶體及處理器時間。因此，建議您使用專用電腦作為監看員節點。舉例來說，您不應設定前端伺服器作為監看員節點。監看員節點應符合下列硬體規格：

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>舊版 Microsoft Lync Server 2010 監看員節點無法與 Lync Server 2013 監看員節點組合在相同機器上。這是因為 Lync Server 2010 及 Lync Server 2013 的核心系統檔案無法安裝在相同電腦上。<br />
然而，Lync Server 2013 監看員節點可以同時監控 Lync Server 2013 及 Lync Server 2010。兩個產品版本都支援預設綜合交易。</td>
</tr>
</tbody>
</table>


可以在企業內或企業外部署 Lync Server 2013 監看員節點，以協助驗證下列事項：

   企業內使用者對集區的連線。

   於企業外工作的遠端使用者透過周邊網路的連線。

   對分公司設備的連線。

   對企業內及透過周邊網路對 Lync Server 2010 的連線。

對於簡化管理，企業內外有不同的驗證選項。如需詳細資訊，請參閱＜[設定監看員節點以執行綜合交易](lync-server-2013-configuring-a-watcher-node-to-run-synthetic-transactions.md)＞。

若要設定電腦作為監看員節點，在安裝 System Center Operations Manager 並匯入 Lync Server 2013 管理套件後，必須完成下列步驟。

在安裝 Lync Server 2013 核心檔案及 System Center 代理程式檔案前，也要確定監看員節點電腦符合所有安裝 Lync Server 2013 的必要條件。此外，監看員節點電腦還應該安裝下列項目：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>硬體元件</th>
<th>最低需求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CPU</p></td>
<td><p>下列其中一項：</p>
<ul>
<li><p>64 位元處理器、四核心、2.33 GHz 或更快速度</p></li>
<li><p>64 位元 2 向處理器、雙核心、2.33 GHz 或更高</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>記憶體</p></td>
<td><p>8 GB</p></td>
</tr>
<tr class="odd">
<td><p>網路作業系統</p></td>
<td><ul>
<li><p>1 張網路介面卡 1 Gbps</p></li>
<li><p>Windows Server 2008 R2、Windows Server 2012 或</p>
<p>Windows Server 2012 R2</p></li>
</ul></td>
</tr>
</tbody>
</table>


  - .NET Framework 4.5 的完整版本。

  - Windows Identity Foundation。

  - Windows PowerShell 3.0。

一旦符合所有這些必要條件，就可以執行下列動作來設定監看員節點：

  - 在監看員節點電腦上安裝 Lync Server 2013 核心檔案。

  - 在監看員節點電腦上安裝 System Center Operations Manager 代理程式。

  - 執行 Watchernode.msi 可執行檔。

  - 使用 **CsWatcherNodeConfiguration** Cmdlet 設定監看員節點要使用的測試使用者。

