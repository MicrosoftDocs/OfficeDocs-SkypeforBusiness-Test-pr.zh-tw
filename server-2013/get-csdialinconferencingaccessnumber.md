---
title: Get-CsDialInConferencingAccessNumber
TOCTitle: Get-CsDialInConferencingAccessNumber
ms:assetid: f2c78377-ad21-4a9f-bef9-e9ef97316c85
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413015(v=OCS.15)
ms:contentKeyID: 49292793
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsDialInConferencingAccessNumber

 

_**上次修改主題的時間：** 2015-03-09_

傳回設定供組織使用之所有電話撥入式會議存取號碼的資訊。電話撥入式會議可讓使用者使用一般的電話、行動電話或公用交換電話網路 (PSTN) 上的其他裝置加入會議的音訊部分。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsDialInConferencingAccessNumber [-Region <String>] <COMMON PARAMETERS>

    Get-CsDialInConferencingAccessNumber -EmptyRegion <SwitchParameter> <COMMON PARAMETERS>

    Get-CsDialInConferencingAccessNumber [-Identity <UserIdParameter>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Filter <String>] [-OU <OUIdParameter>] [-ResultSize <Unlimited>]

## 範例

## 範例 1

範例 1 所示的命令會傳回已設定為在組織內使用的所有電話撥入式會議存取號碼集合。呼叫不含任何其他參數的 **Get-CsDialInConferencingAccessNumber** Cmdlet ，將一律傳回所有可用的電話撥入式存取號碼集合。

    Get-CsDialInConferencingAccessNumber

## 範例 2

範例 2 會傳回 Identity 為 sip:RedmondDialIn@litwareinc.com 的電話撥入式會議存取號碼。由於識別身分必須是唯一的，因此這個命令絕對不會傳回一個以上的存取號碼。

    Get-CsDialInConferencingAccessNumber -Identity sip:RedmondDialIn@litwareinc.com

## 範例 3

範例 3 會使用 Region 參數傳回與 Redmond 地區相關聯的所有電話撥入式會議存取號碼。為達成此目的，會呼叫 **Get-CsDialInConferencingAccessNumber** Cmdlet 搭配 Region 參數。指定參數值 "Redmond" 會讓 **Get-CsDialInConferencingAccessNumber** Cmdlet 傳回 "Redmond" 出現在相關聯地區清單中的所有號碼。例如傳回只將 Redmond 列為地區的存取號碼，以及同時將 Redmond 和 Portland 列為地區的存取號碼。

    Get-CsDialInConferencingAccessNumber -Region "Redmond"

## 範例 4

範例 4 會傳回與某個地區不相關 (也就是，Regions 屬性為空白) 的所有電話撥入式會議存取號碼。

    Get-CsDialInConferencingAccessNumber -Region $Null

## 範例 5

範例 5 所示的命令會傳回已被納入 USA 網站 (也就是 SiteId site:USA 的網站) 的所有電話撥入式會議存取號碼。

    Get-CsDialInConferencingAccessNumber -Region site:USA/Redmond

## 範例 6

範例 6 會使用 Filter 參數傳回 DisplayName 包含字串值 "Seattle" 之所有電話撥入式會議存取號碼的集合。篩選值 {DisplayName -like "\*Seattle\*"} 可將傳回的資料限制在 DisplayName 包含單字 "Seattle" (例如，Seattle Access Number；Dial-In Number for Seattle；Tacoma/Seattle Access Number 等) 的存取號碼。

    Get-CsDialInConferencingAccessNumber -Filter {DisplayName -like "*Seattle*"}

## 範例 7

範例 7 會傳回 Uri 行是以 tel:+1425 開頭的所有電話撥入式會議存取號碼；這可有效傳回區碼為 425 的所有美國存取號碼。為達成此目的，會呼叫 **Get-CsDialInConferencingAccessNumber** Cmdlet 搭配 Filter 參數；篩選值 {LineUri -like "tel:+1425\*"} 會將傳回的資料限制在開頭為字串值 "tel:+1425" 的 Uri 行。若要傳回區碼為 425 或區碼為 206 的所有電話號碼，請使用下列篩選值：

