---
title: Set-CsDialInConferencingAccessNumber
TOCTitle: Set-CsDialInConferencingAccessNumber
ms:assetid: 2b640607-ee83-4962-865d-ed74ddd17649
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425770(v=OCS.15)
ms:contentKeyID: 49290413
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsDialInConferencingAccessNumber

 

_**上次修改主題的時間：** 2015-03-09_

修改現有電話撥入式會議存取號碼的屬性值。電話撥入式會議可讓使用者使用一般的電話、行動電話或公用交換電話網路 (PSTN) 上的其他裝置加入會議的音訊部分。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsDialInConferencingAccessNumber -Identity <UserIdParameter> [-DisplayName <String>] [-DisplayNumber <String>] [-LineUri <String>] [-PrimaryLanguage <String>] [-Regions <MultiValuedProperty>] [-ScopeToGlobal <SwitchParameter>] [-ScopeToSite <SwitchParameter>] [-SecondaryLanguages <MultiValuedProperty>] <COMMON PARAMETERS>

    Set-CsDialInConferencingAccessNumber -Identity <UserIdParameter> -Priority <Int32> -ReorderedRegion <String> <COMMON PARAMETERS>

    Set-CsDialInConferencingAccessNumber -Instance <AccessNumber> [-ScopeToGlobal <SwitchParameter>] [-ScopeToSite <SwitchParameter>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會以 Identity sip:RedmondDialIn@litwareinc.com 修改電話撥入式會議存取號碼的 DisplayName 屬性。在此範例中，顯示名稱設為 "Redmond Dial-In Access Number"。

    Set-CsDialInConferencingAccessNumber -Identity "sip:RedmondDialIn@litwareinc.com" -DisplayName "Redmond Dial-In Access Number"

## 範例 2

範例 2 會以 Identity sip:RedmondDialIn@litwareinc.com 修改電話撥入式會議存取號碼以包含兩個地區：Redmond 和 Seattle。為達此目的，會先呼叫 Region 參數，然後是兩個地區 (以逗號分隔的兩個字串值)。請注意，除非已經在撥號對應表中定義 Redmond 和 Seattle 地區，否則這個命令將會失敗。

    Set-CsDialInConferencingAccessNumber -Identity "sip:RedmondDialIn@litwareinc.com" -Regions "Redmond", "Seattle"

## 範例 3

在範例 3 中，主要語言為法文的所有電話撥入式會議存取號碼都會經過修改，以使用加拿大法文做為次要語言。為了執行此工作，會先呼叫 **Get-CsDialInConferencingAccessNumber** Cmdlet 傳回設定供組織使用之所有電話撥入式存取號碼的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會挑出 PrimaryLanguage 屬性等於 French ("fr-FR") 的存取號碼。接著將篩選後的集合管線傳送到 **Set-CsDialInConferencingAccessNumber** Cmdlet，以將 SecondaryLanguages 屬性的值設為 French Canadian ("fr-CA")。

    Get-CsDialInConferencingAccessNumber | Where-Object {$_.PrimaryLanguage -eq "fr-FR"}| Set-CsDialInConferencingAccessNumber -SecondaryLanguages "fr-CA"

## 範例 4

範例 4 所示的命令會針對指定的電話撥入式會議存取號碼變更 Active Directory 顯示名稱。為達成此目的，命令會先使用 **Get-CsDialInConferencingAccessNumber** Cmdlet 搭配 Filter 參數傳回 DisplayName 屬性等於 "Default DialIn Access Number" 的撥入式存取號碼。然後再將該存取號碼管線傳送到 **Set-CsDialInConferencingAccessNumber** Cmdlet，以將顯示名稱變更為 Litwareinc Conferencing。

    Get-CsDialInConferencingAccessNumber -Filter {DisplayName -eq "Default DialIn Access Number"} | Set-CsDialInConferencingAccessNumber -DisplayName "Litwareinc Conferencing"

## 範例 5

在範例 5 中，顯示名稱和線路統一資源識別元 (URI) 都會針對指定的電話撥入式會議存取號碼進行修改。為了擷取要修改的號碼，此命令先使用 **Get-CsDialInConferencingAccessNumber** Cmdlet 和 Filter 參數；隨附的篩選值會將傳回的資料限制為 LineUri 內容等於 TEL:+14255558715 的存取號碼。接著，該存取號碼會管線傳送到 **Set-CsDialInConferencingAccessNumber** Cmdlet，由它同時修改存取號碼的 DisplayNumber 和 LineUri 內容。

    Get-CsDialInConferencingAccessNumber -Filter {LineUri -eq "TEL:+14255558715"} | Set-CsDialInConferencingAccessNumber -DisplayNumber "1-425-555-1298" -LineUri "tel:+14255551298"

## 範例 6

範例 6 會將一組次要語言指派給不使用美國英文做為其主要語言的所有電話撥入式會議存取號碼。為達成此目的，命令會先呼叫 **Get-CsDialInConferencingAccessNumber** Cmdlet，以傳回設定供組織所用之所有電話撥入式會議存取號碼的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這樣只會選取 PrimaryLanguage 屬性不等於美國英文 (en-US) 的號碼。接著將篩選後的集合管線傳送到 **Set-CsDialInConferencingAccessNumber** Cmdlet，以使用 -SecondaryLanguages 參數為集合中的每個號碼指派次要語言為 French (fr-FR) 和 Italian (it-IT)。

    Get-CsDialInConferencingAccessNumber | Where-Object {$_.PrimaryLanguage -ne "en-US"} | Set-CsDialInConferencingAccessNumber -SecondaryLanguages "fr-FR","it-IT"

## 範例 7

範例 7 所示的命令會將 Rdemond 地區的最高優先順序指派給電話撥入式會議存取號碼 "sip:RedmondDialIn@litwareinc.com"；因此，在會議邀請中和電話撥入式會議網頁上，會最先列出此號碼。為了設定優先順序，會加上 Priority 參數搭配參數值 0 (最高優先順序存取號碼的 Priority 值為 0，次高優先順序號碼的 Priority 值為 1，依此類推)。此外，也加上 ReorderedRegion 參數，以表示要在 Redmond 區域內變更存取號碼優先順序。

    Get-CsDialInConferencingAccessNumber -Identity ""sip:RedmondDialIn@litwareinc.com"" -Priority 0 -ReorderedRegion Redmond

## 詳細描述

電話撥入式會議讓使用者可以使用任何一種電話 (例如，標準的「地面通訊」電話、行動電話或 Voice over Internet Protocol (VoIP) 電話) 加入會議的音訊部分。即使使用者沒有電腦或網際網路連線，都可讓他們參與會議。撥入使用者可用完整的音訊功能：他們可以與其他參與者講話，也可以聽到其他人所說的每句話；他們只是看不到共用的投影片、視訊播放或其他視覺元素。

若要為使用者提供電話撥入式會議的功能，您必須建立電話撥入式會議存取號碼：電話號碼使用者可以利用撥打電話的方式連線到會議。電話撥入式會議存取號碼是以 **New-CsDialInConferencingAccessNumber** Cmdlet 建立。當您建立新的電話撥入式會議存取號碼時，實際上是在 Active Directory 網域服務 中建立新的連絡人物件。此連絡人物件用來代表存取號碼及其所有內容。

電話撥入式會議號碼建立完成之後，您可以使用 **Set-CsDialInConferencingAccessNumber** Cmdlet 修改該號碼的屬性。例如，您可以變更電話號碼 (LineUri) 本身之類的設定；或是表示該號碼之連絡人物件的顯示名稱。此外，**Set-CsDialInConferencingAccessNumber** Cmdlet 可讓您修改號碼的範圍；例如，您可以使用這個 Cmdlet 取得已經指派到全域範圍的號碼並重新指派給網站範圍。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsDialInConferencingAccessNumber** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsDialInConferencingAccessNumber"}

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
<td><p>表示電話撥入式會議號碼之連絡人物件的 SIP 位址。指定 Identity 時，您必須加入 &quot;sip:&quot;首碼；例如：-Identity &quot; sip:RedmondDialIn@litwareinc.com&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.AccessNumber</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>Priority</em></p></td>
<td><p>必要</p></td>
<td><p>System.Int32</p></td>
<td><p>讓您變更使用者在會議邀請中或存取電話撥入式會議網頁時，看到的電話撥入式會議號碼順序。號碼越小，優先順序越高；若要讓號碼出現在清單開頭，請將優先順序設為 0。請注意，如果您變更指定號碼的優先順序，您也必須使用 ReorderedRegion 參數指出已修改優先順序應該生效的地區。</p></td>
</tr>
<tr class="even">
<td><p><em>ReorderedRegion</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>以地區變更電話撥入式會議號碼的優先順序時，搭配 Priority 參數使用。ReorderedRegion 參數會指出進行優先順序重新排列的地區；例如：-ReorderedRegion &quot;Redmond&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>新連絡人物件的 Active Directory 顯示名稱。這是也會顯示在 Lync 中的名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayNumber</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>電話號碼會顯示在會議邀請中和 [電話撥入式會議設定] 網頁上。您可以將 DisplayNumber 的格式設定成任何偏好的形式，如 1-800-555-1234、1-(800)-555-1234 或 1.800.555.1234。</p></td>
</tr>
<tr class="even">
<td><p><em>LineUri</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>實際的電話撥入式會議電話號碼。LineUri 必須以下列語法加以指定：tel:前置詞後依序加上加號 (+)、國碼/地區、區碼及電話號碼。例如：tel:+18005551234。不允許使用空格、連字號、括弧及其他字元。</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>可讓您利用代表已修改撥入會議存取號碼的管線傳遞連絡人物件。根據預設，<strong>Set-CsDialInConferencingAccessNumber</strong> Cmdlet 不會經由該管線傳遞物件。</p></td>
</tr>
<tr class="even">
<td><p><em>PrimaryLanguage</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>用於宣告電話撥入式會議的主要語言。您必須使用任一項可用的電話撥入會議語言代碼來設定語言，例如 en-US 代表美國英文或 fr-FR 代表法文等。若要傳回可用的語言代碼清單，請在 Windows PowerShell 提示字元中輸入下列命令：</p>
<p>Get-CsDialInConferencingLanguageList | Select-Object -ExpandProperty Languages。</p></td>
</tr>
<tr class="odd">
<td><p><em>Regions</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.MultiValuedProperty</p></td>
<td><p>與撥入號碼相關聯的撥號對應表地區。如果地區未包含在至少一個撥號對應表中，該地區便無法和撥入會議存取號碼相關聯。若要指定多個地區，請使用逗號分隔清單：-Regions &quot;Northwest&quot;, &quot;Southwest&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>ScopeToGlobal</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如果存在，會將電話撥入式會議號碼指派到全域範圍。</p></td>
</tr>
<tr class="odd">
<td><p><em>ScopeToSite</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如果存在，會將電話撥入式會議號碼的範圍設為連絡人物件登錄器集區所在的網站。</p></td>
</tr>
<tr class="even">
<td><p><em>SecondaryLanguages</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.MultiValuedProperty</p></td>
<td><p>選用的語言集合也可以用於宣告電話撥入式會議。次要語言必須設定為語言代碼的逗號分隔清單；例如，下列語法會將加拿大法文與法文設為次要語言：-SecondaryLanguages &quot;fr-CA&quot;, &quot;fr-FR&quot;。</p>
<p>存取號碼最多可以與四個次要語言相關聯。</p></td>
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

Microsoft.Rtc.Management.Xds.AccessNumber 物件。**Set-CsDialInConferencingAccessNumber** Cmdlet 接受存取號碼物件的管線傳送輸入。

## 傳回類型

**Set-CsDialInConferencingAccessNumber** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.Xds.AccessNumber 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsDialInConferencingAccessNumber](get-csdialinconferencingaccessnumber.md)  
[New-CsDialInConferencingAccessNumber](new-csdialinconferencingaccessnumber.md)  
[Remove-CsDialInConferencingAccessNumber](remove-csdialinconferencingaccessnumber.md)

