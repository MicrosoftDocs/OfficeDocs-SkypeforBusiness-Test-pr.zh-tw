---
title: Set-CsSimpleUrlConfiguration
TOCTitle: Set-CsSimpleUrlConfiguration
ms:assetid: f0334ae9-e6c1-4134-8749-af202169bb2a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412991(v=OCS.15)
ms:contentKeyID: 49292747
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsSimpleUrlConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的易記 URL 組態集合。易記 URL 可以方便使用者加入會議，以及方便系統管理員登入 Lync Server 控制台。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsSimpleUrlConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsSimpleUrlConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-SimpleUrl <PSListModifier>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會從 Redmond 網站移除所有的簡易 URL，但不會移除簡易 URL 的實際集合 (此集合仍會存在，但不再包含任何 URL)。為達此目的，命令會使用 SimpleUrl 參數搭配參數值 Null ($Null)，以從集合中移除所有的簡易 URL。

    Set-CsSimpleUrlConfiguration -Identity "site:Redmond" -SimpleUrl $Null

## 範例 2

範例 2 顯示如何將新的 URL 新增至簡單 URL 的現有集合中。首先，範例中的第一個命令會使用 **New-CsSimpleUrlEntry** Cmdlet，建立指向 https://meet.fabrikam.com 的 URL 項目；此 URL 項目會儲存在名為 $urlEntry 的變數中。

在第二個命令中，**New-CsSimpleUrl** Cmdlet 用於僅在記憶體中建立簡單 URL 的執行個體。在此範例中，URL 元件設為 Meet；網域設為 fabrikam.com；ActiveUrl 設為 https://meet.fabrikam.com；SimpleUrl 屬性設為 $urlEntry，而 $urlEntry 是第一個命令中建立的 URL 項目。

在 URL 建立 (並儲存在物件參考 $simpleUrl 中) 後，範例中的最後一個命令會將新的 URL 新增至 Redmond 網站的簡易 URL 集合。這可以透過使用 **Set-CsSimpleUrlConfiguration** Cmdlet、SimpleUrl 參數和參數值 @{Add=$simpleUrl} 完成。此語法會使儲存在物件參考 $simpleUrl 中的 URL 新增至 SimpleUrl 屬性。

    $urlEntry = New-CsSimpleUrlEntry -Url "https://meet.fabrikam.com"
    $simpleUrl = New-CsSimpleUrl -Component "meet" -Domain "fabrikam.com" -SimpleUrlEntry $urlEntry -ActiveUrl "https://meet.fabrikam.com"
    
    Set-CsSimpleUrlConfiguration -Identity "site:Redmond" -SimpleUrl @{Add=$simpleUrl}

## 範例 3

範例 3 所示的命令示範您如何從簡易 URL 集合中刪除單一 URL。由於 **Set-CsSimpleUrlConfiguration** Cmdlet 需要與 URL 物件一起運作，因此範例一開始便會建立包含與要刪除 URL 完全相同之屬性值的新物件。作法上第一個命令會使用 **New-CsSimpleUrlEntry** Cmdlet，來建立指向 https://meet.fabrikam.com 的 URL 項目；此 URL 項目儲存於名為 $urlEntry 的變數中。

建立 URL 項目之後，第二個命令會使用 **New-CsSimpleUrl** Cmdlet，建立只存在記憶體內的簡易 URL 執行個體。在此範例中，將 URL Component 設定為 Meet；將網域設定為 fabrikam.com；將 ActiveUrl 設定為 https://meet.fabrikam.com；以及將 SimpleUrl 屬性設定為 $urlEntry，$urlEntry 是第一個命令中建立的 URL 項目。這會建立記憶體內的 URL ($simpleUrl)，該 URL 具備與要刪除之 URL 相同的屬性值。

然後範例中的最後一個命令會從適用於 Redmond 網站的簡易 URL 集合中刪除該 URL。作法是使用 **Set-CsSimpleUrlConfiguration** Cmdlet、SimpleUrl 參數與參數值 @{Remove=$simpleUrl}。此語法只是使儲存於物件參照 $simpleUrl 中的 URL 從 SimpleUrl 屬性中移除。

    $urlEntry = New-CsSimpleUrlEntry -Url "https://fabrikam.vdomain.com"
    $simpleUrl = New-CsSimpleUrl -Component "meet" -Domain "fabrikam.com" -SimpleUrlEntry $urlEntry -ActiveUrl "https://meet.fabrikam.com"
    
    Set-CsSimpleUrlConfiguration -Identity "site:Redmond" -SimpleUrl @{Remove=$simpleUrl}

