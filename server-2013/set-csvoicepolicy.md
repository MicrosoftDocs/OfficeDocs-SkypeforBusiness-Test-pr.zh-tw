---
title: Set-CsVoicePolicy
TOCTitle: Set-CsVoicePolicy
ms:assetid: e6035b74-d760-4c48-aa0b-d09d129e0830
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399021(v=OCS.15)
ms:contentKeyID: 49292636
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoicePolicy

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的語音原則。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsVoicePolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsVoicePolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AllowCallForwarding <$true | $false>] [-AllowPSTNReRouting <$true | $false>] [-AllowSimulRing <$true | $false>] [-CallForwardingSimulRingUsageType <VoicePolicyUsage | InternalOnly | CustomUsage>] [-Confirm [<SwitchParameter>]] [-CustomCallForwardingSimulRingUsages <PSListModifier>] [-Description <String>] [-EnableBWPolicyOverride <$true | $false>] [-EnableCallPark <$true | $false>] [-EnableCallTransfer <$true | $false>] [-EnableDelegation <$true | $false>] [-EnableMaliciousCallTracing <$true | $false>] [-EnableTeamCall <$true | $false>] [-EnableVoicemailEscapeTimer <$true | $false>] [-Force <SwitchParameter>] [-Name <String>] [-PreventPSTNTollBypass <$true | $false>] [-PstnUsages <PSListModifier>] [-PSTNVoicemailEscapeTimer <Int64>] [-Tenant <Guid>] [-VoiceDeploymentMode <OnPrem | Online | OnlineBasic | OnPremOnlineHybrid>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會將個別使用者原則 UserVoicePolicy2 的 AllowSimulRing 屬性設為 False，表示任何指派此原則的使用者，都不會啟用同時響鈴，而此功能決定是否可設定每當使用者的辦公室電話響起時，第二支電話 (例如行動電話) 也會響起。此命令也會從這個原則的 PSTN 使用方式清單中移除 "Local" (請注意，未明確指定 Identity 參數。Identity 參數是位置參數，因此如果將識別身分值放在參數清單的開頭，則不需要明確指出它是 Identity)。

    Set-CsVoicePolicy UserVoicePolicy2 -AllowSimulRing $false -PstnUsages @{remove="Local"}

## 範例 2

此範例會修改網站 Redmond 的語音原則，如此會將已針對組織定義的所有 PSTN 使用方式套用至此原則。此範例的第一行會呼叫 **Get-CsPstnUsage** Cmdlet，以擷取組織所使用的全域 PSTN 使用方式集，並儲存於變數 $a 中。第二行會呼叫 **Set-CsVoicePolicy** Cmdlet，以修改網站 Redmond 的語音原則。傳遞給 PstnUsages 參數的值，會使用全域 PSTN 使用方式集所含的清單來取代原則目前的使用方式清單。請注意取代值的語法：$a.Usage。這是指 PSTN 使用方式設定的 Usage 屬性，其中含有 PSTN 使用方式的清單。

    $a = Get-CsPstnUsage
    Set-CsVoicePolicy -Identity site:Redmond -PstnUsages @{replace=$a.Usage}

## 詳細描述

這個 Cmdlet 會修改現有的語音原則。語音原則可用來管理 Enterprise Voice 相關功能，例如同時響鈴 (每次有人撥打到您的辦公室電話時，能夠讓第二支電話響起) 和來電轉接。使用這個 Cmdlet 來變更啟用和停用其中許多功能的設定。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsVoicePolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoicePolicy"}

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
<td><p><em>AllowCallForwarding</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>如果此參數設為 True，則指派給此原則的使用者可以轉接來電。如果此參數設為 False，則無法轉接來電。</p></td>
</tr>
<tr class="even">
<td><p><em>AllowPSTNReRouting</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>如果此參數設為 True 時，當集區或 WAN 無法使用時，對位在另一集區內部號碼撥號的電話會透過公用交換電話網路 (PSTN) 路由。</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowSimulRing</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>同時響鈴為撥打單一號碼時允許多個電話響鈴的功能。將此參數設為 True 會啟用同時響鈴。如果此參數設為 False，則無法對指派至此原則的任何使用者設定同時響鈴。</p></td>
</tr>
<tr class="even">
<td><p><em>CallForwardingSimulRingUsageType</em></p></td>
<td><p>選用</p></td>
<td><p>CallForwardingSimulRingUsageType</p></td>
<td><p>提供方法，讓系統管理員可以管理來電轉接及同時響鈴。允許的值為：</p>
<p>* VoicePolicyUsage – 用來管理所有來電之來電轉接及同時響鈴的預設語音原則使用方式。此為預設值。</p>
<p>* InternalOnly – 將來電轉接及同時響鈴限制於一位 Lync 使用者撥打給另一位 Lync 使用者的電話。</p>
<p>* CustomUsage - 用來管理來電轉接及同時響鈴的自訂 PSTN 使用方式。此使用方式必須使用 CustomCallForwardingSimulRingUsages 參數加以指定。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>CustomCallForwardingSimulRingUsages</em></p></td>
<td><p>選用</p></td>
<td><p>PSListModifier</p></td>
<td><p>用來管理來電轉接及同時響鈴的自訂 PSTN 使用方式。若要將自訂使用方式新增至語音原則，請使用類似下列的語法：</p>
<p>-CustomCallForwardingSimulRingUsages @{Add=&quot;RedmondPstnUsage&quot;}</p>
<p>若要移除自訂使用方式，請使用下列語法：</p>
<p>-CustomCallForwardingSimulRingUsages @{Remove=&quot;RedmondPstnUsage&quot;}</p>
<p>請注意，使用方式必須存在，才能搭配 CustomCallForwardingSimulRingUsages 參數使用。</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>語音原則的描述。</p>
<p>最大長度：1040 個字元。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableBWPolicyOverride</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>可以設定原則，以限制頻寬及設定各種其他關於網路設定的屬性。將此參數設為 True 將允許覆寫這些原則。換句話說，如果此參數設為 True，則不會進行頻寬檢查，無論通話許可控制 (CAC) 的設定為何，來電都會通過。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableCallPark</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>通話駐留應用程式 允許保留特定號碼範圍內某個號碼的來電，稍後再擷取。將此參數設為 True 可讓此應用程式為使用者指派此原則。如果此參數設為 False，則指派至此原則的使用者無法保留已撥到電話號碼的來電。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableCallTransfer</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>決定來電是否可以轉接至另一個號碼。如果此參數設為 True，則可以轉接來電；如果此參數設為 False，則無法轉接來電。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableDelegation</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>通話委派允許使用者接聽其他使用者的來電，或代表其他使用者撥打電話。例如，經理可以設定通話委派，讓所有來電在自己的電話和管理員的電話上響起。將此參數設為 True，可讓具有此原則的使用者設定通話委派。將此參數設為 False 會停用通話委派。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableMaliciousCallTracing</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>惡意來電追蹤是一種標準，可隨時追蹤使用者指定為惡意的來電。即使已封鎖來電者識別碼，仍然可以追蹤這些來電。僅限適當的授權者才可追蹤，使用者無法使用追蹤。將此屬性設為 True，允許在惡意來電上設定追蹤。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableTeamCall</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>小組通話可讓使用者指定一組其他使用者，當撥打該使用者的號碼時，這一組使用者的電話會響起。在小組中此功能很有用，例如，小組的任何人都可以接聽客戶來電。將此參數設為 True 會啟用此功能。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableVoicemailEscapeTimer</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>設為 True 時，行動裝置的未接來電會轉接至組織的語音信箱，而不是行動裝置提供者的語音信箱。如果「太早」接聽來電 (亦即未達到為 PSTNVoicemailEscapeTimer 屬性設定的值)，則會假設行動裝置沒有空，並將來電轉接至組織的語音信箱。</p>
<p>預設值為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>XdsIdentity</p></td>
<td><p>指定原則的範圍和 (在某些情況下) 名稱的唯一識別碼。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>VoicePolicy</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。 這個物件必須是 VoicePolicy 類型，呼叫 <strong>Get-CsVoicePolicy</strong> Cmdlet 即可擷取此物件。</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>描述此原則的易記名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>PreventPSTNTollBypass</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>PSTN 費用通常稱為長途電話費。組織可以實作 Voice over Internet Protocol (VoIP) 解決方案，讓分公司透過網路電話來聯繫，有時就能節省這些電話費。將此參數設為 True 會透過 PSTN 撥打電話且必須付費，而非經由網路而節省電話費。</p></td>
</tr>
<tr class="even">
<td><p><em>PstnUsages</em></p></td>
<td><p>選用</p></td>
<td><p>PSListModifier</p></td>
<td><p>此原則可用的 PSTN 使用方式清單。PSTN 使用方式將語音原則繫結至電話路由。</p>
<p>任何字串值皆可放置在清單中，只要該值存在於 PSTN 使用方式的目前全域清單中(不允許重複字串；所有字串必須是唯一的)。您可以呼叫 <strong>Get-CsPstnUsage</strong> Cmdlet 來擷取 PSTN 使用方式清單。</p>
<p>請記住，如果您使用此參數，從原則移除所有的 PSTN 使用方式，使用者授與此原則將無法撥出 PSTN 電話。</p></td>
</tr>
<tr class="odd">
<td><p><em>PSTNVoicemailEscapeTimer</em></p></td>
<td><p>選用</p></td>
<td><p>Int64</p></td>
<td><p>用來判斷是否「太快」接聽電話的時間量 (以毫秒為單位)。如果在此時間間隔內收到回應，Lync Server 會假設行動裝置無法使用，並自動將通話切換至組織的語音信箱。如果在達到此時間間隔之前沒有收到任何回應，則可繼續進行通話。</p>
<p>預設值為 1500 毫秒。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>Guid</p></td>
<td><p>要修改其語音原則之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行下列命令傳回每個租用戶的租用戶識別碼：</p>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoicePolicy 物件。接受管線傳送的語音原則物件輸入。

## 傳回類型

此 Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Voice.VoicePolicy 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsVoicePolicy](new-csvoicepolicy.md)  
[Remove-CsVoicePolicy](remove-csvoicepolicy.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Grant-CsVoicePolicy](grant-csvoicepolicy.md)  
[Test-CsVoicePolicy](test-csvoicepolicy.md)  
[Get-CsPstnUsage](get-cspstnusage.md)

