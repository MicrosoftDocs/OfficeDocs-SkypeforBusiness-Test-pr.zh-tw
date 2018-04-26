---
title: 在 Lync Server 2013 中建立新的主幹組態設定集合
TOCTitle: 在 Lync Server 2013 中建立新的主幹組態設定集合
ms:assetid: 4ebd710c-38cd-4cff-9a45-df029d424580
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688054(v=OCS.15)
ms:contentKeyID: 49890061
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建立新的主幹組態設定集合

 

_**上次修改主題的時間：** 2015-03-09_

SIP 主幹組態設定定義中繼伺服器與公用交換電話網路 (PSTN) 閘道、IP 公用交換機 (PBX) 或工作階段界限控制器 (SBC) 之間的關係和功能。這些設定會依指定執行工作：

  - 主幹是否應啟用媒體旁路。

  - 傳送即時傳輸控制通訊協定 (RTCP) 封包的情況。

  - 各主幹是否需要安全即時通訊協定 (SRTP) 加密。

當您安裝 Microsoft Lync Server 2013 時，會為您建立 SIP 主幹組態設定的全域集合。此外，系統管理員可以在網站範圍或服務範圍 (僅限 PSTN 閘道服務) 建立自訂設定集合。

使用 Lync Server 控制台建立 SIP 主幹組態設定時，您可以使用下列選項：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>UI 設定</th>
<th>PowerShell 參數</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>名稱</p></td>
<td><p>Identity</p></td>
<td><p>集合的唯一識別碼。此為唯讀屬性，您無法變更主幹組態設定集合的 Identity。</p></td>
</tr>
<tr class="even">
<td><p>說明</p></td>
<td><p>說明</p></td>
<td><p>為系統管理員提供儲存設定相關資訊 (例如，主幹組態的用途) 的方法。</p></td>
</tr>
<tr class="odd">
<td><p>支援的最大早期對話</p></td>
<td><p>MaxEarlyDialogs</p></td>
<td><p>服務提供者的 PSTN 閘道、IP-PBX 或 SBC 對其傳送到中繼伺服器的 Invite，可接收的分支回應數上限。</p></td>
</tr>
<tr class="even">
<td><p>加密支援等級</p></td>
<td><p>SRTPMode</p></td>
<td><p>指出支援等級，以保護中繼伺服器和服務提供者之 PSTN 閘道、IP-PBX 或 SBC 之間的媒體流量。若是媒體旁路的情況，此值必須與媒體組態中的 EncryptionLevel 設定相容。媒體組態會使用 <a href="new-csmediaconfiguration.md">New-CsMediaConfiguration</a> 和 <a href="set-csmediaconfiguration.md">Set-CsMediaConfiguration</a> Cmdlet 來設定。</p>
<p>允許的值為：</p>
<ul>
<li><p>Required：必須使用 SRTP 加密。</p></li>
<li><p>Optional：如果閘道支援，即會使用 SRTP。</p></li>
<li><p>Not Supported：不支援 SRTP 加密，因此不會使用此加密。</p></li>
</ul>
<p>只有閘道設定為使用傳輸層安全性 (TLS) 時，才能使用 SRTPMode。如果將閘道設定為在傳輸時使用傳輸控制通訊協定 (TCP)，系統會從內部將 SRTPMode 設為 Not Supported。</p></td>
</tr>
<tr class="odd">
<td><p>轉接支援</p></td>
<td><p>Enable3pccRefer</p>
<p>EnableReferSupport</p></td>
<td><p>如果設定為 <strong>[啟用傳送轉接至閘道]</strong>，表示主幹支援接收來自中繼伺服器的 Refer 要求。</p>
<p>如果設定為 <strong>[使用協力廠商撥號控制來啟用轉接]</strong>，表示可以使用 3pcc 通訊協定允許轉接通話略過主控網站。3pcc 也稱為「第三方控制」，當使用第三方來連接一組來電者時 (例如，由接線員撥打從 A 到 B 的電話)，就會發生此情況。</p></td>
</tr>
<tr class="even">
<td><p>啟用媒體旁路</p></td>
<td><p>EnableBypass</p></td>
<td><p>表示此主幹是否啟用媒體旁路。只有在也啟用 <strong>[集中式媒體處理]</strong> 時，才能啟用媒體旁路。</p></td>
</tr>
<tr class="odd">
<td><p>集中式媒體處理</p></td>
<td><p>ConcentratedTopology</p></td>
<td><p>指出是否有已知的媒體終端點 (已知的媒體終端點範例是 PSTN 閘道，其媒體終端的 IP 與訊號終端相同)。</p></td>
</tr>
<tr class="even">
<td><p>啟用 RTP 栓</p></td>
<td><p>EnableRTPLatching</p></td>
<td><p>指出 SIP 主幹是否支援 RTP 栓。RTP 栓是一種技術，可讓 RTP/RTCP 透過 NAT (網路位址轉譯器) 裝置或防火牆連線。</p></td>
</tr>
<tr class="odd">
<td><p>啟用轉接來電記錄</p></td>
<td><p>ForwardCallHistory</p></td>
<td><p>指出是否將透過主幹來轉接來電記錄資訊。</p></td>
</tr>
<tr class="even">
<td><p>啟用轉寄 P-Asserted-Identity 資料</p></td>
<td><p>ForwardPAI</p></td>
<td><p>指出 P-Asserted-Identity (PAI) 標頭是否會和通話一起轉寄。PAI 標頭提供確認來電者身分識別的方法。</p></td>
</tr>
<tr class="odd">
<td><p>啟用輸出路由容錯移轉計時器</p></td>
<td><p>EnableFastFailoverTimer</p></td>
<td><p>指出閘道未在 10 秒內接聽的撥出電話將會被路由傳送到下一個可用的主幹；如果沒有其他主幹，就會自動捨棄此電話。在網路和閘道回應速度緩慢的組織中，這可能會造成電話平白遭到捨棄。</p></td>
</tr>
<tr class="even">
<td><p>關聯的 PSTN 使用方式</p></td>
<td><p>PSTNUsages</p></td>
<td><p>指派給主幹的 PSTN 使用方式集合。</p></td>
</tr>
<tr class="odd">
<td><p>要測試的轉譯號碼</p></td>
<td><p>N/A</p></td>
<td><p>可用於進行主幹組態設定臨機測試的電話號碼。</p></td>
</tr>
<tr class="even">
<td><p>關聯的轉譯規則</p></td>
<td><p>OutboundTranslationRulesList</p></td>
<td><p>套用到由「輸出路由」處理的電話 (路由傳送到 PBX 或 PSTN 目的地的電話) 的電話號碼轉譯規則集合。</p></td>
</tr>
<tr class="odd">
<td><p>撥打號碼轉譯規則</p></td>
<td><p>OutboundCallingNumberTranslationRulesList</p></td>
<td><p>指派給主幹的撥出電話號碼轉譯規則集合。</p></td>
</tr>
<tr class="even">
<td><p>測試的電話號碼</p></td>
<td><p>N/A</p></td>
<td><p>可用於進行轉譯規則臨機測試的電話號碼。</p></td>
</tr>
<tr class="odd">
<td><p>撥打號碼</p></td>
<td><p>N/A</p></td>
<td><p>指出要測試的電話號碼是來電者的電話號碼。</p></td>
</tr>
<tr class="even">
<td><p>撥打的號碼</p></td>
<td><p>N/A</p></td>
<td><p>指出要測試的電話號碼是受話者的電話號碼。</p></td>
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
<td>Lync Server CsTrunkConfiguration Cmdlet 支援 Lync Server 控制台中未顯示的其他屬性。如需詳細資訊，請參閱 <a href="new-cstrunkconfiguration.md">New-CsTrunkConfiguration</a> Cmdlet 的說明主題。</td>
</tr>
</tbody>
</table>


