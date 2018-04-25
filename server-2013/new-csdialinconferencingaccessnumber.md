---
title: New-CsDialInConferencingAccessNumber
TOCTitle: New-CsDialInConferencingAccessNumber
ms:assetid: c6d0536c-0ba3-45e0-affe-7ee00a070435
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398818(v=OCS.15)
ms:contentKeyID: 49292280
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsDialInConferencingAccessNumber

 

_**上次修改主題的時間：** 2015-03-09_

建立新的電話撥入式會議存取號碼。電話撥入式會議可讓使用者使用一般的電話、行動電話或公用交換電話網路 (PSTN) 上的其他裝置加入會議的音訊部分。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsDialInConferencingAccessNumber -Pool <Fqdn> -Regions <MultiValuedProperty> <COMMON PARAMETERS>

    New-CsDialInConferencingAccessNumber -HostingProviderProxyFqdn <Fqdn> <COMMON PARAMETERS>

    COMMON PARAMETERS: -DisplayNumber <String> -LineURI <String> -PrimaryLanguage <String> -PrimaryUri <String> [-Confirm [<SwitchParameter>]] [-DisplayName <String>] [-PassThru <SwitchParameter>] [-ScopeToSite <SwitchParameter>] [-SecondaryLanguages <MultiValuedProperty>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 可利用主要 URI sip:RedmondDialIn@litwareinc.com 建立新的電話撥入式會議存取號碼。除了 PrimaryUri 參數之外，該命令還包括以下參數：將電話號碼設定為如 Lync 所顯示之格式的參數 (DisplayNumber)、將電話號碼設定為 E.164 格式的參數 (LineUri)、代表新號碼指派之目的地登錄器集區的參數 (-Pool)、代表號碼之主要語言的參數 (PrimaryLanguage)，以及代表新號碼指派之目的地地區的參數 (Region)。

    New-CsDialInConferencingAccessNumber -PrimaryUri "sip:RedmondDialIn@litwareinc.com" -DisplayNumber "1-800-555-1234" -LineUri "tel:+18005551234" -Pool atl-cs-001.litwareinc.com -PrimaryLanguage "en-US" -Regions "Redmond"

## 範例 2

範例 2 所示的命令是範例 1 所示命令的變化。唯一的差異在於此範例展示的命令還會將兩個次要語言 (加拿大法文和法文) 指派給新的撥入會議存取號碼。為了指派這些次要語言，此命令加入了 SecondaryLanguages 參數和要指派之語言 (fr-CA 和 fr-FR) 的逗號分隔清單。

    New-CsDialInConferencingAccessNumber -PrimaryUri "sip:RedmondDialIn@litwareinc.com" -DisplayNumber "1-800-555-1234" -LineUri "tel:+18005551234" -Pool atl-cs-001.litwareinc.com -PrimaryLanguage "en-US" -Regions "Redmond" -SecondaryLanguages "fr-CA", "fr-FR"

## 範例 3

範例 3 會建立新的電話撥入式會議存取號碼，其範圍為連絡人物件之主集區所在的網站。為達此目的，命令會加上 ScopeToSite 參數。

    New-CsDialInConferencingAccessNumber -PrimaryUri "sip:RedmondDialIn@litwareinc.com" -DisplayNumber "1-800-555-1234" -LineUri "tel:+18005551234" -Pool atl-cs-001.litwareinc.com -PrimaryLanguage "en-US" -Regions "Redmond" -ScopeToSite

## 詳細描述

電話撥入式會議讓使用者可以使用任何一種電話 (例如，標準的「地面通訊」電話、行動電話或 Voice over Internet Protocol (VoIP) 電話)，來加入線上會議的音訊部分。讓使用者即使沒有電腦或網際網路連線也可以參與會議。使用者可用完整的音訊功能：他們可以對其他參與者講話，聽到其他人所說的每句話。他們只是看不到共用的投影片、視訊播放，或其他視覺元素。

若要為使用者提供電話撥入式會議的功能，您必須建立電話撥入式會議存取號碼：使用者要連線至會議時撥打的電話號碼。電話撥入式會議存取號碼是以 **New-CsDialInConferencingAccessNumber** Cmdlet 建立。當您建立新的電話撥入式會議存取號碼時，您其實是在 Active Directory 網域服務 中建立新的連絡人物件；此連絡人物件是用來代表存取號碼及其所有屬性。

建立新的撥入號碼時，您必須加入下列參數：PrimaryUri、LineURI、Pool、DisplayNumber、PrimaryLanguage 和 Regions。這些參數 (和各自的參數值) 都是符合常理而簡單的參數，可能只有一項例外狀況：然而 Regions 除外。在建立新的存取號碼時，該號碼必須和一或多個地區相關聯。再者，除非地區至少出現在一個撥號對應表中，否則該區域無法和撥入會議號碼相關聯。如果地區至少出現在一個撥號對應表的 DialInConferencingRegion 屬性中，該地區便能和存取號碼相關聯，如果沒有，該地區將無法與存取號碼相關聯。這就表示您必須先建立撥號對應表，並為該撥號對應表指定地區，才能建立電話撥入式會議存取號碼。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsDialInConferencingAccessNumber** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsDialInConferencingAccessNumber"}

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
<td><p><em>DisplayNumber</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>在會議邀請與電話撥入式會議網頁顯示的電話號碼。您可以將 DisplayNumber 的格式設定成任何偏好的形式，如 1-800-555-1234、1-(800)-555-1234 或 1.800.555.1234。</p></td>
</tr>
<tr class="even">
<td><p><em>HostingProviderProxyFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>裝載電話撥入式會議服務之主機供應商的完整網域名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>LineURI</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>實際的撥入會議電話號碼。LineURI 必須以下列語法加以指定：在 tel:前置詞後依序加上加號 (+)、國碼/地區、區碼及電話號碼。例如：tel:+18005551234。請注意，此語法不允許使用空格、連字號、括弧及其他字元。</p>
<p>LineURI 在整個 Active Directory 中必須是唯一的。</p></td>
</tr>
<tr class="even">
<td><p><em>Pool</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>新連絡人物件的 Home 集區。</p></td>
</tr>
<tr class="odd">
<td><p><em>PrimaryLanguage</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>用於發佈撥入會議宣告的主要語言。您必須使用任一項可用的撥入會議語言代碼來設定語言，例如 en-US 代表「美國英文」、fr-FR 代表「法文」等。若要傳回可用的語言代碼清單，請在 Windows PowerShell 提示字元中輸入下列命令：</p>
<p>Get-CsDialInConferencingLanguageList | Select-Object -ExpandProperty Languages。</p></td>
</tr>
<tr class="even">
<td><p><em>PrimaryUri</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要指派給新連絡人物件的唯一 SIP 位址。在指定 PrimaryUri 時，您必須加入 &quot;sip:&quot; 首碼。例如：-PrimaryUri &quot; sip:RedmondDialIn@litwareinc.com&quot;。請注意，sip: 首碼必須以全部小寫字母的方式輸入。</p></td>
</tr>
<tr class="odd">
<td><p><em>Regions</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.MultiValuedProperty</p></td>
<td><p>和撥入號碼相關聯的撥號對應表地區。如果地區未包含在至少一個撥號對應表中，該地區便無法和撥入會議存取號碼相關聯。若要指定多個地區，請使用逗號分隔清單：-Regions &quot;Northwest&quot;, &quot;Southwest&quot;</p></td>
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
<td><p>新連絡人物件的 Active Directory 顯示名稱。這也是顯示在 Lync 中的名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>可讓您利用代表新撥入會議存取號碼的管線傳遞連絡人物件。根據預設，<strong>New-CsDialInConferencingAccessNumber</strong> Cmdlet 不會經由該管線傳遞物件。</p></td>
</tr>
<tr class="odd">
<td><p><em>ScopeToSite</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>使用後，系統會將新號碼納入連絡人物件之主集區的相同網站範圍內。若未加入 ScopeToSite 參數，系統便會將新號碼指派至全域範圍內。</p></td>
</tr>
<tr class="even">
<td><p><em>SecondaryLanguages</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.MultiValuedProperty</p></td>
<td><p>選用的語言集合，亦可用來發佈撥入會議宣告。您必須將次要語言設定為以逗號分隔的語言代碼清單。例如，下列語法可將法文 (加拿大) 和法文設為次要語言：-SecondaryLanguages &quot;fr-CA&quot;, &quot;fr-FR&quot;。</p>
<p>一個存取號碼最多能擁有四個次要語言。</p></td>
</tr>
<tr class="odd">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要建立新電話撥入式會議存取號碼的 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行此命令，為每個租用戶傳回租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
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

無。**New-CsDialInConferencingAccessNumber** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsDialInConferencingAccessNumber** Cmdlet 會建立 Microsoft.Rtc.Management.Xds.AccessNumber 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsDialInConferencingAccessNumber](get-csdialinconferencingaccessnumber.md)  
[Remove-CsDialInConferencingAccessNumber](remove-csdialinconferencingaccessnumber.md)  
[Set-CsDialInConferencingAccessNumber](set-csdialinconferencingaccessnumber.md)