{LineUri -like "tel:+1425\*" -or LineUri -like "tel:+1206\*"}

    Get-CsDialInConferencingAccessNumber -Filter {LineUri -like "tel:+1425*"}

## 範例 8

範例 8 會傳回主要語言已設定為 Italian 的所有電話撥入式會議存取號碼集合。為了執行此工作，會先呼叫 **Get-CsDialInConferencingAccessNumber** Cmdlet，以傳回設定供組織使用之所有存取號碼的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這只會選取 PrimaryLanguage 屬性等於 Italian ("it-It") 的號碼。

    Get-CsDialInConferencingAccessNumber | Where-Object {$_.PrimaryLanguage -eq "it-IT"}

## 範例 9

範例 9 所示的命令會傳回已將 French 列為其中一個次要語言的所有電話撥入式會議存取號碼。為了執行此工作，會先呼叫不含任何參數的 **Get-CsDialInConferencingAccessNumber** Cmdlet，這會傳回設定供組織使用之存取號碼的完整集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這只會選取 SecondaryLanguages 屬性包含 French (fr-FR) 清單的號碼。

    Get-CsDialInConferencingAccessNumber  | Where-Object {$_.SecondaryLanguages -contains "fr-FR"}

## 詳細描述

電話撥入式會議讓使用者可以使用任何一種電話 (例如標準的「地面通訊」電話、行動電話或 Voice over Internet Protocol (VoIP) 電話) 加入線上會議的音訊部分。讓使用者即使沒有電腦或網際網路連線也可以參與會議。使用者可用完整的音訊功能：他們可以對其他參與者講話，聽到其他人所說的每句話。不過，還是看不到共用的投影片、視訊播放，或其他視覺元素。

若要為使用者提供電話撥入式會議的功能，您必須建立電話撥入式會議存取號碼：該使用者可撥入以連線至會議的電話號碼。電話撥入式會議存取號碼是以 **New-CsDialInConferencingAccessNumber** Cmdlet 建立。當您建立新的電話撥入式會議存取號碼時，實際上會在 Active Directory 網域服務 中建立新的連絡人物件；此連絡人物件可用來代表存取號碼及其所有屬性。您可以使用 **Get-CsDialInConferencingAccessNumber** Cmdlet 來擷取連絡人號碼。

