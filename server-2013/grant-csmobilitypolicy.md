---
title: Grant-CsMobilityPolicy
TOCTitle: Grant-CsMobilityPolicy
ms:assetid: c5ca6d6c-e442-4375-b8fd-1016a0aef33b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690038(v=OCS.15)
ms:contentKeyID: 49292263
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsMobilityPolicy

 

_**上次修改主題的時間：** 2015-03-09_

將個別使用者行動原則授與使用者或使用者群組。行動原則可判斷使用者能否使用 Lync Mobile。除此之外，也能管理使用者是否可以使用 \[從公司撥號\]，在其行動電話上使用公司電話號碼，而不使用自己的行動電話號碼撥打及接聽電話。行動原則也可以在撥號或接聽來電時用來要求 Wi-Fi 連線。Lync Server 2010：2011 年 11 月的累計更新中已導入此 Cmdlet。

## 語法

    Grant-CsMobilityPolicy -Identity <UserIdParameter> -PolicyName <String> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將個別使用者行動原則 RedmondMobilityPolicy 指派給單一使用者：Ken Myer。

    Grant-CsMobilityPolicy -Identity "Ken Myer" -PolicyName "RedmondMobilityPolicy"

## 範例 2

範例 2 會將行動原則 RedmondMobilityPolicy 指派給目前由原則 NorthAmericaMobilityPolicy 管理的使用者。為達此目的，命令會先使用 **Get-CsUser** Cmdlet 搭配 Filter 參數，以擷取獲指派原則 NorthAmericaMobilityPolicy 的所有使用者；作法是利用篩選值 {MobilityPolicy –eq "NorthAmericaMobilityPolicy"}。擷取使用者帳戶集合之後，會將這些帳戶管線傳送給 **Grant-CsMobilityPolicy** Cmdlet，以將原則 RedmondMobilityPolicy 指派給每位使用者。

    Get-CsUser -Filter {MobilityPolicy -eq "NorthAmericaMobilityPolicy"} | Grant-CsMobilityPolicy -PolicyName "RedmondMobilityPolicy"

## 範例 3

範例 3 會將 RedmondMobilityPolicy 行動原則指派給位於 Redmond 城市的所有使用者。為了執行此工作，命令會先呼叫 **Get-CsUser** Cmdlet 搭配 LdapFilter 參數；篩選值 "l=Redmond" 可傳回位於 Redmond 的所有使用者 ("l" 表示 Active Directory 屬性 "locality")。擷取使用者帳戶之後，會將這些帳戶管線傳送到 **Grant-CsMobilityPolicy** Cmdlet；然後 **Grant-CsMobilityPolicy** Cmdlet 會將 RedmondMobilityPolicy 原則指派給每一位使用者。

    Get-CsUser -LdapFilter "l=Redmond" | Grant-CsMobilityPolicy -PolicyName "RedmondMobilityPolicy"

## 範例 4

範例 4 會將 RedmondMobilityPolicy 指派給 Lync Server 帳戶位於 atl-cs-001.litwareinc.com 的使用者。為達此目的，命令會先使用 **Get-CsUser** Cmdlet 搭配 Filter 參數，以擷取位於指定登錄器集區的所有使用者帳戶；作法是利用篩選值 {RegistrarPool –eq "atl-cs-001.litwareinc.com"}。擷取使用者帳戶集合之後，會將這些帳戶管線傳送給 **Grant-CsMobilityPolicy** Cmdlet，以將原則 RedmondMobilityPolicy 指派給每位使用者。

    Get-CsUser -Filter {RegistrarPool -eq "atl-cs-001.litwareinc.com"} | Grant-CsMobilityPolicy -PolicyName "RedmondMobilityPolicy"

## 詳細描述

Lync Mobile 是可讓使用者在行動電話上執行 Lync 的用戶端應用程式。\[從公司撥號\] 可讓使用者在行動電話上撥打電話，但是將此通話顯示為從公司電話號碼 (而不是行動電話號碼) 撥出的通話。啟用 \[從公司撥號\] 的使用者可以直接從其行動電話撥號，或透過 \[電話撥出式會議\] 選項來達成此目的。透過電話撥出式會議，使用者實際上是要求 Mobility Service 伺服器代為撥打電話。伺服器會建立通話，然後回撥給使用者的行動電話。在使用者接聽之後，伺服器會接著撥打給受話方。您可以使用行動原則來管理這兩個功能。

