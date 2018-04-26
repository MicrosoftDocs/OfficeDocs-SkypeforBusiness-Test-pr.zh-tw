---
title: Get-CsRgsHoursOfBusiness
TOCTitle: Get-CsRgsHoursOfBusiness
ms:assetid: 2008d55c-fd53-4004-b6e6-08cdf0175af8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398284(v=OCS.15)
ms:contentKeyID: 49290303
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsRgsHoursOfBusiness

 

_**上次修改主題的時間：** 2015-03-09_

擷取設定供組織使用之回應群組營業時間集合的資訊。營業時間集合可用以指定回應群組代理一週中可以正常接聽來電的日子與時段。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsRgsHoursOfBusiness [-Identity <RgsIdentity>] [-Name <String>] [-Owner <RgsIdentity>] [-ShowAll <SwitchParameter>]

## 範例

## 範例 1

範例 1 傳回設定供組織使用之所有營業時間集合的資訊。作法是不使用任何參數而直接呼叫 **Get-CsRgsHoursOfBusiness**。

    Get-CsRgsHoursOfBusiness

## 範例 2

範例 2 所示的命令傳回已設定用於 atl-cs-001.litwareinc.com 的所有營業時間集合。

    Get-CsRgsHoursOfBusiness -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com"

## 範例 3

範例 3 會從 atl-cs-001.litwareinc.com 傳回一組名稱為 "Help Desk Business Hours" 的營業時間集合。

    Get-CsRgsHoursOfBusiness -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" -Name "Help Desk Business Hours"

## 範例 4

範例 4 所示的命令會傳回所有營業時間設定為星期日的營業時間集合。為達此目的，命令會先呼叫 **Get-CsRgsHoursOfBusiness** 傳回在 atl-cs-001.litwareinc.com 上找到的所有營業時間集合。此資料會接著傳送到 **Where-Object** Cmdlet，以選取符合下列兩項準則之一的項目：SundayTimeRange1 屬性不等於 Null 值和/或 SundayTimeRange2 屬性不等於 Null 值。如果時間範圍屬性不是 Null，即表示已為該時段設定營業時間。

    Get-CsRgsHoursOfBusiness -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" | Where-Object {$_.SundayTimeRange1 -ne $Null -or $_.SundayTimeRange2 -ne $Null}

## 範例 5

範例 5 所示的命令會從 atl-cs-001.litwareinc.com 傳回所有營業時間集合，其中 MondayTimeRange1 內容的開啟時間等於 (或早於) 8:00 A.M。為此，命令先使用 **Get-CsRgsHoursOfBusiness**，從 atl-cs-001.litwareinc.com 傳回所有營業時間集合。接著，此資料傳送到 **Where-Object** Cmdlet，此 Cmdlet 只選取 MondayTimeRange1.OpenTime 內容的值小於或等於 8:00 A.M. (08:00:00) 的集合。

    Get-CsRgsHoursOfBusiness -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" | Where-Object {$_.MondayTimeRange1.OpenTime -le "08:00:00"}

## 範例 6

範例 6 所示的命令會傳回所有公用的營業時間集合，亦即可以在工作流程之間共用的集合。為達此目的，命令先使用 **Get-CsRgsHoursOfBusiness** 傳回 atl-cs-001.litwareinc.com 上找到的所有營業時間集合。然後，此資料便會傳送到 **Where-Object** Cmdlet，此 Cmdlet 只挑選出 Custom 內容等於 False 的集合。

    Get-CsRgsHoursOfBusiness -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" | Where-Object {$_.Custom -eq $False}

## 詳細描述

為了提供給來電者最佳的服務經驗，回應群組應用程式 讓您可以清楚定義回應群組代理何時可接聽電話，何時無法接聽電話。透過回應群組應用程式，您可以定義營業時間，指出代理在一星期中有哪幾天和哪些時段可接聽來電。例如，如果您組織的營業時間是星期一到星期五的 9:00 A.M. 到 5:00 P.M.，那麼您可以設定營業時間中顯示代理會在星期一到星期五的 9:00 A.M. 到 5:00 P.M. 接聽來電 (以及該分機代理無法接聽來電的時間，例如星期四 8:00 P.M. 或星期天 2:30 P.M.)。

**Get-CsRgsHoursOfBusiness** Cmdlet 能讓您擷取設定供組織使用之營業時間集合的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsRgsHoursOfBusiness** Cmdlet：RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsRgsHoursOfBusiness"}

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
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>表示主控營業時間集合的服務識別，或是集合本身的完整識別。如果您有指定服務識別 (例如 service:ApplicationServer:atl-cs-001.litwareinc.com)，將會傳回位於該服務的所有營業時間集合。如果您有指定集合的識別，則只會傳回指定的營業時間集合。請注意，營業時間集合的識別是由服務識別後面加上全域唯一識別碼 (GUID) 所組成，例如：service:ApplicationServer-1/1987d3c2-4544-489d-bbe3-59f79f530a83.</p>
<p>還有另一種方法可傳回營業時間集合，就是指定服務識別，然後再加上 Name 參數和集合名稱。如此一來，您無須知道該集合的 GUID 指派，就能擷取特定的營業時間集合。</p>
<p>呼叫若未使用任何參數，<strong>Get-CsRgsHoursOfBusiness</strong> 會傳回設定供組織使用之所有營業時間的集合。</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>建立營業時間集合時指定給該集合的唯一名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>Owner</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>「擁有」營業時間之集區的完整網域名稱。擁有者集區識別碼和營業時間集合的集區識別碼通常一樣。然而，如果需要暫時移動集合 (可能在災害復原程序中)，則集區識別碼將會變更。不過，擁有者識別碼會繼續指向原始集區。</p></td>
</tr>
<tr class="even">
<td><p><em>ShowAll</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定此參數，會顯示所有回應群組營業時間集合，包括擁有者集區識別碼與集區識別碼不同的那些集合。根據預設，Get-CsRgsHoursOfBusiness 只會傳回擁有者集區識別碼與集區識別碼相同之營業時間集合的的資訊。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsRgsHoursOfBusiness** 不接受管線傳送的輸入。

## 傳回類型

傳回 Microsoft.Rtc.Rgs.Management.WritableSettings.BusinessHours 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsRgsHoursOfBusiness](new-csrgshoursofbusiness.md)  
[Remove-CsRgsHoursOfBusiness](remove-csrgshoursofbusiness.md)  
[Set-CsRgsHoursOfBusiness](set-csrgshoursofbusiness.md)

