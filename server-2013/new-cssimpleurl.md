---
title: New-CsSimpleUrl
TOCTitle: New-CsSimpleUrl
ms:assetid: 0dcf919e-9896-4428-8f12-0fc611661fa8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398180(v=OCS.15)
ms:contentKeyID: 49290081
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsSimpleUrl

 

_**上次修改主題的時間：** 2015-03-09_

建立簡單的新 URL，然後加入簡單 URL 組態集合中。簡單 URL 可以方便使用者加入會議，以及方便系統管理員登入 Lync Server 控制台。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsSimpleUrl -Component <String> -Domain <String> [-ActiveUrl <String>] [-SimpleUrlEntry <PSListModifier>]

## 範例

## 範例 1

範例 1 顯示如何將新的 URL 新增至簡單 URL 的現有集合中。首先，範例中的第一個命令會使用 **New-CsSimpleUrlEntry** Cmdlet，建立指向 https://meet.fabrikam.com 的 URL 項目；此 URL 項目會儲存在名為 $urlEntry 的變數中。

在第二個命令中，**New-CsSimpleUrl** Cmdlet 用於僅在記憶體中建立簡單 URL 的執行個體。在此範例中，URL 元件設為 Meet；網域設為 fabrikam.com；ActiveUrl 設為 https://meet.fabrikam.com；SimpleUrl 屬性設為 $urlEntry，而 $urlEntry 是第一個命令中建立的 URL 項目。

在 URL 建立 (並儲存在物件參考 $simpleUrl 中) 後，範例中的最後一個命令會將新的 URL 新增至 Redmond 網站的簡單 URL 集合。這可以透過使用 **Set-CsSimpleUrlConfiguration** Cmdlet、SimpleUrl 參數和參數值 @{Add=$simpleUrl} 完成。此語法會使儲存在物件參考 $simpleUrl 中的 URL 新增至 SimpleUrl 屬性。

    $urlEntry = New-CsSimpleUrlEntry -Url "https://meet.fabrikam.com"
    $simpleUrl = New-CsSimpleUrl -Component "meet" -Domain "fabrikam.com" -SimpleUrlEntry $urlEntry -ActiveUrl "https://meet.fabrikam.com"
    Set-CsSimpleUrlConfiguration -Identity "site:Redmond" -SimpleUrl @{Add=$simpleUrl}

## 詳細描述

在 Microsoft Office Communications Server 2007 R2 中，會議具有類似下列的 URL：

https://imdf.litwareinc.com/Join?uri=sip%3Akenmyer%40litwareinc.com%3Bgruu%3Bopaque%3Dapp%3Aconf%3Afocus%3Aid%3A125f95a0b0184dcea706f1a0191202a8\&key=EcznhLh5K5t

不過，這種 URl 不是很直覺，不容易傳達給其他人。Lync Server 2010 中採用的簡單 URL 提供類似下列的 URL 給使用者，有助於克服這些問題：

https://meet.litwareinc.com/kenmyer/071200

Simple URL 為 Office Communications Server 中使用的 URL 進行改進。但是系統不會自動建立簡單 URL；而是您必須自行設定 URL。此外，您還必須執行其他動作，例如建立每個 URL 的網域名稱系統 (DNS) 記錄、設定外部存取的反向 Proxy 規則、將簡單 URL 新增至前端伺服器憑證等。

Lync Server 可讓您建立三個不同的簡單 URL：

Meet – 用於會議。您的每個 SIP 網域都必須至少有一個 Meet URL。

Admin – 用於將系統管理員指向 Lync Server 控制台。

Dialin – 用於電話撥入式會議網頁。

簡單 URL 儲存在簡單 URL 組態集合中。當您安裝 Lync Server 後，系統會建立全域集合，您也可以在網站範圍建立自訂集合。這讓您能夠在每個網站使用不同的簡單 URL。

若要將實際 URL 新增至簡單 URL 集合，您必須先使用 **New-CsSimpleUrl** Cmdlet 和 **New-CsSimpleUrlEntry** Cmdlet 來建立 URL。**New-CsSimpleUrlEntry** Cmdlet 會建立一個 URL 項目：可當做簡單 URL (用於會議、管理或電話撥入式會議) 使用的 URL (例如 https://meet.litwareinc.com)。由 **New-CsSimpleUrlEntry** Cmdlet 建立的物件便會新增至新簡單 URL 的 SimpleUrlEntry 屬性。您必須使用個別的 Cmdlet 來建立物件，因為 SimpleUrlEntry 屬性可以保留多個 URL (不過，只有一個這類的 URL 可以被指定為使用中的 URL。使用中的 URL 代表用於會議、管理或電話撥入式會議的實際 URL)。

建立簡單 URL 項目後，接下來您可以使用 **New-CsSimpleUrl** Cmdlet，僅在記憶體中建立簡單 URL 執行個體，並將其定義為元件 (簡單 URL 的類型)、網域、使用中的 URL，以及所有簡單 URL 項目。在您建立代表簡單 URL 的物件後，可以將該物件新增至新 (或現有) 的簡單 URL 集合。更新簡單 URL 後，接著您必須執行 **Enable-CsComputer** Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsSimpleUrl** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsSimpleUrl\\b"}

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
<td><p><em>Component</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>表示要建立之簡單 URL 的類型。有效值為：</p>
<p>Meet – 用於管理會議的 URL。</p>
<p>Admin – 指向 Lync Server 控制台的 URL。</p>
<p>Dialin – 用於電話撥入式會議的 URL。</p>
<p>例如：-Component &quot;Meet&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Domain</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>簡單 URL 的 SIP 網域。例如：-Domain &quot;litwareinc.com&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>ActiveUrl</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>表示使用者實際存取的 URL。SimpleUrlEntry 屬性可以包含多個 URL，但是在指定的時間內只有其中一個 URL 會在使用中。如果您嘗試將 ActiveUrl 設為在 SimpleUrlEntry 屬性中找不到的值，就會發生錯誤。</p>
<p>若要指派使用中的 URL，只要使用 URL 本身做為參數值即可。例如：-ActiveUrl https://meet.litwareinc.com&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>SimpleUrlEntry</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>指定元件之 URL 的集合。例如，https://meet.litwareinc.com 和 https://litwareinc.com/meet 都可以設定為 Meet 元件的 URL 項目。不過，只有其中一個 URL 可以 (而且必須) 設定為使用中的 URL。</p>
<p>簡單 URL 項目必須使用 <strong>New-CsSimpleUrlEntry</strong> Cmdlet 建立。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsSimpleUrl** Cmdlet 不接受管線傳送的資料。

## 傳回類型

**New-CsSimpleUrl** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.SimpleUtl.SimpleUrl 物件的新執行個體。

## 請參閱

#### 其他資源

[New-CsSimpleUrlConfiguration](new-cssimpleurlconfiguration.md)  
[New-CsSimpleUrlEntry](new-cssimpleurlentry.md)

