---
title: Set-CsAutodiscoverConfiguration
TOCTitle: Set-CsAutodiscoverConfiguration
ms:assetid: 06f59d62-b4dd-4b50-9cf3-40d6d41d74af
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh689980(v=OCS.15)
ms:contentKeyID: 49289988
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsAutodiscoverConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的自動探索服務組態設定集合。自動探索服務可讓 Lync Web App 或 Lync Mobile 等用戶端應用程式尋找主要資源 (例如使用者的主集區或 URL)，以加入電話撥入式會議。 Lync Server 2010：2011 年 11 月的累計更新中已導入此 Cmdlet。

## 語法

    Set-CsAutodiscoverConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsAutodiscoverConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-ExternalSipClientAccessFqdn <String>] [-ExternalSipClientAccessPort <UInt32>] [-Force <SwitchParameter>] [-WebLinks <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將新的自動探索 URL (http://LyncDiscover.fabrikam.com) 新增至指派給 Redmond 網站的自動探索組態設定。為達成此目的，範例中的第一個命令會使用 **New-CsWebLink** Cmdlet 建立新的自動探索 URL；該 URL 會以名稱為 $Link1 的變數儲存。第二個命令會使用 **Set-CsAutoDiscoverConfiguration** Cmdlet 將新的 URL 新增至指派給這些設定的 URL。作法是使用 WebLinks 參數和參數值 @{Add=$Link1}。

    $Link1 = New-CsWebLink -Token "Fabrikam" -Href "http://LyncDiscover.fabrikam.com"
    
    Set-CsAutoDiscoverConfiguration -Identity "site:Redmond" -WebLinks @{Add=$Link1}

## 範例 2

範例 2 所示的命令示範如何從自動探索服務組態設定集合中移除 URL。為達成此目的，集合中的第一個命令會擷取要刪除之 URL 的物件參照 (具有 Token 等於 "Fabrikam" 的 URL)。作法是先呼叫 **Get-CsAutoDiscoverConfiguration** Cmdlet，以擷取 Redmond 網站的自動探索服務設定。然後，此集合會管線傳送到 **Select-Object** Cmdlet，以使用 ExpandProperty 參數來「展開」WebLinks 屬性 (展開屬性時，可將 **Get-CsAutoDiscoverConfiguration** Cmdlet 存取權提供給儲存在該屬性的個別物件)。然後，這些 WebLinks 物件會管線傳送到 **Where-Object** Cmdlet，這會選取 Token 屬性等於 "Fabrikam" 的物件，並將該 WebLinks 物件儲存在名稱為 $Link1 的變數中。

接著，範例中的第二個命令會使用 **Set-CsAutoDiscoverConfiguration** Cmdlet 移除以 $Link1 儲存的物件。為達成此目的，命令會使用 WebLinks 參數和參數值 @{Remove=$Link1}。

    $Link1 = Get-CsAutoDiscoverConfiguration  -Identity "site:Redmond" | Select-Object -ExpandProperty WebLinks | Where-Object {$_.Token -eq "Fabrikam"}
    
    Set-CsAutoDiscoverConfiguration -Identity "site:Redmond" -WebLinks @{Remove=$Link1}

## 範例 3

範例 3 顯示如何取代現有的自動探索 URL 集合 (在本例中為單一 URL)。為了執行此工作，範例中的第一個命令會使用 **New-CsWebLink** Cmdlet，為 http://LyncDiscover.contoso.com 建立新的自動探索 URL；產生的 URL 會以名稱為 $Link2 的變數儲存。範例中的第二個命令接著會使用 **Set-CsAutoDiscoverConfiguration** Cmdlet 和 WebLinks 參數移除先前指派給 Redmond 網站的任何 URL，並以 http://LyncDiscover.contoso.com 的 URL 取代。為達成此目的，命令會使用取代方法，而不是新增或移除方法。

    $Link2 = New-CsWebLink -Token "Contoso" -Href "http://LyncDiscover.contoso.com"
    
    Set-CsAutoDiscoverConfiguration -Identity "site:Redmond" -WebLinks @{Replace=$Link2}

## 範例 4

範例 4 所示的命令會移除指派給 Redmond 網站的所有自動探索 URL。為達此目的，命令會將 WebLinks 屬性設為 Null 值。如此即可刪除任何先前指派給該屬性的任何 URL。

    Set-CsAutoDiscoverConfiguration -Identity "site:Redmond" -WebLinks $Null

## 詳細描述

為了讓用戶端應用程式有效地充分利用 Lync Server，這些應用程式必須知道主要 Lync Server 元件的位置。例如，已驗證的使用者必須能夠尋找其主集區；畢竟，這些使用者僅可由該主集區進行驗證。同樣地，未驗證的使用者必須能夠執行諸如尋找用於加入會議的 URL 等作業。

如果所有使用者都從組織防火牆後方登入，探索這些位置相對會是較簡單的工作。但是，此相對簡單的工作會隨使用者使用 Lync Mobile 或 Lync Web App 從外部位置存取系統，而變得愈來愈複雜。

特別是在分隔網域案例中；在這些案例中，組織的某些使用者具有 Lync Server 的內部部署版本帳戶，而其他使用者則具有 Office 365 帳戶。在此情況下，使用者帳戶可能位於不同的 Active Directory 樹系。這會造成問題：例如，如果美國地區使用者從歐洲登入，系統必須能夠辨識使用者的樹系，再將登入要求參照至適當的集區。

Lync Server：2011 年 11 月的累計更新版本即已導入自動探索服務來解決這些問題。當用戶端應用程式嘗試存取 Lync Server 時，自動探索服務會剖析用戶端 SIP 位址，然後將該要求重新導向至適當的集區。用戶端應用程式會透過將 HTTP 要求傳送至自動探索 URL 來連線至自動探索服務；系統管理員必須設定這些 URL，自動探索服務才可以運作 (請注意，除了設定 URL 之外，系統管理員也必須建立與這些 URL 對應的 DNS 記錄)。

自動探索 URL 會指派給自動探索服務組態設定。如此這些設定便可以套用至全域範圍或網站範圍。當您安裝 Lync Server 時，系統會為您建立一組通用的設定集合 (但是不會將自動探索 URL 指派給該集合)。如果單一自動探索設定集合不符合需求，則可以使用 **New-CsAutoDiscoverConfiguration** Cmdlet 在網站範圍建立其他組態設定。接著，您可以使用 **Set-CsAutoDiscoverConfiguration** Cmdlet，從全域集合或任何網站範圍集合新增或移除自動探索 URL。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsAutoDiscoverConfiguration** Cmdlet：RTCUniversalServerAdmins。

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
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalSipClientAccessFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>用於外部用戶端存取之伺服器的完整網域名稱 (FQDN)。</p></td>
</tr>
<tr class="odd">
<td><p><em>ExternalSipClientAccessPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>用於外部用戶端存取的連接埠。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要修改之自動探索組態設定集合的唯一識別碼。若要修改全域集合，請使用下列語法：</p>
<p>-Identity &quot;global&quot;</p>
<p>若要修改在網站範圍設定的集合，請使用類似下列的語法：</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>如果未指定此參數，則 <strong>Set-CsAutoDiscoverConfiguration</strong> Cmdlet 將會自動修改全域設定。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>AutoDiscoverConfiguration 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>WebLinks</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>自動探索 URL 的集合。這些 URL 必須使用 <strong>New-CsWebLink</strong> Cmdlet 建立。</p></td>
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

**Set-CsAutoDiscoverConfiguration** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WriteableConfig.Settings.AutoDiscoverConfiguration.AutoDiscoverConfiguration 物件輸入。

## 傳回類型

無。反之， **Set-CsAutoDiscoverConfiguration** Cmdlet 會修改 Microsoft.Rtc.Management.WriteableConfig.Settings.AutoDiscoverConfiguration.AutoDiscoverConfiguration 物件的執行個體。

