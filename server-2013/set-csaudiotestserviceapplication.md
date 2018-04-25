---
title: Set-CsAudioTestServiceApplication
TOCTitle: Set-CsAudioTestServiceApplication
ms:assetid: d2c6880b-58df-43d1-9f26-d2b9f54d3f0b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398907(v=OCS.15)
ms:contentKeyID: 49292402
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsAudioTestServiceApplication

 

_**上次修改主題的時間：** 2015-03-09_

可讓您修改組織目前所使用之任何音訊測試服務應用程式連絡人的屬性值。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsAudioTestServiceApplication -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-DisplayName <String>] [-DisplayNumber <String>] [-Enabled <$true | $false>] [-EnabledForFederation <$true | $false>] [-EnterpriseVoiceEnabled <$true | $false>] [-ExchangeArchivingPolicy <Uninitialized | UseLyncArchivingPolicy | NoArchiving | ArchivingToExchange>] [-LineURI <String>] [-PassThru <SwitchParameter>] [-PrimaryLanguage <String>] [-SecondaryLanguages <MultiValuedProperty>] [-SipAddress <String>] [-Type <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

在範例 1 中，適用於音訊測試服務連絡人 sip:RedmondAudioTest@litwareinc.com 的主要語言已設定為「英文 (美國)」(en-US)。

    Set-CsAudioTestServiceApplication -Identity "sip:RedmondAudioTest@litwareinc.com" -PrimaryLanguage "en-US" 

## 範例 2

範例 2 會清除音訊測試服務連絡人 sip:RedmondAudioTest@litwareinc.com 的 PrimaryLanguage 屬性值。作法是使用 PrimaryLanguage 參數搭配參數值 $Null。

    Set-CsAudioTestServiceApplication -Identity "sip:RedmondAudioTest@litwareinc.com" -PrimaryLanguage $Null 

## 範例 3

在範例 3 中，已將組織使用的所有音訊測試服務連絡人設為使用「英文 (美國)」做為其主要語言。為達成此目的，會先呼叫不含任何參數的 **Get-CsAudioTestServiceApplication** Cmdlet，以傳回音訊測試服務連絡人的集合。然後，此集合會管線傳送到 **Set-CsAudioTestServiceApplication**，以將「英文 (美國)」(en-Us) 指派給集合中每一位連絡人的 PrimaryLanguage 屬性。

    Get-CsAudioTestServiceApplication | Set-CsAudioTestServiceApplication -PrimaryLanguage "en-US"

## 詳細描述

音訊測試服務可讓 Lync Server 使用者在進行語音通話之前測試其語音連線。為達此目的，使用者必須在 \[ Lync 選項\] 對話方塊中，按一下 \[音訊裝置\] 索引標籤上的 \[檢查通話品質\] 按鈕。當使用者按下此按鈕後，將會撥電話給自動音訊測試服務。來電將被接聽，並在播放一段介紹提示之後，要求來電者錄製一段簡短的訊息 (最多 10 秒)。接著會重新播放該錄音，讓來電者利用現有的連線試聽其聲音。

音訊測試服務在某種程度上會依賴 Active Directory 連絡人物件。當您安裝 Audio Bot 時，系統會為您自動建立這些物件；沒有其他方法可以手動建立這些物件。但是，系統管理員可以使用 **Get-CsAudioTestServiceApplication** Cmdlet，來擷取組織目前使用之各種測試服務連絡人的資訊。系統管理員也可以使用 **Set-CsAudioTestServiceApplication** Cmdlet，來修改這些連絡人的屬性。

誰可以執行這個 Cmdlet：根據預設，會授權下列群組的成員執行 **Set-CsAudioTestServiceApplication** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsAudioTestServiceApplication"}

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
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>要修改之音訊測試服務連絡人的 SIP 位址。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>連絡人物件的 Active Directory 顯示名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayNumber</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>雖然是有效的內容，但是 DisplayNumber 實際上無法與音訊測試服務搭配使用。</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>表示是否已為 Lync Server 啟用連絡人物件。如果您將此值設為 False ($False)，連絡人就無法再登入 Lync Server；將此值設為 True ($True) 可重新啟用連絡人的登入權限。</p></td>
</tr>
<tr class="even">
<td><p><em>EnabledForFederation</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>表示此連絡人是否可以用於同盟網域的使用者。若設定為 False，則只有您組織內的使用者具有該連絡人的存取權。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnterpriseVoiceEnabled</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>表示連絡人物件是否已啟用 Enterprise Voice，這是 Microsoft 的 Voice over Internet Protocol (VoIP) 實作。透過 Enterprise Voice，使用者可以使用網際網路來撥打電話，而非使用標準電話網路。</p></td>
</tr>
<tr class="even">
<td><p><em>ExchangeArchivingPolicy</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.ExchangeArchivingPolicyOptionsEnum</p></td>
<td><p>表示連絡人之立即訊息工作階段的封存位置。允許的值為：</p>
<p>* Uninitialized</p>
<p>* UseLyncArchivingPolicy</p>
<p>* ArchivingToExchange</p>
<p>* NoArchiving</p></td>
</tr>
<tr class="odd">
<td><p><em>LineURI</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>雖然是有效的內容，但是 LineUri 實際上無法與音訊測試服務搭配使用。</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>可讓您透過代表已指派原則的使用者之管線傳遞使用者物件。根據預設，<strong>Set-CsAudioTestServiceApplication</strong> Cmdlet 不會透過管線傳遞任何物件。</p></td>
</tr>
<tr class="odd">
<td><p><em>PrimaryLanguage</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>用於音訊測試服務的主要語言。您必須使用任一項允許的語言代碼來設定語言，例如，en-US 代表「英文 (美國)」、fr-FR 代表「法文」等。若要傳回可用的語言代碼清單，請在 Windows PowerShell 提示字元中輸入下列命令：</p>
<p>Get-CsDialInConferencingLanguageList | Select-Object -ExpandProperty Languages。</p></td>
</tr>
<tr class="even">
<td><p><em>SecondaryLanguages</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.MultiValuedProperty</p></td>
<td><p>雖然是有效的內容，但是 SecondaryLanguages 實際上無法與音訊測試服務搭配使用。</p></td>
</tr>
<tr class="odd">
<td><p><em>SipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此參數目前停用。您無法使用 Set-CsAudioTestServiceApplication 變更 SIP 位址。</p></td>
</tr>
<tr class="even">
<td><p><em>Type</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>表示要進行部署的測試連絡人類型。根據預設，將連絡人列為自動，這表示他們可以與來電者互動。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

**Set-CsAudioTestServiceApplication** Cmdlet 接受 Microsoft.Rtc.Management.ADConnect.Schema.OCSADApplicationContact 物件管線傳送的執行個體。

## 傳回類型

**Set-CsAudioTestServiceApplication** Cmdlet 不會傳回任何物件或值。

## 請參閱

#### 其他資源

[Get-CsAudioTestServiceApplication](get-csaudiotestserviceapplication.md)

