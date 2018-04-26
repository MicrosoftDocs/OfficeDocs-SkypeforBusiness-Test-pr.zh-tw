---
title: Remove-CsAutodiscoverConfiguration
TOCTitle: Remove-CsAutodiscoverConfiguration
ms:assetid: f7cda472-c23b-4eb9-b45b-b9353b93e1df
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690054(v=OCS.15)
ms:contentKeyID: 49292851
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsAutodiscoverConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除自動探索組態設定集合。自動探索服務可讓 Lync Web App 之類的用戶端應用程式尋找主要資源 (例如使用者的主集區或 URL)，以加入電話撥入式會議。Lync Server 2010：2011 年 11 月的累計更新中已導入此 Cmdlet。

## 語法

    Remove-CsAutodiscoverConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會刪除 Redmond 網站的自動探索組態設定。

    Remove-CsAutoDiscoverConfiguration -Identity "site:Redmond"

## 範例 2

範例 2 會移除指派給網站範圍的所有自動探索組態設定。為達成此目的，命令會先使用 **Get-CsAutoDiscoverConfiguration** Cmdlet 搭配 Filter 參數，以傳回組態設定集合；篩選值 "site:\*" 可確保只會傳回 Identity 開頭為字串值 "site:" 的設定。然後再將篩選後的集合管線傳送給 **Remove-CsAutoDiscoverConfiguration** Cmdlet，以刪除集合中的每個項目。

    Get-CsAutoDiscoverConfiguration -Filter "site:*" | Remove-CsAutoDiscoverConfiguration

## 詳細描述

為了讓用戶端應用程式有效地充分利用 Lync Server，這些應用程式必須知道主要 Lync Server 元件的位置。例如，已驗證的使用者必須能夠尋找其主集區；畢竟，這些使用者僅可由該主集區進行驗證。同樣地，未驗證的使用者必須能夠執行諸如尋找用於加入會議的 URL 等作業。

如果所有使用者都從組織防火牆後方登入，探索這些位置相對會是較簡單的工作。但是，此相對簡單的工作會隨使用者使用 Lync Web App 等應用程式從外部位置存取系統，而變得愈來愈複雜。

特別是在分隔網域案例中；在這些案例中，組織的某些使用者具有 Lync Server 的內部部署版本帳戶，而其他使用者則具有 商務用 Skype Online 帳戶。在此情況下，使用者帳戶可能位於不同的 Active Directory 樹系。這會造成問題：例如，如果美國地區使用者從歐洲登入，系統必須能夠辨識使用者的樹系，再將登入要求參照至適當的集區。

Lync Server：2011 年 11 月的累計更新版本即已導入自動探索服務來解決這些問題。當用戶端應用程式嘗試存取 Lync Server 時，自動探索服務會剖析用戶端 SIP 位址，然後將該要求重新導向至適當的集區。用戶端應用程式會透過將 HTTP 要求傳送至自動探索 URL 來連線至自動探索服務；系統管理員必須設定這些 URL，自動探索服務才可以運作 (請注意，除了設定 URL 之外，系統管理員也必須建立與這些 URL 對應的 DNS 記錄)。

會將自動探索 URL 指派給自動探索組態設定；接著，可以將這些設定套用至全域範圍或網站範圍。如果您稍後決定要移除指派給網站範圍的設定，可以執行 **Remove-CsAutoDiscoverConfiguration** Cmdlet。請注意，您也可以對全域設定執行此 Cmdlet。但在此情況下，並不會移除全域設定，而是會刪除指派給全域集合的自動探索 URL。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsAutoDiscoverConfiguration** Cmdlet：RTCUniversalServerAdmins。

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要移除之自動探索設定的唯一識別碼。您可以在全域範圍或網站範圍設定自動探索設定。若要移除全域原則，請使用這個語法：-Identity global (請注意，系統不會實際移除全域設定，而是將全域設定中的所有屬性重設為其預設值)。</p>
<p>若要移除在此網站範圍設定的設定，請使用類似下列的語法：</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>請注意，指定 Identity 時不得使用萬用字元。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
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

Microsoft.Rtc.Management.WriteableConfig.Settings.AutoDiscoverConfiguration.AutoDiscoverConfiguration。**Remove-CsAutoDiscoverConfiguration** Cmdlet 接受管線傳送的 AutoDiscoverConfiguration 物件輸入。

## 傳回類型

無。而是由 Cmdlet 刪除 Microsoft.Rtc.Management.WriteableConfig.Settings.AutoDiscoverConfiguration.AutoDiscoverConfiguration 物件的執行個體。