如果您已從 Microsoft Office Communications Server 2007 匯入電話撥入式會議存取號碼，系統會藉由執行 **Get-CsDialInConferencingAccessNumber** Cmdlet 且包含 Region 參數，也擷取這些號碼 (除非您使用 Region 參數，否則系統不會顯示匯入的號碼)。但是，請注意，會有一則警告訊息顯示在匯入號碼的統一資源識別元 (URI) 旁邊。這只是 Cmdlet 處理匯入的電話撥入式會議存取號碼的方式。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsDialInConferencingAccessNumber** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsDialInConferencingAccessNumber"}

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
<td><p><em>EmptyRegion</em></p></td>
<td><p>必要</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回與區域相關聯的撥號對應表相關資訊，該區域與至少一組電話撥入式會議存取號碼無關聯。例如，假設 Bellevue 撥號對應表會與 Bellevue 地區產生關聯，但並未針對 Bellevue 地區設定任何存取號碼。因此 Bellevue 區域應被視為空白區域。</p>
<p>此參數無法和任何其他參數一起使用。</p></td>
</tr>
<tr class="even">
<td><p><em>Credential</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>可讓您以替代認證來執行 <strong>Get-CsDialInConferencingAccessNumber</strong> Cmdlet；如果您用來登入 Windows 的帳戶不具有使用連絡人物件所需的權限，可能就需要這一項。</p>
<p>若要使用 Credential 參數，您必須先使用 <strong>Get-Credential</strong> Cmdlet 來建立 PSCredential 物件。如需詳細資訊，請參閱 <strong>Get-Credential</strong> Cmdlet 說明主題。</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>可讓您連線至指定的網域控制站，以擷取連絡人資訊。若要連線至特定的網域控制站，請加入 DomainController 參數，後面加上電腦名稱 (例如，atl-mcs-001) 或其完整網域名稱 (例如，atl-mcs-001.litwareinc.com)。</p></td>
</tr>
<tr class="even">
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您篩選 Lync Server 的特定屬性來限制傳回的資料。例如，您可以將傳回的資料限制為在其顯示名稱中含字串值 &quot;Redmond&quot; 的電話撥入式會議號碼，或者使用 1-800 首碼的免付費電話撥入式會議號碼。</p>
<p>Filter 參數使用的 Windows PowerShell 篩選語法與 <strong>Where-Object</strong> Cmdlet 相同。例如，只會傳回首碼為 1-800 之存取號碼的篩選看起來如下：{LineUri -like &quot;tel:+1800*&quot;}，其中 withLineUri 代表 Active Directory 屬性、-like 代表比較運算子，而 &quot;tel:+1800*&quot; 代表篩選值。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>要擷取之電話撥入式會議存取號碼的 SIP 位址 (也就是，代表該號碼的連絡人物件)。指定 Identity 時，必須加上 &quot;sip:&quot;指定 Identity 時的首碼；例如：-Identity sip:RedmondDialIn@litwareinc.com。</p>
<p>若未指定此參數，則 <strong>Get-CsDialInConferencingAccessNumber</strong> Cmdlet 將傳回已設定要在組織內使用的所有電話撥入式會議存取號碼。</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>可讓您從特定 Active Directory 組織單位 (OU) 傳回存取號碼。這會包括來自指定 OU 及其任何子 OU 的資料。例如，如果 Finance OU 有兩個子 OU (即 AccountsPayable 和 AccountsReceivable)，則會從這三個 OU 中的每一個 OU 傳回存取號碼資訊。</p>
<p>指定 OU 時，請使用該容器的辨別名稱；例如：-OU &quot;OU=Finance,dc=litwareinc,dc=com&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>Region</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>傳回與指定撥號對應表地區相關聯的所有電話撥入式會議存取號碼。例如，若要傳回 Northwest 地區的所有撥入號碼，請使用下列語法：-Region Northwest。</p>
<p>您也可以藉由在參數值中包含範圍，傳回已被納入特定網站範圍 (或納入全域範圍) 的存取號碼。例如，若要傳回使用 Northwest 區域的存取號碼，且這些存取號碼已被納入 Redmond 網站的範圍，請使用下列語法：-Region site:Redmond/Northwest。請注意，參考網站範圍時，您必須使用 SiteId 屬性。您可以使用 <strong>Get-CsSite</strong> Cmdlet 來擷取 SiteId 值。</p>
<p>若要傳回與撥號對應表不相關的存取號碼清單，請將 Region 參數值設定為 $Null:-Region $Null。</p>
<p>請注意，如果指定此值，電話撥入式會議存取號碼僅會以其指派的優先順序傳回。優先順序與號碼出現在會議邀請及電話撥入式會議網頁上的順序相同。如需詳細資訊，請參閱 <a href="set-csdialinconferencingaccessnumber.md">Set-CsDialInConferencingAccessNumber</a> Cmdlet 說明主題。</p></td>
</tr>
<tr class="even">
<td><p><em>ResultSize</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>可讓您限制命令傳回的記錄數。例如，若只要傳回七個存取號碼 (不考慮樹系中有多少存取號碼)，只需加入 ResultSize 參數並將參數值設為 7。請注意，無法保證傳回哪七個項目。如果您將 ResultSize 設為 7，但樹系中只有三個存取號碼，則命令會傳回這三個號碼，然後完成執行而不會出現錯誤。</p>
<p>結果大小可以設為 0 和 2147483647 (含) 之間的任何數字。如果設為 0，命令會執行，但不會傳回資料。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

字串。**Get-CsDialInConferencingAccessNumber** Cmdlet 會接受代表存取號碼之 Identity 的字串值。

## 傳回類型

**Get-CsDialInConferencingAccessNumber** Cmdlet 會傳回 Microsoft.Rtc.Management.Xds.AccessNumber 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsDialInConferencingAccessNumber](new-csdialinconferencingaccessnumber.md)  
[Remove-CsDialInConferencingAccessNumber](remove-csdialinconferencingaccessnumber.md)  
[Set-CsDialInConferencingAccessNumber](set-csdialinconferencingaccessnumber.md)

