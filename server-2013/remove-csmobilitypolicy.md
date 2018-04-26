---
title: Remove-CsMobilityPolicy
TOCTitle: Remove-CsMobilityPolicy
ms:assetid: d3dc4653-25ab-45ef-b325-fba01e45acca
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690048(v=OCS.15)
ms:contentKeyID: 49292413
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsMobilityPolicy

 

_**上次修改主題的時間：** 2015-03-09_

移除現有的行動原則。行動原則會判斷使用者是否可以使用 \[從公司撥號\]，在其行動電話上使用公司電話號碼，而不使用自己的行動電話號碼收發電話。在撥打或接聽來電時，行動原則也可以用來要求 Wi-Fi 連線。 Lync Server 2010：2011 年 11 月的累計更新中已導入此 Cmdlet。

## 語法

    Remove-CsMobilityPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會移除為 Redmond 網站設定的行動原則。移除原則之後，先前受到 Redmond 網站原則管理的使用者，現在將變成由全域原則管理。

    Remove-CsMobilityPolicy -Identity "site:Redmond"

## 範例 2

範例 2 會移除在個別使用者範圍設定的所有行動原則。為達此目的，命令會先使用 **Get-CsMobilityPolicy** Cmdlet 搭配 Filter 參數，以擷取所有 Identity 開頭為字串值 "Tag:" 的原則 (根據定義，所有符合該準則的原則都是個別使用者原則)。然後再將將個別使用者原則集合管線傳送到 **Remove-CsMobilityPolicy** Cmdlet，以刪除集合中的每個原則。

    Get-CsMobilityPolicy -Filter "tag:*" | Remove-CsMobilityPolicy

## 範例 3

範例 3 示範如何刪除所有已啟用 \[從公司撥號\] 的行動原則。為達成此目的，命令會先使用 **Get-CsMobilityPolicy** Cmdlet，以擷取組織目前使用之所有行動原則的集合。然後，此集合會管線傳送到 where-Object Cmdlet，這會只挑出 EnableOutsideVoice 屬性設為 False 的原則。接著將所有 EnableOutsideVoice 為 False 的原則管線傳送到 **Remove-CsMobilityPolicy** Cmdlet 加以移除。

    Get-CsMobilityPolicy | Where-Object {$_.EnableOutsideVoice -eq $False} | Remove-CsMobilityPolicy

## 詳細描述

Lync Mobile 是可讓使用者在行動電話上執行 Lync 的用戶端應用程式。\[從公司撥號\] 可讓使用者在行動電話上撥打電話，但是將此通話顯示為從公司電話號碼 (而不是行動電話號碼) 撥出的通話。啟用 \[從公司撥號\] 的使用者可以直接從其行動電話撥號，或透過 \[電話撥出式會議\] 選項來達成此目的。透過電話撥出式會議，使用者實際上是要求 Mobility Service 伺服器代為撥打電話。伺服器會建立通話，然後回撥給使用者的行動電話。在使用者接聽之後，伺服器會接著撥打給受話方。您可以使用行動原則來管理這兩個功能。

透過 Lync Server 2013，行動裝置可以使用標準行動電話網路或 Wi-Fi 連線來撥打或接聽電話。行動原則可以用來要求 Wi-Fi 連線並防止透過行動網路的來電。

當您安裝 Lync Server 時，即會有套用到所有使用者的單一全域行動性原則。但是，系統管理員可以使用 **New-CsMobilityPolicy** Cmdlet，在網站範圍或個別使用者範圍建立自訂原則。

如果您在網站範圍或個別使用者範圍建立自訂原則，稍後可以使用 **Remove-CsMobilityPolicy** Cmdlet 刪除這些原則。如果您刪除個別使用者原則，則指派該原則的任何使用者將變成由適當的網站原則 (如其存在) 或全域原則管理。如果您移除網站原則，則受到該原則管理的使用者將變成由全域原則管理。

請注意，您也可以對全域原則執行 **Remove-CsMobilityPolicy** Cmdlet。不過，這樣做實際上不會刪除全域原則，而是將該原則中的屬性重設為其預設值。在此情況下，也就是啟用 \[從公司撥號\]。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsMobilityPolicy** Cmdlet：RTCUniversalServerAdmins。

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
<td><p>要移除之用戶端原則的唯一識別碼。若要移除全域原則，請使用下列語法：</p>
<p>-Identity global</p>
<p>不過請注意，這樣做實際上不會移除全域原則，而是將該原則中的所有屬性重設為其預設值。</p>
<p>若要移除網站原則，請使用類似下列的語法：</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>若要移除個別使用者原則，請使用類似下列的語法：</p>
<p>-Identity &quot;SalesDepartmentPolicy&quot;</p>
<p>在指定原則 Identity 時不能使用萬用字元。</p></td>
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
<td><p>如果使用此參數，即使原則目前已指派給至少一位使用者，也會遭到移除。若未使用此參數，則 <strong>Remove-CsMobilityPolicy</strong> Cmdlet 就不會自動移除已指派給至少一位使用者的個別使用者原則。但是會顯示確認提示，詢問您是否確定要移除該原則。您必須回答是 (按下 Y 鍵)，命令才會繼續並移除該原則。</p>
<p>此參數僅適用於個別使用者原則。</p></td>
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

Microsoft.Rtc.Management.WriteableConfig.Policy.Mobility.Mobility。 **Remove-CsMobilityPolicy** Cmdlet 接受管線傳送的 Mobility 物件執行個體。

## 傳回類型

無。反之， **Remove-CsMobilityPolicy** Cmdlet 會刪除 Microsoft.Rtc.Management.WriteableConfig.Policy.Mobility.Mobility 物件的執行個體。

