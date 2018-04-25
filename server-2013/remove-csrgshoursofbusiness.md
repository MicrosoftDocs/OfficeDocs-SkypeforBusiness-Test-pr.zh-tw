---
title: Remove-CsRgsHoursOfBusiness
TOCTitle: Remove-CsRgsHoursOfBusiness
ms:assetid: 753b2cd7-709b-455b-85a3-8b80ea35d4e0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398568(v=OCS.15)
ms:contentKeyID: 49291329
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsRgsHoursOfBusiness

 

_**上次修改主題的時間：** 2015-03-09_

移除回應群組營業時間的現有集。營業時間可用以指定回應群組代理在一週中會正常接聽來電的日子與時段。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsRgsHoursOfBusiness -Instance <BusinessHours> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會移除在 ApplicationServer:atl-cs-001.litwareinc.com 服務上找到的所有營業時間集。為達此目的，命令會先呼叫 **Get-CsRgsHoursOfBusiness** 傳回在 ApplicationServer:atl-cs-001.litwareinc.com 服務上找到的所有營業時間集。然後再將這些集合管線傳送到 **Remove-CsRgsHoursOfBusiness** Cmdlet，以刪除傳遞而來的每一個營業時間集。

    Get-CsRgsHoursOfBusiness -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" | Remove-CsRgsHoursOfBusiness

## 範例 2

在範例 2 中，營業時間的單一集會從 ApplicationServer:atl-cs-001.litwareinc.com 移除：名為 Help Desk Business Hours 的集合。

    Get-CsRgsHoursOfBusiness -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" -Name "Help Desk Business Hours" | Remove-CsRgsHoursOfBusiness

## 範例 3

範例 3 會刪除已為星期日設定營業時間的所有營業時間集。為達此目的，命令會先呼叫 **Get-CsRgsHoursOfBusiness** 傳回在 ApplicationServer:atl-cs-001.litwareinc.com 上找到的所有營業時間集。這些集合會傳送到 **Where-Object** Cmdlet，以選取符合下列其中一項準則的項目：SundayTimeRange1 屬性不等於 Null 值，或 SundayTimeRange2 屬性不等於 Null 值 (如果時間範圍屬性不是 Null，即表示已為該時間間隔設定營業時間)。凡至少符合其中一項準則的集合，皆會傳送到 **Remove-CsRgsHoursOfBusiness** Cmdlet，以移除該營業時間集。

    Get-CsRgsHoursOfBusiness -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" | Where-Object {$_.SundayTimeRange1 -ne $Null -or $_.SundayTimeRange2 -ne $Null} | Remove-CsRgsHoursOfBusiness

## 範例 4

範例 4 所示的命令會刪除所有自訂的營業時間集 (亦即無法在工作流程中共用的集)。為達此目的，命令會先使用 **Get-CsRgsHoursOfBusiness** 傳回在 ApplicationServer:atl-cs-001.litwareinc.com 上找到的所有營業時間集。然後再將該資料管線傳送到 **Where-Object** Cmdlet，以選取 Custom 內容為 True 的集合。接著將這些集合管線傳送到 **Remove-CsRgsHoursOfBusiness** 加以刪除。

    Get-CsRgsHoursOfBusiness -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" | Where-Object {$_.Custom -eq $True} | Remove-CsRgsHoursOfBusiness -Force

## 詳細描述

為了提供給來電者最佳的服務經驗，回應群組應用程式 讓您可以清楚定義回應群組代理何時可接聽電話，何時無法接聽電話。透過 回應群組應用程式，您可以定義營業時間，這些時間指出代理在一星期的哪幾天和那些時段可接聽來電。例如，如果您組織的營業時間是星期一到星期五的 9:00 A.M. 到 5:00 P.M.，那麼您可以設定營業時間中顯示代理會在星期一到星期五的 9:00 A.M. 到 5:00 P.M. 接聽來電 (以及該分機代理無法接聽來電的時間，例如星期四 8:00 P.M. 或星期天 2:30 P.M.)。

使用 **New-CsRgsHoursOfBusiness** Cmdlet 可建立新的營業時間集；稍後可使用 **Remove-CsRgsHoursOfBusiness** Cmdlet 移除這些集合。請注意，呼叫 **Remove-CsRgsHoursOfBusiness** 會移除整個時間集，且移除後該集就無法再使用。如果要移除特定日期的營業時間 (例如，服務台不再於星期天開放)，您必須使用 **Set-CsRgsHoursOfBusiness**，以從集當中只移除適用的值。

根據預設，如果您嘗試刪除使用中工作流程目前使用的營業時間集，**Remove-CsRgsHoursOfBusiness** 會提示您。該提示會要求您確認是否要移除集，並且在您回應提示之前不會採取任何動作。若要略過此提示，即使這些營業時間集目前是指派給使用中的工作流程，也要以無訊息的方式刪除，請新增 Force 參數。例如：

Get-CsRgsHoursOfBusiness –Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" | Remove-CsRgsHoursOfBusiness –Force

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsRgsHoursOfBusiness** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsRgsHoursOfBusiness"}

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
<td><p><em>Instance</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.BusinessHours</p></td>
<td><p>指向要移除之營業時間集的物件參考。將工作流程物件傳送到 <strong>Remove-CsRgsHoursOfBusiness</strong> 時，您可以省略 Instance 參數。</p>
<p>若要使用 Instance 參數，請使用類似下列的命令：</p>
<p>$x = Get-CsRgsHoursOfBusiness –Identity ApplicationServer:atl-cs-001.litwareinc.com /1987d3c2-4544-489d-bbe3-59f79f530a83</p>
<p>Remove-CsRgsHoursOfBusiness –Instance $x</p>
<p>請注意，使用 Instance 參數時，您一次只能移除一個營業時間集。這表示物件參考 ($x) 不能包含多個營業時間物件。</p></td>
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
<td><p>強制刪除營業時間集。如果設定此參數，即使集目前指派給作用中的工作流程，它仍然會被刪除而不會有警告。如果沒有設定此參數，則系統會要求您確認是否刪除目前指派給作用中工作流程的任何營業時間集。</p></td>
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

Microsoft.Rtc.Rgs.Management.WritableSettings.BusinessHours 物件。**Remove-CsRgsHoursOfBusiness** 接受管線傳送的回應群組營業時間物件執行個體。

## 傳回類型

刪除現有的 Microsoft.Rtc.Rgs.Management.WritableSettings.BusinessHours 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsRgsHoursOfBusiness](get-csrgshoursofbusiness.md)  
[New-CsRgsHoursOfBusiness](new-csrgshoursofbusiness.md)  
[Set-CsRgsHoursOfBusiness](set-csrgshoursofbusiness.md)