## 使用 Lync Server 控制台建立新的主幹組態設定

1.  在 Lync Server 控制台中，依序按一下 **\[語音路由\]** 和 **\[主幹組態\]**。

2.  在 **\[主幹組態\]** 索引標籤上，按一下 **\[新增\]**，然後按一下 **\[站台主幹\]** 以建立在網站範圍的新設定，或按一下 **\[集區主幹\]** 以建立在服務範圍的新設定。

3.  在 **\[選取站台\]** 或 **\[選取服務\]** 對話方塊中 (顯示的對話方塊會視您是建立網站範圍或服務範圍的設定而定)，選取新組態設定的位置，然後按一下 **\[確定\]**。如果對話方塊是空白的，表示沒有空間可建立新設定；例如，如果 **\[選取站台\]** 對話方塊是空白的，表示您所有的網站都已被指派主幹組態設定集合，且每個網站 (及每項服務) 都只能主控一個此類集合。在這種情況下，您可以刪除現有的集合後再建立新集合，或只是修改現有的集合。

4.  在 **\[新主幹組態\]** 對話方塊中，選取適當的選項，然後按一下 **\[確定\]**。

5.  集合的 **\[State\]** 屬性將會更新為 **\[未認可\]**。如果要認可變更，並刪除集合，請依序按一下 **\[認可\]** 和 **\[全部認可\]**。

6.  在 **\[未認可的語音組態設定\]** 對話方塊中，按一下 **\[確定\]**。

7.  在 **\[Microsoft Lync Server 2013 控制台\]** 對話方塊中，按一下 **\[確定\]**。

