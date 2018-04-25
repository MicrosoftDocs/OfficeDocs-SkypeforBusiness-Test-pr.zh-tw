---
title: Get-CsMobilityPolicy
TOCTitle: Get-CsMobilityPolicy
ms:assetid: 51ef83de-9cc2-4df8-b4f1-8d816b8de431
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690017(v=OCS.15)
ms:contentKeyID: 49290914
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsMobilityPolicy

 

_**上次修改主題的時間：** 2015-03-09_

擷取組織目前所使用之行動原則的資訊。行動原則決定使用者是否可以使用 Lync Mobile。這些原則也可以管理使用者是否能使用「從公司撥號」功能，以在其行動電話上使用公司電話號碼撥接電話，而不是自己的行動電話號碼。行動原則也可以在撥號或接聽來電時用來要求 Wi-Fi 連線。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsMobilityPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsMobilityPolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回設定供組織使用之所有行動原則的資訊。

    Get-CsMobilityPolicy

## 範例 2

範例 2 會傳回單一行動原則資訊：Identity 為 site:Redmond 的原則。

    Get-CsMobilityPolicy -Identity "site:Redmond"

## 範例 3

範例 3 會傳回所有個別使用者行動原則的資訊。若要執行此作業，必須加入 Filter 參數搭配篩選值 "tag:\*"，以將傳回的資料限制在 Identity 開頭為字串值 "tag:" 的原則。根據定義，所有 Identity 開頭為 "tag:" 的原則都是個別使用者原則。

    Get-CsMobilityPolicy -Filter "tag:*"

## 範例 4

範例 4 所示的命令會將傳回的資料限制為已停用「從公司撥號」的行動原則。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsMobilityPolicy** Cmdlet，以傳回設定供組織使用之所有行動原則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 EnableOutsideVoice 屬性等於 (-eq) False 的原則。

    Get-CsMobilityPolicy | Where-Object {$_.EnableOutsideVoice -eq $False}

## 詳細描述

Lync Mobile 是可讓使用者在行動電話上執行 Lync 的用戶端應用程式。\[從公司撥號\] 可讓使用者在行動電話上撥打電話，但是將此通話顯示為從公司電話號碼 (而不是行動電話號碼) 撥出的通話。啟用 \[從公司撥號\] 的使用者可以直接從其行動電話撥號，或透過 \[電話撥出式會議\] 選項來達成此目的。透過電話撥出式會議，使用者實際上是要求 Lync Server Mobility Service 伺服器代為撥打電話。伺服器會建立通話，然後回撥給使用者的行動電話。在使用者接聽之後，伺服器會接著撥打給受話方。您可以使用行動原則來管理這兩個功能。

透過 Lync Server 2013，行動裝置可以使用標準行動電話網路或 Wi-Fi 連線來撥打或接聽電話。行動原則可用於要求 Wi-Fi 連線，以避免透過行動電話網路進行通話。

行動原則可以在全域範圍、網站範圍或個別使用者範圍設定，且可使用 **Get-CsMobilityPolicy** Cmdlet 來擷取這些原則的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsMobilityPolicy** Cmdlet：RTCUniversalServerAdmins。

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
<td><p>可讓您在指示要傳回的原則 (或多個原則) 時使用萬用字元。例如，若要傳回在網站範圍設定的所有原則，請使用下列語法：</p>
<p>-Filter &quot;site:*&quot;</p>
<p>若要傳回所有個別使用者原則的集合，請使用下列語法：</p>
<p>-Filter &quot;tag:*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要傳回之行動原則的唯一識別碼。若要參考全域原則，請使用下列語法：</p>
<p>-Identity global</p>
<p>若要參考網站原則，請使用類似下列的語法：</p>
<p>-Identity site:Redmond</p>
<p>若要參考個別使用者原則，請使用類似下列的語法：</p>
<p>-Identity SalesDepartmentPolicy</p>
<p>若未指定此參數，則 <strong>Get-CsMobilityPolicy</strong> Cmdlet 會傳回在組織中使用的所有行動原則集合。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區的本機複本擷取行動原則資料，而非從 中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

**Get-CsMobilityPolicy** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsMobilityPolicy** Cmdlet 會傳回 Microsoft.Rtc.Management.WriteableConfig.Policy.Mobility.Mobility 物件的執行個體。

