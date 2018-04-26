---
title: Get-CsLocationPolicy
TOCTitle: Get-CsLocationPolicy
ms:assetid: d338af1b-3865-4010-a7fc-d5841c515ae6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398911(v=OCS.15)
ms:contentKeyID: 49292428
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsLocationPolicy

 

_**上次修改主題的時間：** 2015-03-09_

傳回 位置資訊服務如何 (有無) 設定增強型 9-1-1 (E9-1-1) 的資訊。E9-1-1 服務可協助接聽緊急電話的人員判別來電者的地理位置。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsLocationPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsLocationPolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 會傳回組織目前使用的所有位置原則集合。作法是只需呼叫不含任何參數的 **Get-CsLocationPolicy** Cmdlet 即可。

    Get-CsLocationPolicy

## 範例 2

範例 2 所示的命令只會傳回 Identity 等於 Reno 的位置原則。由於 Identity 必須是唯一的，因此這個命令最多只會傳回一個位置原則。

    Get-CsLocationPolicy -Identity Reno

## 範例 3

範例 3 會使用 Filter 參數來傳回已在個別使用者範圍設定的所有位置原則 (在個別使用者範圍設定的原則可直接指派給使用者和網站)。萬用字元 tag:\* 會指示 **Get-CsLocationPolicy** Cmdlet，將傳回的資料限制在 Identity 開頭為字串值 tag: 的位置原則。即便在擷取個別原則時不需指定 tag: 前置詞，您還是可以使用這個前置詞來篩選所有個別使用者原則。

    Get-CsLocationPolicy -Filter tag:*

## 範例 4

範例 4 會傳回已停用增強型緊急服務的所有位置原則集合。為達成此目的，命令會先使用 **Get-CsLocationPolicy** Cmdlet，以傳回組織目前使用之所有位置原則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet。接著 **Where-Object** Cmdlet 會套用篩選，將傳回的資料限制在 EnhancedEmergencyServicesEnabled 屬性等於 (-eq) False ($False) 的原則。

    Get-CsLocationPolicy | Where-Object {$_.EnhancedEmergencyServicesEnabled -eq $False}

## 詳細描述

位置原則可用來套用和 E9-1-1 功能相關的設定。位置原則會判斷使用者是否已啟用 E9-1-1，如果是，則會決定緊急電話的行為。例如，您可以使用位置原則來定義組成緊急電話的數字 (在美國為 911)、是否應自動告知公司的安全部門，以及應如何路由傳送來電等等。此 Cmdlet 會擷取一或多個位置原則。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsLocationPolicy** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsLocationPolicy"}

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
<td><p>System.Strkng</p></td>
<td><p>含有萬用字元的字串，這個字串可藉由比對原則的 Identity 值和萬用字元字串來擷取位置原則。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要擷取之位置原則的唯一識別碼。若要擷取全域位置原則，請使用 Global 值。對於在網站範圍內建立的原則，這個值的格式將為 site:&lt;網站名稱&gt;。其中「網站名稱」是指在 Lync Server 部署中定義之網站的名稱 (例如 site:Redmond)。對於已在個別使用者範圍內建立的原則，此值將只是原則的名稱，例如 Reno。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區本機複本擷取位置原則資訊，而不從 中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

**Get-CsLocationPolicy** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Policy.Location.LocationPolicy 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsLocationPolicy](new-cslocationpolicy.md)  
[Remove-CsLocationPolicy](remove-cslocationpolicy.md)  
[Set-CsLocationPolicy](set-cslocationpolicy.md)  
[Grant-CsLocationPolicy](grant-cslocationpolicy.md)  
[Test-CsLocationPolicy](test-cslocationpolicy.md)

