---
title: New-CsSimpleUrlConfiguration
TOCTitle: New-CsSimpleUrlConfiguration
ms:assetid: 3140f15a-e448-42fe-b494-bf9caba32b35
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425813(v=OCS.15)
ms:contentKeyID: 49290504
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsSimpleUrlConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

建立易記之新 URL 組態集合。易記 URL 可以方便使用者加入會議，以及方便系統管理員登入 Lync Server 控制台。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsSimpleUrlConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-SimpleUrl <PSListModifier>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會為 Redmond 網站建立新的簡易 URL 集合。由於此命令不提供 Identity 以外的參數，因此新的集合中不會包含任何的簡易 URL。如果 Redmond 網站已主控簡易 URL 集合，則此命令會失敗。

    New-CsSimpleUrlConfiguration -Identity "site:Redmond"

## 範例 2

範例 2 顯示如何建立包含兩個簡單 URL (一個供會議管理使用，另一個供電話撥入式會議使用) 的新簡單 URL 集合。為達此目的，範例中的第一個命令會使用 **New-CsSimpleUrlEntry** Cmdlet 建立一個指向 https://dialin.litwareinc.com 的 URL 項目；此 URL 項目會儲存在名為 $urlEntry 的變數中。然後，第二個命令會建立另一個 URL 項目，指向 https://meet.fabrikam.com。

接下來，此命令使用 **New-CsSimpleUrl** Cmdlet 來建立只存在於記憶體中的簡易 URL 執行個體。在此範例中，URL 元件已設為 dialin、網域已設為星號 (\*)、ActiveUrl 已設為 https://dialin.fabrikam.com，而 SimpleUrl 內容則設為 $urlEntry ($urlEntry 變數代表在第一個命令中建立的 URL 項目)。此範例接著使用相似的命令來建立 meet.fabrikam.com 的簡易 URL。

在建立 URL (並儲存到物件參考 $simpleUrl 和 simpleUrl2 中) 後，範例中的最後一個命令會為 Redmond 網站建立新的簡易 URL 集合，並將兩個只存在於記憶體中的 URL 新增至該集合。新的 URL 可藉由使用 **New-CsSimpleUrlConfiguration** Cmdlet、SimpleUrl 參數及 @{Add=$simpleUrl, $simpleUrl2} 參數值新增至集合。該語法會使系統將儲存在 $simpleUrl 和 $simpleUrl2 等物件參考中的 URL 新增至 SimpleUrl 內容。

    $urlEntry = New-CsSimpleUrlEntry -Url "https://dialin.fabrikam.com"
    $simpleUrl = New-CsSimpleUrl -Component "dialin" -Domain "*" -SimpleUrlEntry $urlEntry -ActiveUrl "https://dialin.fabrikam.com"
    
    $urlEntry2 = New-CsSimpleUrlEntry -Url "https://meet.fabrikam.com"
    $simpleUrl2 = New-CsSimpleUrl -Component "meet" -Domain "fabrikam.com" -SimpleUrlEntry $urlEntry2 
    
    New-CsSimpleUrlConfiguration -Identity "site:Redmond" -SimpleUrl @{Add=$simpleUrl,$simpleUrl2}

## 詳細描述

在 Microsoft Office Communications Server 2007 R2 中，會議具有類似下列的 URL：

https://imdf.litwareinc.com/Join?uri=sip%3Akenmyer%40litwareinc.com%3Bgruu%3Bopaque%3Dapp%3Aconf%3Afocus%3Aid%3A125f95a0b0184dcea706f1a0191202a8\&key=EcznhLh5K5t

不過，這種 URl 不是很直覺，不容易傳達給其他人。Lync Server 2010 中採用的簡易 URL 提供類似下列的 URL 給使用者，有助於克服這些問題：

https://meet.litwareinc.com/kenmyer/071200

Simple URL 為 Office Communications Server 中使用的 URL 進行改進。但是系統不會自動建立簡易 URL；而是您必須自行設定 URL。此外，您還必須執行其他動作，例如建立每個 URL 的網域名稱系統 (DNS) 記錄、設定外部存取的反向 Proxy 規則、將簡易 URL 新增至前端伺服器憑證等。

Lync Server 可讓您建立三個不同的簡易 URL：

Meet – 用於會議。您的每個 SIP 網域必須至少有一個 Meet URL。

Admin – 用於將系統管理員指向 Lync Server 控制台。

Dialin – 用於電話撥入式會議網頁。

簡易 URL 儲存在簡易 URL 組態集合中。當您安裝 Lync Server 後，系統會建立全域集合，您也可以在網站範圍建立自訂集合。這讓您能夠在每個網站使用不同的簡易 URL。

簡單 URL 組態集合是使用 **New-CsSimpleUrlConfiguration** Cmdlet 建立的，您之後可以使用其他的 Cmdlet (例如 **New-CsSimpleUrl** Cmdlet 和 **Set-CsSimpleUrlConfiguration** Cmdlet) 將簡單 URL 填入到這些集合中。更新簡單 URL 後，接著您必須執行 **Enable-CsComputer** Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsSimpleUrlConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsSimpleUrlConfiguration"}

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
<td><p>新簡易 URL 組態集合的唯一識別碼。因為新的集合只會在網站範圍建立，所以 Identity 的首碼必須是 &quot;site:&quot;後面再加上網站的名稱。例如，這個語法會為 Redmond 網站建立新的集合：-Identity &quot;site:Redmond&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
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
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="odd">
<td><p><em>SimpleUrl</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>已為此集合設定的簡單 URL。必須使用 <strong>New-SimpleUrl</strong> Cmdlet 和 <strong>New-SimpleUrlEntry</strong> Cmdlet 建立這些 URL。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要建立新簡單 URL 組態設定之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行此命令，為每個租用戶傳回租用戶識別碼：</p>
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

無。

## 傳回類型

**New-CsSimpleUrlConfiguration** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.SimpleUrl.SimpleUrlConfiguration 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsSimpleUrlConfiguration](get-cssimpleurlconfiguration.md)  
[New-CsSimpleUrl](new-cssimpleurl.md)  
[New-CsSimpleUrlEntry](new-cssimpleurlentry.md)  
[Remove-CsSimpleUrlConfiguration](remove-cssimpleurlconfiguration.md)  
[Set-CsSimpleUrlConfiguration](set-cssimpleurlconfiguration.md)

