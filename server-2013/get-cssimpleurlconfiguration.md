---
title: Get-CsSimpleUrlConfiguration
TOCTitle: Get-CsSimpleUrlConfiguration
ms:assetid: 59f5528b-d1f4-4da9-9dfe-102c96c6d7c2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398392(v=OCS.15)
ms:contentKeyID: 49291013
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsSimpleUrlConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回設定供組織使用之易記 URL 的資訊。易記 URL 可方便使用者加入會議，以及方便系統管理員登入 Lync Server 控制台。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsSimpleUrlConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsSimpleUrlConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>] [-Tenant <Guid>]

## 範例

## 範例 1

範例 1 會傳回組織目前所使用之所有易記 URL 組態集合的資訊。作法是呼叫不含任何參數的 **Get-CsSimpleUrlConfiguration** Cmdlet。

    Get-CsSimpleUrlConfiguration

## 範例 2

範例 2 會傳回單一易記 URL 組態集合的資訊：Identity 為 site:Redmond 的組態。

    Get-CsSimpleUrlConfiguration -Identity "site:Redmond"

## 範例 3

範例 3 會傳回已指派給網站範圍之所有易記 URL 組態集合的資訊。為達成此目的，會呼叫 **Get-CsSimpleUrlConfiguration** Cmdlet 並搭配 Filter 參數；篩選值 "site:\*" 可將傳回的資料限制在 Identity 開頭為字串值 "site:" 的集合。

    Get-CsSimpleUrlConfiguration -Filter "site:*"

## 範例 4

範例 4 會顯示設定供組織使用之每個易記 URL 的詳細資訊。為了執行此工作，命令會先呼叫 **Get-CsSimpleUrlConfiguration** Cmdlet 傳回一組完整的易記 URL 資訊。然後再將該資料管線傳送到 **Select-Object** Cmdlet，以使用 ExpandProperty 參數「展開」SimpleUrl 屬性的值。展開屬性值會以易讀的格式顯示該屬性中儲存的所有資料。

    Get-CsSimpleUrlConfiguration | Select-Object -ExpandProperty SimpleUrl

## 範例 5

範例 5 所示的命令會傳回組織中目前使用之會議管理的所有易記 URL。為達成此目的，此命令會先呼叫不含任何額外參數的 **Get-CsSimpleUrlConfiguration** Cmdlet，以傳回一組完整的易記 URL 資訊。然後再將該資料管線傳送到 **Select-Object** Cmdlet，以使用 ExpandProperty 參數展開 SimpleUrl 屬性的值。接著將篩選後的集合管線傳送到 **Where-Object** Cmdlet，這會只挑出 Component 屬性等於 "Meet" 的易記 URL。

    Get-CsSimpleUrlConfiguration | Select-Object -ExpandProperty SimpleUrl | Where-Object {$_.Component -eq "Meet"}

## 詳細描述

在 Microsoft Office Communications Server 2007 R2 中，會議具有類似下列的 URL：

https://imdf.litwareinc.com/Join?uri=sip%3Akenmyer%40litwareinc.com%3Bgruu%3Bopaque%3Dapp%3Aconf%3Afocus%3Aid%3A125f95a0b0184dcea706f1a0191202a8\&key=EcznhLh5K5t

不過，這種 URl 不是很直覺，不容易傳達給其他人。Lync Server 2010 中採用的易記 URL 提供類似下列的 URL 給使用者，有助於克服這些問題：

https://meet.litwareinc.com/kenmyer/071200

易記 URL 為 Office Communications Server 中使用的 URL 進行改進。但是系統不會自動建立易記 URL；而是您必須自行設定 URL (您也必須為每個 URL 建立網域名稱系統 (DNS) 記錄；設定外部存取的反向 Proxy 規則；將易記 URL 新增至您的前端伺服器憑證等等)。

Lync Server 可讓您建立三個不同的易記 URL：

Meet – 用於會議。您的每個 SIP 網域都必須至少有一個 Meet URL。

Admin – 用於將系統管理員指向 Lync Server 控制台。

Dialin – 用於電話撥入式會議網頁。

易記 URL 儲存在易記 URL 組態集合中。當您安裝 Lync Server 後，系統會建立全域集合，您也可以在網站範圍建立自訂集合。這讓您能夠在每個網站使用不同的易記 URL。

**Get-CsSimpleUrlConfiguration** Cmdlet 可讓您擷取組織目前所使用之所有易記 URL 組態集合的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsSimpleUrlConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsSimpleUrlConfiguration"}

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
<td><p>可讓您使用萬用字元指定要傳回的易記 URL 集合。例如，下列語法會傳回已在網站範圍設定的所有易記 URL 集合：-Filter &quot;site:*&quot;。</p>
<p>請注意，您不能在同一個命令中同時使用 Filter 和 Identity 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要傳回之易記 URL 集合的唯一識別碼。若要傳回全域集合，請使用下列語法：-Identity global。若要傳回網站範圍的集合，請使用類似下列的語法：-Identity &quot;site:Redmond&quot;。請注意，如有指定 Identity，即無法使用萬用字元。如果要使用萬用字元，請改用 Filter 參數。</p>
<p>呼叫不含任何參數的 <strong>Get-CsSimpleUrlConfiguration</strong> Cmdlet，會傳回設定供組織使用的所有易記 URL。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取 Simple URL 組態資料，而非從中央管理存放區本身擷取。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要擷取其易記 URL 組態設定之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行此命令來傳回每位租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

**Get-CsSimpleUrlConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.SimpleUrl.SimpleUrlConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsSimpleUrlConfiguration](new-cssimpleurlconfiguration.md)  
[Remove-CsSimpleUrlConfiguration](remove-cssimpleurlconfiguration.md)  
[Set-CsSimpleUrlConfiguration](set-cssimpleurlconfiguration.md)

