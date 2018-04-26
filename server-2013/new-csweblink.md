---
title: New-CsWebLink
TOCTitle: New-CsWebLink
ms:assetid: f5c19896-4ce0-42cd-a934-30b1cdc64e3a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690053(v=OCS.15)
ms:contentKeyID: 49292826
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsWebLink

 

_**上次修改主題的時間：** 2015-03-09_

建立新 Web 連結指向自動探索服務。自動探索服務可讓 Lync Web App 或 Lync Mobile 等用戶端應用程式尋找主要資源 (例如使用者的主集區或 URL)，以加入電話撥入式會議。Lync Server 2010：2011 年 11 月的累計更新中已導入此 Cmdlet。

## 語法

    New-CsWebLink -Href <String> -Token <String>

## 範例

## 範例 1

範例 1 所示的命令會將新的自動探索 URL (http://LyncDiscover.fabrikam.com) 新增至指派給 Redmond 網站的自動探索組態設定。為達成此目的，範例中的第一個命令會使用 **New-CsWebLink** Cmdlet 建立新的自動探索 URL；該 URL 會以名稱為 $Link1 的變數儲存。接著會使用 **Set-CsAutoDiscoverConfiguration** Cmdlet 將新的 URL 新增至已指派給這些設定的任何 URL。作法是使用 WebLinks 參數和參數值 @{Add=$Link1}。

    $Link1 = New-CsWebLink -Token "Fabrikam" -Href "http://LyncDiscover.fabrikam.com"
    
    Set-CsAutoDiscoverConfiguration -Identity "site:Redmond" -WebLinks @{Add=$Link1}

## 範例 2

範例 2 的命令會將一組自動探索 URL (http://LyncDiscover.fabrikam.com 和 http://LyncDiscoverInternal.fabrikam.com) 指派給指定給 Redmond 網站的自動探索組態設定。為達此目的，前兩個命令會使用 **New-CsWebLink** Cmdlet 建立兩個自動探索 URL；然後將新建立的 URL 儲存在名為 $Link1 和 $Link2 的變數中。建立這兩個 URL 之後，第三個命令會使用 **Set-CsAutoDiscoverConfiguration** Cmdlet 將這兩個 URL 指派給 Redmond 網站。為達成此目的，會加上 WebLinks 參數搭配參數值 @{Add=$Link1,$Link2}。該語法會將儲存在變數 $Link1 和 $Link2 中的值新增至設定的 WebLinks 屬性中。

    $Link1 = New-CsWebLink -Token "Fabrikam" -Href "http://LyncDiscover.fabrikam.com"
    $Link2 = New-CsWebLink -Token "Fabrikam" -Href "http://LyncDiscoverInternal.fabrikam.com"
    
    Set-CsAutoDiscoverConfiguration -Identity "site:Redmond" -WebLinks @{Add=$Link1,$Link2}

## 詳細描述

為了讓用戶端應用程式有效地充分利用 Lync Server，這些應用程式必須知道主要 Lync Server 元件的位置。例如，已驗證的使用者必須能夠尋找其主集區；畢竟，這些使用者僅可由該主集區進行驗證。同樣地，未驗證的使用者必須能夠執行諸如尋找用於加入會議的 URL 等作業。

如果所有使用者都從組織防火牆後方登入，探索這些位置相對會是較簡單的工作。但是，此相對簡單的工作會隨使用者使用 Lync Mobile 或 Lync Web App 從外部位置存取系統，而變得愈來愈複雜。

特別是在分隔網域案例中；在這些案例中，組織的某些使用者具有 Lync Server 的內部部署版本帳戶，而其他使用者則具有 Microsoft Office 365 帳戶。在此情況下，使用者帳戶可能位於不同的 Active Directory 樹系。這會造成問題：例如，如果美國地區使用者從歐洲登入，系統必須能夠辨識使用者的樹系，再將登入要求參照至適當的集區。

在 2011 年 11 月發行的 Lync Server 版本中，已引進自動探索服務來解決這些問題。當用戶端應用程式嘗試存取 Lync Server 時，自動探索服務會剖析用戶端 SIP 位址，然後將該要求重新導向至適當的集區。用戶端應用程式會透過將 HTTP 要求傳送至自動探索 URL 來連線至自動探索服務；系統管理員必須設定這些 URL，自動探索服務才可以運作 (請注意，除了設定 URL 之外，系統管理員也必須建立與這些 URL 對應的 DNS 記錄)。

會將自動探索 URL 指派給自動探索組態設定；接著，可以將這些設定套用至全域範圍或網站範圍。當您安裝 Lync Server 時，系統會為您建立一組全域設定集合 (但是不會將自動探索 URL 指派給該集合)。如果單一自動探索設定集合不符合需求，則可以使用 **New-CsAutoDiscoverConfiguration** Cmdlet 在網站範圍建立其他組態設定。

管理自動探索組態設定通常是指新增自動探索 URL。這些 URL 必須使用 **New-CsWebLink** Cmdlet 建立，且產生的 URL 會儲存在變數中，再新增至自動探索組態設定集合。自動探索 URL 會以組織使用的 SIP 網域為基礎；系統管理員通常會建立一個 URL (例如 http://LyncDiscover.litwareinc.com)，以供組織防火牆外部的使用者使用，並建立第二個 URL (例如 http://LyncDiscoverInternal.litwareinc.com)，以供防火牆內部的使用者使用。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsWebLink** Cmdlet：RTCUniversalServerAdmins。

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
<td><p><em>Href</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>自動探索服務的 URL。例如：</p>
<p>–Href &quot;http://LyncDiscover.fabrikam.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Token</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>指定給 URL 的唯一名稱。例如：</p>
<p>-Token &quot;Fabrikam&quot;</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsWebLink** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

建立 Microsoft.Rtc.Management.WriteableConfig.Settings.WebLink.WebLink 物件的新執行個體。

