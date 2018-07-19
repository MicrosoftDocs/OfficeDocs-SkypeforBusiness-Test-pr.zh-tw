---
title: 在 Lync Server 2013 中修改 SIP 主幹組態設定
TOCTitle: 在 Lync Server 2013 中修改 SIP 主幹組態設定
ms:assetid: 7d68b09c-9ea0-43bd-997c-df887869d607
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688104(v=OCS.15)
ms:contentKeyID: 49890136
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中修改 SIP 主幹組態設定

 

_**上次修改主題的時間：** 2015-03-09_

SIP 主幹組態設定定義了中繼伺服器與公用交換電話網路 (PSTN) 閘道、IP 公用交換機 (PBX) 或是服務提供者處的工作階段界限控制器 (SBC) 之間的關係和功能。這些設定可指定：

  - 是否應在主幹上啟用媒體旁路。

  - 傳送即時傳輸控制通訊協定 (RTCP) 封包的條件。

  - 各個主幹是否需要安全即時通訊協定 (SRTP) 加密。

當您安裝 Microsoft Lync Server 2013 時，系統會為您建立一組全域 SIP 主幹組態設定集合。此外，系統管理員可建立網站範圍或服務範圍 (僅針對 PSTN 閘道服務) 的自訂設定集合。往後使用 Lync Server 控制台或 Windows PowerShell 即可修改任何這些集合。

