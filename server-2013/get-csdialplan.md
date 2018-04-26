---
title: Get-CsDialPlan
TOCTitle: Get-CsDialPlan
ms:assetid: f77df510-ea43-4352-84c1-13f69eda252e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413043(v=OCS.15)
ms:contentKeyID: 49292847
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsDialPlan

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織所使用之撥號對應表的資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsDialPlan [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsDialPlan [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 會傳回設定來供組織使用的所有撥號對應表集合，方法是呼叫 **Get-CsDialPlan** Cmdlet 且不指定任何其他參數。

    Get-CsDialPlan

## 範例 2

範例 2 會使用 Identity 參數，將擷取的資料限制為擁有 Identity 為 RedmondDialPlan 之個別使用者撥號對應表的撥號對應表。由於識別身分必須是唯一的，所以此命令只會傳回指定的撥號對應表。

    Get-CsDialPlan -Identity RedmondDialPlan

## 範例 3

範例 3 與範例 2 相同，唯一不同是不會擷取個別使用者撥號對應表，而會擷取指派給網站的撥號對應表。作法是指定 site: 值加上要擷取之網站的名稱 (在此範例中為 Redmond)。

    Get-CsDialPlan -Identity site:Redmond

## 範例 4

本例使用 Filter 參數來傳回已在個別使用者範圍上設定之所有撥號對應表的集合 (設定於個別使用者 (或標籤) 範圍上的設定，可直接指派給使用者和群組)。萬用字元字串 tag:\* 會指示 Cmdlet 只傳回其識別身分開頭為字串值 tag: 的撥號對應表，這會將撥號對應表識別為個別使用者撥號對應表。

    Get-CsDialPlan -Filter tag:*

## 範例 5

本範例會顯示已設定為供組織使用之撥號對應表所使用的正規化規則。由於 NormalizationRules 屬性會包含物件的陣列，所以螢幕上通常不會顯示一組完整的正規化規則。為了看到所有這類規則，此範例命令會先使用 **Get-CsDialPlan** Cmdlet 來擷取所有撥號對應表的集合。然後將該集合傳送到 **Select-Object** Cmdlet；接著，使用 **Select-Object** Cmdlet 的 ExpandProperty 參數來「展開」在 NormalizationRules 屬性中找到的值。展開值只是表示所有正規化規則都會單獨列於螢幕上，如果當初呼叫 **Get-CsVoiceNormalizationRule** Cmdlet，使用者會看到相同的輸出結果。

    Get-CsDialPlan | Select-Object -ExpandProperty NormalizationRules

## 範例 6

在範例 6 中，**Get-CsDialPlan** Cmdlet 和 **Where-Object** Cmdlet 可用來擷取描述中包含 Redmond 這個字的所有撥號對應表集合。為達成此目的，命令會先使用 **Get-CsDialPlan** Cmdlet 擷取所有撥號對應表。然後再將該集合管線傳送至 **Where-Object** Cmdlet 套用篩選器，以將傳回的資料限制在 Description 包含 Redmond 一字的設定檔。

    Get-CsDialPlan | Where-Object {$_.Description -match "Redmond"}

## 詳細描述

此 Cmdlet 會傳回組織中一或多個撥號對應表 (又稱為位置設定檔) 的資訊。撥號對應表可提供 Enterprise Voice 使用者撥打電話所需的資訊。會議服務員應用程式 也會在執行電話撥入式會議時使用撥號對應表。撥號對應表可指定所要套用的正規化規則，以及撥打外線時是否需要先撥首碼。

附註：您可以使用 **Get-CsDialPlan** Cmdlet 來擷取有關撥號對應表之正規化規則的特定資訊，但如果這是您唯一需要的撥號對應表資訊，也可以使用 **Get-CsVoiceNormalizationRule** Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsDialPlan** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsDialPlan"}

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
<td><p>執行萬用字元搜尋，它允許您將結果縮減為只有 Identity 符合指定萬用字元字串的撥號對應表。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>指定範圍的唯一識別碼，以及針對個別使用者範圍指定名稱，以識別您要擷取的撥號對應表。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區 的本機複本擷取撥號對應表資訊，而非從 中央管理存放區 本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

此 Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.LocationProfile 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsDialPlan](new-csdialplan.md)  
[Remove-CsDialPlan](remove-csdialplan.md)  
[Set-CsDialPlan](set-csdialplan.md)  
[Grant-CsDialPlan](grant-csdialplan.md)  
[Test-CsDialPlan](test-csdialplan.md)  
[Get-CsVoiceNormalizationRule](get-csvoicenormalizationrule.md)

