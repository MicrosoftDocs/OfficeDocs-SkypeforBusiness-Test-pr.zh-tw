---
title: New-CsVoicePolicy
TOCTitle: New-CsVoicePolicy
ms:assetid: 3852de89-a604-437a-9fdf-3597b88ce13d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425856(v=OCS.15)
ms:contentKeyID: 49290601
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsVoicePolicy

 

_**上次修改主題的時間：** 2015-03-09_

建立新的語音原則。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsVoicePolicy -Identity <XdsIdentity> [-AllowCallForwarding <$true | $false>] [-AllowPSTNReRouting <$true | $false>] [-AllowSimulRing <$true | $false>] [-CallForwardingSimulRingUsageType <VoicePolicyUsage | InternalOnly | CustomUsage>] [-Confirm [<SwitchParameter>]] [-CustomCallForwardingSimulRingUsages <PSListModifier>] [-Description <String>] [-EnableBWPolicyOverride <$true | $false>] [-EnableCallPark <$true | $false>] [-EnableCallTransfer <$true | $false>] [-EnableDelegation <$true | $false>] [-EnableMaliciousCallTracing <$true | $false>] [-EnableTeamCall <$true | $false>] [-EnableVoicemailEscapeTimer <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Name <String>] [-PreventPSTNTollBypass <$true | $false>] [-PstnUsages <PSListModifier>] [-PSTNVoicemailEscapeTimer <Int64>] [-Tenant <Guid>] [-VoiceDeploymentMode <OnPrem | Online | OnlineBasic | OnPremOnlineHybrid>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會以預設設定建立 Identity 為 UserVoicePolicy1 的新個別使用者語音原則。

    New-CsVoicePolicy -Identity UserVoicePolicy1

## 範例 2

此範例會建立 Identity 為 UserVoicePolicy2 的新個別使用者語音原則，並將 AllowSimulRing 屬性設為 False，表示指派到此原則的任何使用者都未啟用同時響鈴，而此功能決定是否可設定每當使用者的辦公室電話響起時，第二支電話 (例如行動電話) 也響起。此命令也會將 "Local" 新增到 PSTN 使用方式的清單，此清單會將這個語音原則與也使用 Local PSTN 使用方式的語音路由產生關聯(請注意，未明確指定 Identity 參數。Identity 參數是位置參數，因此如果將識別值放在參數清單的開頭，則不需要明確指出它是 Identity)。

    New-CsVoicePolicy UserVoicePolicy2 -AllowSimulRing $false -PstnUsages @{add = "Local"}

## 範例 3

此範例會為網站 Redmond 建立新的語音原則，並將組織已定義的所有 PSTN 使用方式套用至此原則。此範例的第一行會呼叫 **Get-CsPstnUsage** Cmdlet，以擷取一組組織通用的 PSTN 使用方式，並儲存在 $a 變數中。第二行則會呼叫 **New-CsVoicePolicy** Cmdlet，以為網站 Redmond 建立新的語音原則。系統會將值傳遞到 PstnUsages 參數，將 PSTN 使用方式通用集內包含的清單新增到此原則中。請注意新增值的語法：$a.Usage。這是指 PSTN 使用方式設定的 Usage 屬性，含有 PSTN 使用方式的清單。

    $a = Get-CsPstnUsage
    New-CsVoicePolicy site:Redmond -PstnUsages @{add = $a.Usage}

## 詳細描述

此 Cmdlet 會建立新的語音原則。語音原則可用來管理 Enterprise Voice 相關功能，例如同時響鈴 (每次有人撥打到您的辦公室電話時，能夠讓第二支電話響起) 和來電轉接。此 Cmdlet 所建立的原則會決定是否啟用或停用許多功能。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsVoicePolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsVoicePolicy"}

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
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>XdsIdentity</p></td>
<td><p>指定原則的範圍或名稱的唯一識別碼。此Cmdlet 的有效值為 site:&lt;網站名稱&gt; (其中 &lt;網站名稱&gt; 是指要套用此原則的 Lync Server 網站名稱，例如 site:Redmond)，以及指定個別使用者原則的字串，例如 RedmondVoicePolicy。全域原則預設即已存在。</p></td>
</tr>
<tr class="even">
<td><p><em>AllowCallForwarding</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>如果此參數設為 True，則無法轉接來電。如果此參數設為 False，則無法轉接來電。</p>
<p>預設值：True</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowPSTNReRouting</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>如果此參數設為 True 時，當集區或 WAN 無法使用時，對位在另一集區內部號碼撥號的電話會透過公用交換電話網路 (PSTN) 路由。</p>
<p>預設值：True</p></td>
</tr>
<tr class="even">
<td><p><em>AllowSimulRing</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>同時響鈴為撥打單一號碼時允許多個電話響鈴的功能。將此參數設為 True 會啟用此功能。如果此參數設為 False，則無法對指派至此原則的任何使用者設定同時響鈴。</p>
<p>預設值：True</p></td>
</tr>
<tr class="odd">
<td><p><em>CallForwardingSimulRingUsageType</em></p></td>
<td><p>選用</p></td>
<td><p>CallForwardingSimulRingUsageType</p></td>
<td><p>為系統管理員提供用來管理來電轉接及同時響鈴的方式。允許的值為：</p>
<p>* VoicePolicyUsage – 預設語音原則使用方式可用來管理所有通話的來電轉接及同時響鈴。此為預設值。</p>
<p>* InternalOnly – 來電轉接及同時響鈴限制為由一位 Lync 使用者撥打給另一位的通話。</p>
<p>* CustomUsage – 自訂的 PSTN 使用方式將會用來管理來電轉接及同時響鈴。此使用方式必須用 CustomCallForwardingSimulRingUsages 參數來指定。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>CustomCallForwardingSimulRingUsages</em></p></td>
<td><p>選用</p></td>
<td><p>PSListModifier</p></td>
<td><p>用來管理來電轉接及同時響鈴的自訂 PSTN 使用方式。若要新增自訂使用方式至語音原則，請使用類似下列的語法：</p>
<p>-CustomCallForwardingSimulRingUsages @{Add=&quot;RedmondPstnUsage&quot;}</p>
<p>若要移除自訂使用方式，請使用下列語法：</p>
<p>-CustomCallForwardingSimulRingUsages @{Remove=&quot;RedmondPstnUsage&quot;}</p>
<p>請注意，使用方式必須存在，才能與 CustomCallForwardingSimulRingUsages 參數搭配使用。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>語音原則的描述。</p>
<p>最大長度：1040 個字元。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableBWPolicyOverride</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>可以設定原則來管理網路設定，包括限制頻寬。將此參數設為 True 將允許覆寫這些原則。換句話說，如果此參數設為 True，則不會進行頻寬檢查，無論通話許可控制 (CAC) 的設定為何，來電都會通過。</p>
<p>預設值：False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableCallPark</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>通話駐留應用程式 允許保留特定號碼範圍內某個號碼的來電，稍後再擷取。將此參數設為 True 會啟用此應用程式。如果此參數設為 False，則指派至此原則的使用者無法保留已撥到電話號碼的來電。</p>
<p>預設值：False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableCallTransfer</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>決定來電是否可以轉接至另一個號碼。如果此參數設為 True，則可以轉接來電；如果此參數設為 False，則無法轉接來電。</p>
<p>預設值：True</p></td>
</tr>
<tr class="even">
<td><p><em>EnableDelegation</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>通話委派允許使用者接聽其他使用者的來電，或代表其他使用者撥打電話。例如，經理可以設定通話委派，讓所有來電同時在經理的電話和管理員的電話上響起。將此參數設為 True，可讓具有此原則的使用者設定通話委派。將此參數設為 False 會停用通話委派。</p>
<p>預設值：True</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableMaliciousCallTracing</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>惡意來電追蹤是一種標準，可隨時追蹤使用者指定為惡意的來電。即使已封鎖來電者識別碼，仍然可以追蹤這些來電。僅限適當的授權者才可追蹤，使用者無法使用追蹤。將此屬性設為 True，允許在惡意來電上設定追蹤。</p>
<p>預設值：False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableTeamCall</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>小組通話可讓使用者指定一組其他使用者，當撥打該使用者的號碼時，這一組使用者的電話會響起。在小組中此功能很有用，例如，小組的任何人都可以接聽客戶來電。將此參數設為 True 會啟用此功能。</p>
<p>預設值：True</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableVoicemailEscapeTimer</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>此參數設為 True 時，撥打至未接聽之行動裝置的通話會路由至組織的語音信箱，而不是行動裝置提供者的語音信箱。如果「太快」接聽通話 (亦即，在經過為 PSTNVoicemailEscapeTimer 屬性設定的值之前)，將會假設行動裝置無法使用，而將通話路由至組織的語音信箱。</p>
<p>預設值為 False。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>描述此原則的可顯示名稱。</p>
<p>預設值：DefaultPolicy</p></td>
</tr>
<tr class="odd">
<td><p><em>PreventPSTNTollBypass</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>PSTN 費用通常稱為長途電話費。組織可以實作 Voice over Internet Protocol (VoIP) 解決方案，讓分公司透過網路電話來聯繫，有時就能節省這些電話費。將此參數設為 True 會透過 PSTN 撥打電話且必須付費，而非經由網路而節省電話費。</p>
<p>預設值：False</p></td>
</tr>
<tr class="even">
<td><p><em>PstnUsages</em></p></td>
<td><p>選用</p></td>
<td><p>PSListModifier</p></td>
<td><p>此原則可用的 PSTN 使用方式清單。PSTN 使用方式將語音原則繫結至電話路由。</p>
<p>任何字串值皆可放置在清單中，只要該值存在於 PSTN 使用方式的目前全域清單中(不允許重複字串；所有字串必須是唯一的)。您可以呼叫 <strong>Get-CsPstnUsage</strong> Cmdlet 來擷取 PSTN 使用方式清單。</p>
<p>此清單預設為空白。如果您不提供此參數的值，則會收到警告訊息表示被授予這個原則的使用者將無法撥打輸出 PSTN 通話。</p></td>
</tr>
<tr class="odd">
<td><p><em>PSTNVoicemailEscapeTimer</em></p></td>
<td><p>選用</p></td>
<td><p>Int64</p></td>
<td><p>用來判斷是否「太快」接聽電話的時間量 (以毫秒為單位)。如果在此時間間隔內收到回應，Lync Server 會假設行動裝置無法使用，並自動將通話切換至組織的語音信箱。如果在達到此時間間隔之前沒有收到任何回應，則可繼續進行通話。預設值為 1500 毫秒。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>Guid</p></td>
<td><p>要建立新語音原則之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行下列命令傳回每個租用的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
<tr class="odd">
<td><p><em>VoiceDeploymentMode</em></p></td>
<td><p>選用</p></td>
<td><p>VoiceDeploymentMode</p></td>
<td><p>允許的值為：</p>
<p>* OnPrem</p>
<p>* Online</p>
<p>* OnlineBasic</p>
<p>* OnPremOnlineHybrid</p>
<p>預設值為 OnPrem。</p></td>
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

無。

## 傳回類型

此 Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Voice.VoicePolicy 物件的執行個體。

## 請參閱

#### 其他資源

[Remove-CsVoicePolicy](remove-csvoicepolicy.md)  
[Set-CsVoicePolicy](set-csvoicepolicy.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Grant-CsVoicePolicy](grant-csvoicepolicy.md)  
[Test-CsVoicePolicy](test-csvoicepolicy.md)  
[Get-CsPstnUsage](get-cspstnusage.md)

