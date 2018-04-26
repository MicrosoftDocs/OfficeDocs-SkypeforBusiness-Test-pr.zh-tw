---
title: New-CsSimpleUrlEntry
TOCTitle: New-CsSimpleUrlEntry
ms:assetid: 3d9dbebf-d23f-40da-9676-19e7906decda
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425902(v=OCS.15)
ms:contentKeyID: 49290676
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsSimpleUrlEntry

 

_**上次修改主題的時間：** 2015-03-09_

建立易記的新 URL 項目，供建立易記 URL 時使用。易記 URL 可方便使用者加入會議，以及方便系統管理員登入 Lync Server 控制台。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsSimpleUrlEntry -Url <String>

## 範例

## 範例 1

範例 1 顯示如何將新的 URL 新增至簡單 URL 的現有集合中。首先，範例中的第一個命令會使用 **New-CsSimpleUrlEntry** Cmdlet，建立指向 https://meet.fabrikam.com 的 URL 項目；此 URL 項目會儲存在名為 $urlEntry 的變數中。

在第二個命令中，**New-CsSimpleUrl** Cmdlet 用於僅在記憶體中建立簡單 URL 的執行個體。在此範例中，URL 元件設為 Meet；網域設為 fabrikam.com；ActiveUrl 設為 https://meet.fabrikam.com；SimpleUrl 屬性設為 $urlEntry，而 $urlEntry 是第一個命令中建立的 URL 項目。

在 URL 建立 (並儲存在物件參考 $simpleUrl 中) 後，範例中的最後一個命令會將新的 URL 新增至 Redmond 網站的易記 URL 集合。這可以透過使用 **Set-CsSimpleUrlConfiguration** Cmdlet、SimpleUrl 參數和參數值 @{Add=$simpleUrl} 完成。此語法會使儲存在物件參考 $simpleUrl 中的 URL 新增至 SimpleUrl 屬性。

    $urlEntry = New-CsSimpleUrlEntry -Url "https://meet.fabrikam.com"
    $simpleUrl = New-CsSimpleUrl -Component "meet" -Domain "fabrikam.com" -SimpleUrlEntry $urlEntry -ActiveUrl "https://meet.fabrikam.com"
    
    Set-CsSimpleUrlConfiguration -Identity "site:Redmond" -SimpleUrl @{Add=$simpleUrl}

## 範例 2

範例 2 會將一對 URL 項目新增至現有簡單 URL 的集合。為達此目的，範例中的第一個命令會使用 **New-CsSimpleUrlEntry** Cmdlet 建立指向 https://meet.fabrikam.com 的 URL 項目，並將其儲存在名為 $urlEntry 的變數中。接著，第二個命令會再建立另一個 URL 項目，將其儲存在名為 $urlEntry2 的變數中並指向 URL https://dialin.fabrikam.com。

建立這兩個 URL 項目後，**New-CsSimpleUrl** Cmdlet 會用於建立兩個僅在記憶體中的簡單 URL 執行個體。在第一個執行個體中，URL 元件設為 Meet；網域設為 fabrikam.com；而 ActiveUrl 設為 https://meet.fabrikam.com。在第二個執行個體中，元件設為 Dialin；網域設為星號 (\*)；而 ActiveURL 屬性設為 https://dialin.fabrikam.com。

建立 URL (並儲存於物件參照 $simpleUrl 和 $simpleUrl2 中) 之後，範例的最後一個命令會將新的 URL 新增至適用於 Redmond 網站的易記 URL 集合中。這可以透過使用 **Set-CsSimpleUrlConfiguration** Cmdlet、SimpleUrl 參數和參數值 @{Add=$simpleUrl, $simpleUrl2} 完成。此語法會導致儲存在物件中的 URL 參照 $simpleUrl，並將 $simpleUrl2 新增至 SimpleUrl 內容。

    $urlEntry = New-CsSimpleUrlEntry -Url "https://meet.fabrikam.com"
    $urlEntry2 = New-CsSimpleUrlEntry -Url "https://dialin.fabrikam.com"
    
    $simpleUrl = New-CsSimpleUrl -Component "meet" -Domain "fabrikam.com" -SimpleUrlEntry $urlEntry -ActiveUrl "https://meet.fabrikam.com"
    $simpleUrl2 = New-CsSimpleUrl -Component "dialin" -Domain "*" -SimpleUrlEntry $urlEntry -ActiveUrl "https://dialin.fabrikam.com"
    
    Set-CsSimpleUrlConfiguration -Identity "site:Redmond" -SimpleUrl @{Add=$simpleUrl, $simpleUrl2}