使用 Lync Server 控制台修改 SIP 主幹組態設定時，下列選項可供使用：


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
<td><p>身分識別</p></td>
<td><p>集合的唯一識別碼。此內容為唯讀；您無法變更主幹組態設定集合的身分識別。</p></td>
</tr>
<tr class="even">
<td><p>說明</p></td>
<td><p>說明</p></td>
<td><p>讓系統管理員儲存設定的其他資訊 (例如，主幹組態的用途)。</p></td>
</tr>
<tr class="odd">
<td><p>支援的最大早期對話</p></td>
<td><p>MaxEarlyDialogs</p></td>
<td><p>表示服務供應商的 PSTN 閘道、IP-PBX 或 SBC 可接收其傳送到中繼伺服器之對 Invite 的分支回應數上限。</p></td>
</tr>
<tr class="even">
<td><p>加密支援等級</p></td>
<td><p>SRTPMode</p></td>
<td><p>指出將 Mediation Server 與服務提供者的 PSTN 閘道、IP-PBX 或 SBC 之間的媒體流量加以保護的支援等級。若是媒體旁路的情況，此值必須與媒體組態中的 EncryptionLevel 設定相容。媒體組態必須使用 <a href="https://docs.microsoft.com/en-us/powershell/module/skype/New-CsMediaConfiguration">New-CsMediaConfiguration</a> 和 <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsMediaConfiguration">Set-CsMediaConfiguration</a> Cmdlet 加以設定。</p>
<p>允許的值為：</p>
<ul>
<li><p>Required：必須使用 SRTP 加密。</p></li>
<li><p>Optional：如果閘道支援，即會使用 SRTP。</p></li>
<li><p>NotSupported：不支援 SRTP 加密，因此不會使用此加密。</p></li>
</ul>
<p>只有閘道設定為使用傳輸層安全性 (TLS) 時，才能使用 SRTPMode。如果將閘道設定為在傳輸時使用傳輸控制通訊協定 (TCP)，系統會從內部將 SRTPMode 設為 NotSupported。</p></td>
</tr>
<tr class="odd">
<td><p>轉接支援</p></td>
<td><p>Enable3pccRefer</p>
<p>EnableReferSupport</p></td>
<td><p>如果設定為 [啟用傳送轉接至閘道]，表示主幹支援接收 Mediation Server 的轉接要求。</p>
<p>如果設定為 [啟用使用第三方通話控制的轉接]，表示可使用 3pcc 通訊協定允許轉接的電話避開託管的網站。3pcc 也稱為「第三方控制」，會在使用第三方連接一組來電者 (例如，接線員將 A 人的電話接通到 B 人) 時發生。</p></td>
</tr>
<tr class="even">
<td><p>啟用媒體旁路</p></td>
<td><p>EnableBypass</p></td>
<td><p>指出是否啟用此主幹的媒體旁路。只有也啟用 [集中式媒體處理] 時，才可啟用媒體旁路。</p></td>
</tr>
<tr class="odd">
<td><p>集中式媒體處理</p></td>
<td><p>ConcentratedTopology</p></td>
<td><p>指出是否有已知的媒體終端點。(舉例來說，PSTN 閘道就是已知的媒體終端點，其中媒體終端的 IP 與訊號終端相同)。</p></td>
</tr>
<tr class="even">
<td><p>啟用 RTP 栓</p></td>
<td><p>EnableRTPLatching</p></td>
<td><p>指出 SIP 主幹是否支援 RTP 栓。RTP 栓是能夠透過 NAT (網路位址轉譯器) 裝置或防火牆啟用 RTP/RTCP 連線的技術。</p></td>
</tr>
<tr class="odd">
<td><p>啟用來電轉接記錄</p></td>
<td><p>ForwardCallHistory</p></td>
<td><p>指出是否將透過主幹轉送來電記錄資訊。</p></td>
</tr>
<tr class="even">
<td><p>啟用轉送 P-Asserted-Identity 資料</p></td>
<td><p>ForwardPAI</p></td>
<td><p>指出是否隨來電轉送 P-Asserted-Identity (PAI) 標頭。PAI 標頭可供確認來電者的身分。</p></td>
</tr>
<tr class="odd">
<td><p>啟用輸出路由容錯移轉計時器</p></td>
<td><p>EnableFastFailoverTimer</p></td>
<td><p>指出閘道未在 10 秒內應答的撥出電話是否將路由到下一個可用的主幹；如果沒有其他主幹，則將自動放棄來電。在網路和閘道回應緩慢的組織中，這可能導致非必要放棄來電。</p></td>
</tr>
<tr class="even">
<td><p>相關 PSTN 使用</p></td>
<td><p>PSTNUsages</p></td>
<td><p>指派給主幹的 PSTN 使用集合，</p></td>
</tr>
<tr class="odd">
<td><p>要測試的轉譯號碼</p></td>
<td><p>N/A</p></td>
<td><p>可用來臨時測試主幹組態設定的電話號碼。</p></td>
</tr>
<tr class="even">
<td><p>相關轉譯規則</p></td>
<td><p>OutboundTranslationRulesList</p></td>
<td><p>電話號碼轉譯規則的集合，這些規則會套用到輸出路由所處理的電話 (亦即路由到 PBX 或 PSTN 目的地的電話)。</p></td>
</tr>
<tr class="odd">
<td><p>通話號碼轉譯規則</p></td>
<td><p>OutboundCallingNumberTranslationRulesList</p></td>
<td><p>指派給主幹的撥出通話號碼轉譯規則集合。</p></td>
</tr>
<tr class="even">
<td><p>要測試的電話號碼</p></td>
<td><p>N/A</p></td>
<td><p>可用來臨時測試轉譯規則的電話號碼。</p></td>
</tr>
<tr class="odd">
<td><p>發話方號碼</p></td>
<td><p>N/A</p></td>
<td><p>指出要測試的電話號碼是來電者的電話號碼。</p></td>
</tr>
<tr class="even">
<td><p>受話方號碼</p></td>
<td><p>N/A</p></td>
<td><p>指出要測試的電話號碼是接聽來電者的電話號碼。</p></td>
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
<td>Lync Server CsTrunkConfiguration Cmdlet 支援 Lync Server 控制台中未顯示的其他內容。如需詳細資訊，請參閱 <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsTrunkConfiguration">set-cstrunkconfiguration</a> Cmdlet 的說明主題。</td>
</tr>
</tbody>
</table>


## 使用 Lync Server 控制台修改 SIP 主幹組態設定

1.  在 Lync Server 控制台中。按一下 \[語音路由\]，然後按一下 \[主幹組態\]。

2.  在 \[主幹組態\] 索引標籤上，連按兩下要修改的主幹組態設定。請注意，一次只能編輯一個集合的設定。如果要針對多個集合進行相同的變更，請改用 Windows PowerShell。

3.  在 \[編輯主幹組態\] 對話方塊中，進行適當的選取，然後按一下 \[確定\]。

4.  集合的 \[狀態\] 內容將更新為 \[未認可\]。若要認可變更，並刪除集合，請按一下 \[認可\]，然後按一下 \[全部認可\]。

5.  在 \[未認可的語音組態設定\] 對話方塊中，按一下 \[確定\]。

6.  在 \[Microsoft Lync Server 2013 控制台\] 對話方塊中，按一下 \[確定\]。

