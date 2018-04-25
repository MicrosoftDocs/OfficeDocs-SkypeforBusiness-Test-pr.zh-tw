---
title: Set-CsTrunkConfiguration
TOCTitle: Set-CsTrunkConfiguration
ms:assetid: 18152388-68de-4a6b-b5a1-248534ecde72
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398238(v=OCS.15)
ms:contentKeyID: 49290223
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTrunkConfiguration

 

_**上次修改主題的時間：** 2015-02-27_

修改現有描述對等主幹實體 (例如服務提供者的公用交換電話網路 (PSTN) 閘道、IP 公用交換機 (PBX) 或工作階段邊界控制器 (SBC)) 的主幹組態。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsTrunkConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsTrunkConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-ConcentratedTopology <$true | $false>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Enable3pccRefer <$true | $false>] [-EnableBypass <$true | $false>] [-EnableFastFailoverTimer <$true | $false>] [-EnableLocationRestriction <$true | $false>] [-EnableMobileTrunkSupport <$true | $false>] [-EnableOnlineVoice <$true | $false>] [-EnablePIDFLOSupport <$true | $false>] [-EnableReferSupport <$true | $false>] [-EnableRTPLatching <$true | $false>] [-EnableSessionTimer <$true | $false>] [-EnableSignalBoost <$true | $false>] [-Force <SwitchParameter>] [-ForwardCallHistory <$true | $false>] [-ForwardPAI <$true | $false>] [-MaxEarlyDialogs <UInt32>] [-NetworkSiteID <String>] [-OutboundCallingNumberTranslationRulesList <PSListModifier>] [-OutboundTranslationRulesList <PSListModifier>] [-PstnUsages <PSListModifier>] [-RemovePlusFromUri <$true | $false>] [-RTCPActiveCalls <$true | $false>] [-RTCPCallsOnHold <$true | $false>] [-SipResponseCodeTranslationRulesList <PSListModifier>] [-SRTPMode <Required | Optional | NotSupported>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會使用 Identity site:Redmond 來修改主幹組態，以啟用媒體旁路。藉由將 $True 值指派給 EnableBypass 參數以啟用媒體旁路。此組態剩下的屬性將保留現有的值。

    Set-CsTrunkConfiguration -Identity site:Redmond -EnableBypass $True

## 範例 2

此範例會使用 Identity site:Redmond 來修改為主幹組態定義的外撥轉譯規則。請注意，我們實際上不會撥打電話至 **Set-CsTrunkConfiguration** Cmdlet 來進行此變更。使用 **Set-CsOutboundTranslationRule** Cmdlet 進行的變更將自動反映在 Identity 符合外撥轉譯規則之 Identity 的範圍部分的主幹組態中。

    Set-CsOutboundTranslationRule -Identity site:Redmond/OTR1 -Translation '$1'

## 範例 3

範例 3 將網站範圍定義之所有主幹組態的 SRTPMode 設定為 Optional。命令的第一部分為呼叫 **Get-CsTrunkConfiguration** Cmdlet，該 Cmdlet 會使用 Filter 參數擷取 Identity 開頭為 site: 的所有主幹組態，亦即在網站層級定義的所有主幹組態。組態的集合隨即便傳送到 **Set-CsTrunkConfiguration** Cmdlet，此 Cmdlet 會將每個組態的 SRTPMode 屬性設為 Optional。

    Get-CsTrunkConfiguration -Filter site:* | Set-CsTrunkConfiguration -SRTPMode "Optional"

## 範例 4

範例 4 會使用 Identity site:Redmond 來修改主幹組態，以啟用 PIDF-LO 支援。EnablePIDFLOSupport 參數預設為 False。在此範例中，我們已將該值設為 True 以啟用緊急電話的位置支援。您必須將 EnablePIDFLOSupport 設定為 True，以便位置資訊可以透過輸出路由應用程式傳送至主幹。

    Set-CsTrunkConfiguration -Identity site:Redmond -EnablePIDFLOSupport $True

## 詳細描述

使用此 Cmdlet 可修改適用於 PSTN 閘道實體的主幹組態。每個組態均含有對等主幹實體 (例如，服務提供者的 PSTN 閘道、IP-PBX 或 SBC) 的專屬設定。這些設定所設定的項目包括此主幹是否啟用媒體旁路、是否在特定情況下傳送即時傳輸控制通訊協定 (RTCP) 封包，以及是否需要安全即時通訊協定 (SRTP) 加密。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsTrunkConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsTrunkConfiguration"}

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
<td><p><em>ConcentratedTopology</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>此參數的值會決定是否有已知的媒體終端點。(舉例來說，PSTN 閘道就是已知的媒體終端點，其中媒體終端的 IP 與訊號終端相同)。如果主幹沒有已知的媒體終端點，請將此值設為 False。</p>
<p>預設值：True</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>描述主幹組態用途的字串。</p></td>
</tr>
<tr class="even">
<td><p><em>Enable3pccRefer</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>指出是否可以使用 3pcc 通訊協定來讓轉接的通話略過主控的網站。3pcc 亦稱為「第三方控制」，並且會在使用第三方來連接一對通話者時出現 (例如，操作員安排從人員 A 接到人員 B 的通話)。REFER 方法是標準 SIP 方法，它會指示受話者應使用發話者提供的資訊來連絡第三方。預設值為 False ($False)。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableBypass</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>此參數的值可決定是否啟用此主幹的媒體旁路。將這個值設為 True 以啟用旁路功能。請注意，為了使媒體旁路得以順利運作，PSTN 閘道、SBC 及 PBX 必須支援某些功能，包括：</p>
<p>- 能夠接收對 Invite 的分支回應。</p>
<p>- Lync Server 用戶端與媒體終端點必須能夠直接通訊，而不必經由中繼伺服器。</p>
<p>- 閘道子網路必須定義為位在與用戶端的子網路相同的網站，如果位在不同的網站，則網站必定無法由頻寬受限的 WAN 連結加以區別。</p>
<p>媒體旁路只能在下列情況下啟用：</p>
<p>- ConcentratedTopology 參數已設為 True</p>
<p>- EnableReferSupport 參數已設為 False 且 RTCPActiveCalls 和 RTCPCallsOnHold 已設為 False，或是 EnableReferSupport 已設為 True</p>
<p>請注意，如果 EnableBypass 為 True 且 EnableReferSupport 為 False，後續傳輸的旁路通話將成為非旁路通話。</p>
<p>為了讓特定主幹的媒體旁路能運作，媒體旁路必須全域啟用，上述之主幹的媒體旁路也必須啟用。使用 <strong>New-CsNetworkMediaBypassConfiguration</strong> Cmdlet 以全域啟用媒體旁路。</p>
<p>預設值：False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableFastFailoverTimer</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>若設為 True，當閘道未在 10 秒之內接聽外撥通話時，會將該通話路由到下一條可用的主幹；若已無可用的主幹，會自動將該通話掛斷。組織的網路速度與閘道回應速度若是很慢，可能會造成來電不必要地遭到掛斷。</p>
<p>預設值為 True。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableLocationRestriction</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>設為 True 時，會針對透過 SIP 主幹 (由指定之 SIP 主幹組態設定的集合所管理) 傳送的通話啟用以位置為主的語音路由。藉由以位置為主的語音路由，當路由傳送通話時，會同時將撥打電話的使用者及接聽電話的使用者納入考量。如果將此屬性設為 True (預設值為 False)，您也應該設定 NetworkSiteId 屬性。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableMobileTrunkSupport</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>定義服務提供者是否為行動裝置電信業者。</p>
<p>預設值：False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableOnlineVoice</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>指出 SIP 主幹是否支援線上語音。透過線上語音，使用者可以具有內部部署 Lync Server 帳戶，但其語音信箱是由 商務用 Skype Online 主控。預設值為 False ($False)。</p></td>
</tr>
<tr class="even">
<td><p><em>EnablePIDFLOSupport</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>定義是否要透過已定義的閘道傳送含目前狀態資訊資料格式位置物件 (PIDF-LO) 的緊急通話。如果要將緊急通話傳送到取得認證的緊急服務提供者，請將此參數設為 True (位置將隨通話一併傳送)。</p>
<p>預設值：False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableReferSupport</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>定義此主幹是否支援接收來自中繼伺服器的 Refer 要求。</p>
<p>媒體旁路只能在下列情況下啟用：</p>
<p>- ConcentratedTopology 參數已設為 True</p>
<p>- EnableReferSupport 參數已設為 False 且 RTCPActiveCalls 和 RTCPCallsOnHold 已設為 False，或是 EnableReferSupport 已設為 True</p>
<p>請注意，如果 EnableBypass 為 True 且 EnableReferSupport 為 False，後續傳輸的旁路通話將成為非旁路通話。</p>
<p>預設值：True</p></td>
</tr>
<tr class="even">
<td><p><em>EnableRTPLatching</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>指出 SIP 主幹是否支援 RTP 鎖定。RTP 鎖定是可以透過 NAT (網路位址轉譯器) 裝置或防火牆進行 RTP/RTCP 連線的技術。預設值為 False ($False)。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableSessionTimer</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>指定是否啟用工作階段計時器。工作階段計時器用於決定特定的工作階段是否仍為使用中。</p>
<p>請注意，即使此參數已設為 False，倘若遠端連線啟用工作階段計時器，仍可套用工作階段計時器。在這種情況下，中繼伺服器將從遠端實體回覆工作階段計時器探查。</p>
<p>預設值：False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableSignalBoost</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>此參數設為 True 時，服務提供者的 PSTN 閘道、IP-PBX 或 SBC 將增加傳送到中繼伺服器或 Lync Server 用戶端之語音串流的音訊音量。如果將此值設為 False，音訊音量會在中繼伺服器 (非旁路通話) 或在 Lync Server 用戶端 (旁路通話) 中增強。</p>
<p>預設值：False</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="even">
<td><p><em>ForwardCallHistory</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>指出是否透過主幹轉送通話記錄資訊。預設值為 False ($False)。</p></td>
</tr>
<tr class="odd">
<td><p><em>ForwardPAI</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>指出 P-Asserted-Identity (PAI) 標頭是否要隨通話轉接。PAI 標頭可用於驗證來電者的身分識別。預設值為 False ($False)。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>XdsIdentity</p></td>
<td><p>包含主幹組態範圍的唯一識別碼。主幹組態可存在於全域範圍、網站範圍或 PSTN 閘道服務的服務範圍上。例如，site:Redmond (網站) 或 PstnGateway:Redmond.litwareinc.com (服務)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>TrunkConfiguration</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p>
<p>此參數必須有 Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration 類型的物件，其可藉由呼叫 <strong>Get-CsTrunkConfiguration</strong> Cmdlet 來加以擷取。</p></td>
</tr>
<tr class="even">
<td><p><em>MaxEarlyDialogs</em></p></td>
<td><p>選用</p></td>
<td><p>UInt32</p></td>
<td><p>服務提供者的 PSTN 閘道、IP-PBX 或 SBC 對其傳送到中繼伺服器的 Invite，可接收的分支回應數上限。</p>
<p>預設值：20</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkSiteID</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>與主幹組態設定集合相關聯之網路站台的 ID。如果 EnableLocationRestriction 屬性設為 True，則會使用針對特定網站所做的設定來管理通過此主幹傳送之以位置為主的語音路由。藉由使用下列命令可擷取網路的網站 ID：</p>
<p>Get-CsNetworkSite | Select NetworkSiteID</p></td>
</tr>
<tr class="even">
<td><p><em>OutboundCallingNumberTranslationRulesList</em></p></td>
<td><p>選用</p></td>
<td><p>PSListModifier</p></td>
<td><p>指派給主幹的撥出電話號碼轉譯規則集合。您可以執行下列命令來擷取可用規則的資訊。</p>
<p>Get-CsOutboundCallingNumberTranslationRule</p></td>
</tr>
<tr class="odd">
<td><p><em>OutboundTranslationRulesList</em></p></td>
<td><p>選用</p></td>
<td><p>PSListModifier</p></td>
<td><p>電話號碼轉譯規則的集合，這些規則會套用到輸出路由所處理的電話 (亦即路由到 PBX 或 PSTN 目的地的電話)。</p>
<p>雖然可使用此 Cmdlet 直接修改清單與這些規則，但我們仍建議您使用 <strong>Set-CsOutboundTranslationRule</strong> Cmdlet 修改外撥轉譯規則。<strong>Set-CsOutboundTranslationRule</strong> Cmdlet 將修改規則，這些修改會自動反映在主幹組態中。若要藉由新增外撥轉譯規則來修改主幹組態，請呼叫 <strong>New-CsOutboundTranslationRule</strong> Cmdlet；新規則將新增到含符合範圍的主幹組態。</p></td>
</tr>
<tr class="even">
<td><p><em>PstnUsages</em></p></td>
<td><p>選用</p></td>
<td><p>PSListModifier</p></td>
<td><p>指派給主幹的 PSTN 使用方式集合。您可以執行下列命令來擷取可用使用方式的資訊。</p>
<p>Get-CsPstnUsage</p></td>
</tr>
<tr class="odd">
<td><p><em>RemovePlusFromUri</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>將此參數設為 True 將造成中繼伺服器先移除統一資源識別元 (URI) 前置的加號 (+)，再將這些 URI 傳送到服務提供者。</p>
<p>預設值：False</p></td>
</tr>
<tr class="even">
<td><p><em>RTCPActiveCalls</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>此參數可決定目前通話是否可從服務提供者的 PSTN 閘道、IP-PBX 或 SBC 傳送 RTCP 封包。此處的目前通話指的是至少允許媒體流向一個方向的通話。如果 RTCPActiveCalls 設為 True，當中繼伺服器或 Lync Server 用戶端未在 30 秒內收到 RTCP 封包時，便能終止通話。</p>
<p>請注意，在 Lync Server 元素中停用目前通話的 RTCP 媒體接收檢查也會移除重要的對等中斷偵測防護，因此若非絕對必要，請勿採用。</p>
<p>預設值：True</p></td>
</tr>
<tr class="odd">
<td><p><em>RTCPCallsOnHold</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>此參數會決定保留中、且預期將無任何媒體封包流向任一方向之通話的 RTCP 封包是否繼續在主幹中傳送。如果已在 Lync Server 用戶端或主幹啟用等候音樂，此通話將被視為目前通話，並且會忽略此內容。在上述情況下，請使用 RTCPActiveCalls 參數。</p>
<p>請注意，在 Lync Server 元素中停用目前通話的 RTCP 媒體接收檢查也會移除重要的對等中斷偵測防護，因此若非絕對必要，請勿採用。</p>
<p>預設值：True</p></td>
</tr>
<tr class="even">
<td><p><em>SipResponseCodeTranslationRulesList</em></p></td>
<td><p>選用</p></td>
<td><p>PSListModifier</p></td>
<td><p>SIP 回應碼轉譯規則清單，這些規則會套用在從服務提供者之 PSTN 閘道、IP-PBX 或 SBC 接收到的回應碼。這些規則可讓系統管理員將透過主幹接收到的 SIP 回應碼值 (介於 400 到 699 之間) 對應到和 Lync Server 比較一致的新值。</p>
<p>儘管您可以使用這個 Cmdlet 建立此清單和對應的規則，不過我們還是建議您呼叫 <strong>New-CsSipResponseCodeTranslationRule</strong> Cmdlet 來建立 SIP 回應碼轉譯規則。這個 Cmdlet 除了能建立規則之外，還能將規則指派給範圍相符的主幹組態。</p></td>
</tr>
<tr class="odd">
<td><p><em>SRTPMode</em></p></td>
<td><p>選用</p></td>
<td><p>SRTPMode</p></td>
<td><p>此參數的值會決定 SRTP 的支援層級，以保護中繼伺服器和服務提供者之 PSTN 閘道、IP-PBX 或 SBC 之間的媒體流量。若是媒體旁路的情況，此值必須與媒體組態中的 EncryptionLevel 設定相容。媒體組態必須使用 <strong>New-CsMediaConfiguration</strong> Cmdlet 和 <strong>Set-CsMediaConfiguration</strong> Cmdlet 來加以設定。</p>
<p>有效值：</p>
<p>- Required：必須使用 SRTP 加密。</p>
<p>- Optional：如果服務提供者支援 SRTP，則使用 SRTP。</p>
<p>- NotSupported:不支援 SRTP 加密，因此不會使用此加密。</p>
<p>注意：只有閘道設定為使用傳輸層安全性 (TLS) 時，才能使用 SRTPMode。如果將閘道設定為在傳輸時使用傳輸控制通訊協定 (TCP)，系統會從內部將 SRTPMode 設為 NotSupported。</p>
<p>預設值：必要</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration 物件。接受主幹組態物件管線傳送的輸入。

## 傳回類型

此 Cmdlet 不會傳回值，而會修改 Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration 類型的物件。

## 請參閱

#### 其他資源

[New-CsTrunkConfiguration](new-cstrunkconfiguration.md)  
[Remove-CsTrunkConfiguration](remove-cstrunkconfiguration.md)  
[Get-CsTrunkConfiguration](get-cstrunkconfiguration.md)  
[Test-CsTrunkConfiguration](test-cstrunkconfiguration.md)  
[New-CsOutboundTranslationRule](new-csoutboundtranslationrule.md)  
[Set-CsOutboundTranslationRule](set-csoutboundtranslationrule.md)

