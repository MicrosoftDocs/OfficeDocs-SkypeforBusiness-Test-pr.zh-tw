---
title: New-CsAutodiscoverConfiguration
TOCTitle: New-CsAutodiscoverConfiguration
ms:assetid: 6b878b0e-f0c0-46a2-99b8-fd2105250600
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690022(v=OCS.15)
ms:contentKeyID: 49291225
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsAutodiscoverConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

在網站範圍建立新的自動探索組態設定集合。自動探索服務可讓 Lync Web App 或 Microsoft Lync Mobile 等用戶端應用程式尋找主要資源 (例如使用者的主集區或 URL)，以加入電話撥入式會議。 Lync Server 2010：2011 年 11 月的累計更新中已導入此 Cmdlet。

## 語法

    New-CsAutodiscoverConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-ExternalSipClientAccessFqdn <String>] [-ExternalSipClientAccessPort <UInt32>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WebLinks <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會為 Redmond 網站建立新的自動探索組態設定集合。由於未加上 WebLinks 參數，因此這些設定不會包含任何自動探索 URL。

    New-CsAutoDiscoverConfiguration -Identity "site:Redmond"

## 範例 2

範例 2 所示的命令會為 Redmond 網站建立新的自動探索組態設定集合，並將一組自動探索 URL 指派給這些新設定：http://LyncDiscover.fabrikam.com 和 http://LyncDiscoverInternal.fabrikam.com。為了執行此工作，前兩個命令會使用 **New-CsWebLink** Cmdlet 建立兩個自動探索 URL，並將新建立的 URL 儲存在名為 $Link1 和 $Link2 的變數中。建立這兩個 URL 之後，第三個命令會使用 **New-CsAutoDiscoverConfiguration** Cmdlet 建立新的自動探索組態設定。若要將這兩個 URL 指派給這些設定，必須加上 WebLinks 參數並搭配參數值 @{Add=$Link1,$Link2}。該語法會將儲存在變數 $Link1 和 $Link2 中的值新增至 WebLinks 屬性。

    $Link1 = New-CsWebLink -Token "Fabrikam" -Href "http://LyncDiscover.fabrikam.com"
    $Link2 = New-CsWebLink -Token "Fabrikam" -Href "http://LyncDiscoverInternal.fabrikam.com"
    
    New-CsAutoDiscoverConfiguration -Identity "site:Redmond" -WebLinks @{Add=$Link1,$Link2}

## 詳細描述

為了讓用戶端應用程式有效地充分利用 Lync Server，這些應用程式必須知道主要 Lync Server 元件的位置。例如，已驗證的使用者必須能夠尋找其主集區；畢竟，這些使用者僅可由該主集區進行驗證。同樣地，未驗證的使用者必須能夠執行諸如尋找用於加入會議的 URL 等作業。

如果所有使用者都從組織防火牆後方登入，探索這些位置相對會是較簡單的工作。但是，此相對簡單的工作會隨使用者使用 Microsoft Lync Mobile 或 Lync Web App 從外部位置存取系統，而變得愈來愈複雜。

特別是在分隔網域案例中；在這些案例中，組織的某些使用者具有 Lync Server 的內部部署版本帳戶，而其他使用者則具有 商務用 Skype Online 帳戶。在此情況下，使用者帳戶可能位於不同的 Active Directory 樹系。這會造成問題：例如，如果美國地區使用者從歐洲登入，系統必須能夠辨識使用者的樹系，再將登入要求參照至適當的集區。

Lync Server：2011 年 11 月的累計更新版本即已導入自動探索服務來解決這些問題。當用戶端應用程式嘗試存取 Lync Server 時，自動探索服務會剖析用戶端 SIP 位址，然後將該要求重新導向至適當的集區。用戶端應用程式會透過將 HTTP 要求傳送至自動探索 URL 來連線至自動探索服務；系統管理員必須設定這些 URL，自動探索服務才可以運作 (請注意，除了設定 URL 之外，系統管理員也必須建立與這些 URL 對應的 DNS 記錄)。

會將自動探索 URL 指派給自動探索組態設定；接著，可以將這些設定套用至全域範圍或網站範圍。當您安裝 Lync Server 時，系統會為您建立一組全域設定集合 (但是不會將自動探索 URL 指派給該集合)。如果單一自動探索設定集合不符合需求，則可以使用 **New-CsAutoDiscoverConfiguration** Cmdlet 在網站範圍建立其他組態設定。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsAutoDiscoverConfiguration** Cmdlet：RTCUniversalServerAdmins。

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
<td><p>要修改之自動探索組態設定集合的唯一識別碼。若要建立在網站範圍設定的集合，請使用類似下列的語法：</p>
<p>-Identity &quot;site:Redmond&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>ExternalSipClientAccessFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>用於外部用戶端存取之伺服器的完整網域名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalSipClientAccessPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>用於外部用戶端存取的連接埠。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照，但不實際將物件認可為永久變更。如果您將利用此參數呼叫之命令的輸出指派給變數，則可變更物件參照的屬性，然後呼叫 <strong>Set-CsAutoDiscoverConfiguration</strong> Cmdlet 來認可這些變更。</p></td>
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

**New-CsAutoDiscoverConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

建立 Microsoft.Rtc.Management.WriteableConfig.Settings.AutoDiscoverConfiguration.AutoDiscoverConfiguration 物件的新執行個體。