## 詳細描述

在 Microsoft Office Communications Server 2007 R2 中，會議具有類似下列的 URL：

https://imdf.litwareinc.com/Join?uri=sip%3Akenmyer%40litwareinc.com%3Bgruu%3Bopaque%3Dapp%3Aconf%3Afocus%3Aid%3A125f95a0b0184dcea706f1a0191202a8\&key=EcznhLh5K5t

不過，這種 URl 不是很直覺，不容易傳達給其他人。Lync Server 中採用的簡易 URL 提供類似下列的 URL 給使用者，有助於克服這些問題：

https://meet.litwareinc.com/kenmyer/071200

Simple URL 大幅改善了舊版 Office Communications Server 中使用的 URL。但是系統不會自動建立簡易 URL；而是您必須自行設定 URL。此外，您還必須執行其他動作，例如建立每個 URL 的網域名稱系統 (DNS) 記錄、設定外部存取的反向 Proxy 規則、將簡易 URL 新增至前端伺服器憑證等。

Lync Server 可讓您建立三個不同的簡易 URL：

Meet – 用於會議。您的每個 SIP 網域必須至少有一個 Meet URL。

Admin – 用於將系統管理員指向 Lync Server。

Dialin – 用於電話撥入式會議網頁。

簡易 URL 儲存在簡易 URL 組態集合中。當您安裝 Lync Server 後，系統會建立全域集合，您也可以在網站範圍建立自訂集合。這讓您能夠在每個網站使用不同的簡易 URL。

簡易 URL 組態集合是使用 **New-CsSimpleUrlConfiguration** Cmdlet 建立的，您之後可以使用其他的 Cmdlet (例如 **New-CsSimpleUrl** Cmdlet 和 **Set-CsSimpleUrlConfiguration** Cmdlet) 將簡易 URL 填入到這些集合中。建立集合之後，**Set-CsSimpleUrlConfiguration** Cmdlet 也會為您提供修改這些集合中所儲存之 URL 的能力。

將簡易 URL 新增至集合相當簡單。一開始，您使用 **New-CsSimpleUrl** Cmdlet 和 **New-CsSimpleUrlEntry** Cmdlet 來建立只存在記憶體內的 URL。然後使用 Add 命令，將新的 URL 新增至現有的集合。或者，可以使用 Replace 方法，利用新的 URL 來取代所有現有的 URL。

從集合中移除 URL 就有點困難；這是因為您必須先建立該 URL (模擬現有 URL 的那一個) 的新物件參照，然後使用該物件參照和 Remove 方法來刪除 URL。

更新簡易 URL 後，接著您必須執行 **Enable-CsComputer** Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsSimpleUrlConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsSimpleUrlConfiguration"}

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
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要修改之簡易 URL 集合的唯一識別碼。若要修改全域集合，請使用下列語法：-Identity global。若要從網站範圍修改集合，請使用類似下列的語法：-Identity &quot;site:Redmond.&quot;</p>
<p>若未指定此參數，將會修改全域集合。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>SimpleUrlConfiguration 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>SimpleUrl</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>針對此集合設定的簡易 URL。必須使用 <strong>New-SimpleUrl</strong> Cmdlet 和 <strong>New-SimpleUrlEntry</strong> Cmdlet 建立這些 URL。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要修改簡易 URL 組態設定之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行下列命令傳回每個租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.SimpleUrl.SimpleUrlConfiguration 物件。**Set-CsSimpleUrlConfiguration** Cmdlet 會接受簡單 URL 組態物件的管線傳送執行個體。

## 傳回類型

無。

## 請參閱

#### 其他資源

[Get-CsSimpleUrlConfiguration](get-cssimpleurlconfiguration.md)  
[New-CsSimpleUrl](new-cssimpleurl.md)  
[New-CsSimpleUrlConfiguration](new-cssimpleurlconfiguration.md)  
[New-CsSimpleUrlEntry](new-cssimpleurlentry.md)  
[Remove-CsSimpleUrlConfiguration](remove-cssimpleurlconfiguration.md)

