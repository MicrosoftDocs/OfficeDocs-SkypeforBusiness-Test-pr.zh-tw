---
title: Get-CsAutodiscoverConfiguration
TOCTitle: Get-CsAutodiscoverConfiguration
ms:assetid: 221d26d6-0f77-4873-8872-d600913eb98b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690014(v=OCS.15)
ms:contentKeyID: 49290325
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAutodiscoverConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織目前所使用之自動探索組態設定的資訊。自動探索服務可讓 Lync Web App 等用戶端應用程式尋找主要資源 (例如使用者的主集區或 URL)，以加入電話撥入式會議。Lync Server 2010：2011 年 11 月的累計更新中已導入此 Cmdlet。

## 語法

    Get-CsAutodiscoverConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsAutodiscoverConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回組織目前使用的所有自動探索組態設定。

    Get-CsAutoDiscoverConfiguration

## 範例 2

在範例 2 中只會傳回自動探索組態設定的一個集合：全域集合。

    Get-CsAutoDiscoverConfiguration -Identity "global"

## 範例 3

範例 3 所示的命令會傳回指派給網站範圍的所有自動探索組態設定。為達此目的，命令會加上 Filter 參數搭配篩選值 "site:\*" (此篩選值可確保只會傳回 Identity 開頭為 "site:" 字串值的設定)。根據定義，Identity 開頭為 "site:" 的設定都是在網站範圍設定的設定。

    Get-CsAutoDiscoverConfiguration -Filter "site:*"

## 範例 4

範例 4 所示的命令會傳回所有包含 fabrikam.com 之自動探索 URL 的自動探索組態設定。為了執行此工作，命令會先使用 **Get-CsAutoDiscoverConfiguration** Cmdlet 傳回組織目前所使用之所有自動探索設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 WebLinks 屬性包含字串值 "fabrikam.com" 的設定。

    Get-CsAutoDiscoverConfiguration | Where-Object {$_.WebLinks -like "*fabrikam.com"}

## 詳細描述

為了讓用戶端應用程式有效地充分利用 Lync Server，這些應用程式必須知道主要 Lync Server 元件的位置。例如，已驗證的使用者必須能夠尋找其主集區；畢竟，這些使用者僅可由該主集區進行驗證。同樣地，未驗證的使用者必須能夠執行諸如尋找用於加入會議的 URL 等作業。

如果所有使用者都從組織防火牆後方登入，探索這些位置相對會是較簡單的工作。但是，此相對簡單的工作會隨使用者使用 Lync Web App 等應用程式從外部位置存取系統，而變得愈來愈複雜。

特別是在分隔網域案例中；在這些案例中，組織的某些使用者具有 Lync Server 的內部部署版本帳戶，而其他使用者則具有 商務用 Skype Online 帳戶。在此情況下，使用者帳戶可能位於不同的 Active Directory 樹系。這會造成問題：例如，如果美國地區使用者從歐洲登入，系統必須能夠辨識使用者的樹系，再將登入要求參照至適當的集區。

Lync Server：2011 年 11 月的累計更新版本即已導入自動探索服務來解決這些問題。當用戶端應用程式嘗試存取 Lync Server 時，自動探索服務會剖析用戶端 SIP 位址，然後將該要求重新導向至適當的集區。用戶端應用程式會透過將 HTTP 要求傳送至自動探索 URL 來連線至自動探索服務；系統管理員必須設定這些 URL，自動探索服務才可以運作 (請注意，除了設定 URL 之外，系統管理員也必須建立與這些 URL 對應的 DNS 記錄)。

會將自動探索 URL 指派給自動探索組態設定；接著，可以將這些設定套用至全域範圍或網站範圍。**Get-CsAutoDiscoverConfiguration** Cmdlet 可傳回組織目前所使用的自動探索設定 (和自動探索 URL) 資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsAutoDiscoverConfiguration** Cmdlet：RTCUniversalServerAdmins。

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
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您在指定要傳回之自動探索組態設定的 Identity 時使用萬用字元。例如，此語法會傳回在網站範圍設定的所有設定：</p>
<p>-Filter &quot;site:*&quot;</p>
<p>請注意，您不能在同一個命令中同時使用 Identity 和 Filter 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要擷取之自動探索組態設定集合的唯一識別碼。若要擷取全域設定，請使用下列語法：</p>
<p>-Identity &quot;global&quot;</p>
<p>若要擷取在網站範圍內所做的設定，請使用類似下列的語法：</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>若未加入此參數，<strong>Get-CsAutoDiscoverConfiguration</strong> Cmdlet 會傳回組織目前所使用之所有自動探索組態設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取自動探索組態資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

**Get-CsAutoDiscoverConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsAutoDiscoverConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WriteableConfig.Settings.AutoDiscoverConfiguration.AutoDiscoverConfiguration 物件的執行個體。