## 詳細描述

在 Microsoft Office Communications Server 2007 R2 中，會議具有類似下列的 URL：

https://imdf.litwareinc.com/Join?uri=sip%3Akenmyer%40litwareinc.com%3Bgruu%3Bopaque%3Dapp%3Aconf%3Afocus%3Aid%3A125f95a0b0184dcea706f1a0191202a8\&key=EcznhLh5K5t

不過，這種 URl 不是很直覺，不容易傳達給其他人。Lync Server 2010 中採用的易記 URL 提供類似下列的 URL 給使用者，有助於克服這些問題：

https://meet.litwareinc.com/kenmyer/071200

Simple URL 為 Office Communications Server 中使用的 URL 做了明顯改善。但是系統不會自動建立易記 URL；而是您必須自行設定 URL。此外，您還必須執行其他動作，例如建立每個 URL 的網域名稱系統 (DNS) 記錄、設定外部存取的反向 Proxy 規則、將易記 URL 新增至前端伺服器憑證等。

Lync Server 可讓您建立三個不同的易記 URL：

Meet – 用於會議。您的每個 SIP 網域都必須至少有一個 Meet URL。

Admin – 用於將系統管理員指向 Lync Server 控制台。

Dialin – 用於電話撥入式會議網頁。

易記 URL 儲存在易記 URL 組態集合中。當您安裝 Lync Server 後，系統會建立全域集合，您也可以在網站範圍建立自訂集合。這讓您能夠在每個網站使用不同的易記 URL。

若要將實際 URL 新增至簡單 URL 集合，您必須先使用 **New-CsSimpleUrl** Cmdlet 和 **New-CsSimpleUrlEntry** Cmdlet 來建立 URL。**New-CsSimpleUrlEntry** Cmdlet 會建立一個 URL 項目；這不過是可當作簡單 URL (用於會議、管理或電話撥入式會議) 使用的 URL (例如 https://meet.litwareinc.com)。由 **New-CsSimpleUrlEntry** 建立的物件會新增至新簡單 URL 的 SimpleUrlEntry 屬性。您必須使用個別的 Cmdlet 來建立物件，因為 SimpleUrlEntry 屬性可以保留多個 URL。(不過，只有一個這類的 URL 可以被指定為使用中的 URL。使用中的 URL 代表用於會議、管理或電話撥入式會議的實際 URL)。

建立易記 URL 項目後，接下來您可以使用 **New-CsSimpleUrl** Cmdlet 建立僅在記憶體中的易記 URL 執行個體，並將其定義為元件 (易記 URL 的類型)、網域、使用中的 URL，以及所有易記 URL 項目。在您建立代表易記 URL 的物件後，可以將該物件新增至新的或現有的易記 URL 集合。更新易記 URL 後，接著您必須執行 **Enable-CsComputer** Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsSimpleUrlEntry** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsSimpleUrlEntry"}

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
<td><p><em>Url</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要新增至易記 URL 之 SimpleUrlEntry 屬性的 URL。例如：-Url &quot;https://meet.litwareinc.com&quot;。URL 的開頭必須是 &quot;https:&quot;首碼。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

**New-CsSimpleUrlEntry** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.SimpleUtl.SimpleUrlEntry 物件的新執行個體。

## 請參閱

#### 其他資源

[New-CsSimpleUrl](new-cssimpleurl.md)  
[New-CsSimpleUrlConfiguration](new-cssimpleurlconfiguration.md)