透過 Lync Server 2013，行動裝置可以使用標準行動電話網路或 Wi-Fi 連線來撥打或接聽電話。行動原則可用於要求 Wi-Fi 連線，以避免透過行動電話網路進行通話。

當您安裝 Lync Server 時，即會有套用到所有使用者的單一全域行動性原則。但是，系統管理員可以使用 **New-CsMobilityPolicy** Cmdlet，在網站範圍或個別使用者範圍建立自訂原則。

如果您在網站範圍建立新原則，即會自動將該原則指派給適當的網站。但是，如果您在個別使用者範圍建立行動原則，雖原則會存在，但不會自動指派給任何使用者。相反地，您必須使用 **Grant-CsMobilityPolicy** Cmdlet 將個別使用者原則明確指派給一或多位使用者。

請注意，當您執行 **Get-CsUser** Cmdlet 時，預設不會顯示行動原則。因此執行類似下列的命令時，無法看見指派給使用者的個別使用者行動原則：

Get-CsUser "Ken Myer"

相反地，您必須使用類似如下的命令，才可以看見使用者的所有屬性值 (包括行動原則)：

Get-CsUser "Ken Myer" | Select-Object \*

或者，您可以使用類似如下的命令，僅檢視使用者的顯示名稱和行動原則：

Get-CsUser "Ken Myer" | Select-Object DisplayName, MobilityPolicy

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Grant-CsMobilityPolicy** Cmdlet：RTCUniversalServerAdmins。

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
<td><p>表示要指派個別使用者行動原則的使用者帳戶 Identity。通常可以使用下列四種格式的其中一種來指定使用者識別：1) 使用者的 SIP 位址；2) 使用者的使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (例如 litwareinc\kenmyer)；4) 使用者的 Active Directory 顯示名稱 (例如 Ken Myer)。也可以使用使用者的 Active Directory 辨別名稱來指定使用者識別。</p>
<p>此外，使用顯示名稱做為使用者 Identity 時，可以使用星號 (*) 萬用字元。例如，若 Identity 為 &quot;* Smith&quot;，則會將原則指派給所有顯示名稱結尾為字串值 &quot; Smith&quot; 的使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>PolicyName</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要指派之原則的「名稱」。簡單來說，PolicyName 是原則 Identity 減去原則範圍 (&quot;tag:&quot; 首碼)。例如，Identity 為 tag:Redmond 的原則擁有與 Redmond 相等的 PolicyName；而 Identity 為 tag:RedmondUsersMobilityPolicy 的原則則擁有與 RedmondUsersMobilityPolicy 相等的 PolicyName。若要指派個別使用者原則，請使用類似下列的語法：</p>
<p>-PolicyName RedmondUsersMobilityPolicy</p>
<p>若要取消指派先前已指派給使用者的個別使用者原則，請將 PolicyName 設定為 Null 值 ($Null)：</p>
<p>-PolicyName $Null</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>允許在指派新原則時，指定要連線網域控制站的完整網域名稱 (FQDN)。如果未指定此參數，則 <strong>Grant-CsMobilityPolicy</strong> Cmdlet 將連絡第一個可用的網域控制站。</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>可讓您透過代表已指派原則之使用者的管線來傳遞使用者物件。根據預設，<strong>Grant-CsMobilityPolicy</strong> Cmdlet 不會透過管線傳遞任何物件。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>描述執行命令後的結果，但無須實際執行命令。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

**Grant-CsMobilityPolicy** Cmdlet 接受代表使用者帳戶 Identity 之字串值的管線傳送輸入。Cmdlet 也接受管線傳送的使用者物件輸入。

## 傳回類型

根據預設，**Grant-CsMobilityPolicy** Cmdlet 不會傳回任何物件或值。但是，如果加入 PassThru 參數，Cmdlet 會管線傳送 Microsoft.Rtc.Management.ADConnect.Schema.OCSUserOrAppContact 物件的執行個體。

