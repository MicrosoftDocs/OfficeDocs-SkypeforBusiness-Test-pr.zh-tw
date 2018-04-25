---
title: Set-CsRgsHoursOfBusiness
TOCTitle: Set-CsRgsHoursOfBusiness
ms:assetid: be976e84-00aa-46d5-94d3-527c4c9f3963
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412929(v=OCS.15)
ms:contentKeyID: 49292163
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsRgsHoursOfBusiness

 

_**上次修改主題的時間：** 2015-03-09_

設定現有的回應群組營業時間集合。營業時間集合可用以指定回應群組代理在一週中可以正常接聽來電的日子與時段。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsRgsHoursOfBusiness -Instance <BusinessHours> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 顯示您可以將新的時間範圍值指派給 Help Desk Business Hours 營業時間集的 SaturdayHours1 和 SundayHours1 屬性。為達此目的，範例中的第一個命令會使用 **New-CsRgsTimeRange** 建立新的時間範圍物件 (Weekend Hours)，開始時間為 12:00 P.M. (12:00)，結束時間為 5:00 P.M. (17:00)。此物件儲存在名為 $weekend 的變數中。

下個命令會在 ApplicationServer:atl-cs-001.litwareinc.com 建立 Help Desk Business Hours 營業時間集的物件參考 ($x)。該命令完成後，會使用命令 3 與 4 將 SaturdayHours1 與 SundayHours1 屬性設為儲存在 $weekend 的時間範圍值。最後，範例中的最後一個命令會使用 **Set-CsRgsHoursOfBusiness** 將這些變更寫回到實際的營業時間集。

    $weekend = New-CsRgsTimeRange -Name "Weekend Hours" -OpenTime "12:00" -CloseTime "17:00"
    
    $x = Get-CsRgsHoursOfBusiness -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" -Name "Help Desk Business Hours"
    $x.SaturdayHours1 = $weekend
    $x.SundayHours1 = $weekend
    Set-CsRgsHoursOfBusiness -Instance $x

## 範例 2

範例 2 所示的命令會刪除 Help Desk Business Hours 營業時間集中所設定的 SaturdayHours1 和 SaturdayHours2 屬性值。為達此目的，第一個命令會在 ApplicationServer:atl-cs-001.litwareinc.com 建立 Help Desk Business Hours 營業時間集的物件參考 ($x)。在建立參考物件後，第二個命令會將 SaturdayHours1 屬性設為 Null 值 ($Null)；這會有效的清除任何先前指派給 SaturdayHours1 的值。然後，使用類似命令清除先前指派給 SaturdayHours2 的任何值。

範例中的最後一個命令會使用 **Set-CsRgsHoursOfBusiness** 將這些變更寫回到實際的營業時間集。當命令執行完成時，就不會再有任何 Saturday 營業時間指派給 Help Desk Business Hours。

    $x = Get-CsRgsHoursOfBusiness -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" -Name "Help Desk Business Hours"
    $x.SaturdayHours1 = $Null
    $x.SaturdayHours2 = $Null
    
    Set-CsRgsHoursOfBusiness -Instance $x

## 詳細描述

為了提供給來電者最佳的服務經驗，回應群組應用程式 讓您可以清楚定義回應群組代理何時可接聽電話，何時無法接聽電話。透過 回應群組應用程式，您可以定義營業時間，這些時間指出代理在一星期的哪幾天和那些時段可接聽來電。例如，如果您組織的營業時間是星期一到星期五的 9:00 A.M. 到 5:00 P.M.，那麼您可以設定營業時間中顯示代理會在星期一到星期五的 9:00 A.M. 到 5:00 P.M. 接聽來電 (以及該分機代理無法接聽來電的時間，例如星期四 8:00 P.M. 或星期天 2:30 P.M.)。

使用 **New-CsRgsHoursOfBusiness** Cmdlet 可建立營業時間集。建立營業時間集後，可使用 **Set-CsRgsHoursOfBusiness** Cmdlet 修改這些營業時間集，通常這表示可變更一週中一或多天的營業時間。例如，如果服務台過去在星期五的服務時間為到 5:00 P.M. 為止，現在星期五的服務時間要延長到 7:00 P.M.，您必須修改星期五的營業時間。如果服務台過去在星期六會提供服務，現在星期六停止服務，同樣的您必須修改星期六的營業時間(若要指出某個群組無法在特定的日子使用，只要將該日的營業時間設為 Null 值：-SundayTimeRange1 $Null)。

在營業時間集內設定營業時間時，請記住一星期的每一天都有 Hours1 和 Hours2 屬性。如果您服務台的服務時間是 8:00 A.M. 到 5:00 P.M.，您只需要將值指派到適當的 Hours1 屬性即可。但假設服務台的服務時間是 8:00 A.M.到 2:00 P.M.，然後再於 5:00 P.M.到 11:00 P.M.提供服務。在此狀況下，您必須將 8:00 A.M.到 2:00 P.M.的時間範圍指派給 Hours1，5:00 P.M. 到 11:00 P.M. 指派給 Hours2。

請注意，**Set-CsRgsHoursOfBusiness** 不會直接修改營業時間集，而是您必須使用 **Get-CsRgsHoursOfBusiness** 為待修改的營業時間集建立物件參考(建立物件參考時，只要擷取營業時間集的複本，再將該複本儲存在變數中即可)。建立物件參考後，您可以為只存在於記憶體中的物件修改屬性。完成修改後，接著您可以使用 **Set-CsRgsHoursOfBusiness** 將那些變更寫入實際的營業時間集。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsRgsHoursOfBusiness** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsRgsHoursOfBusiness"}

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
<td><p>待修改營業時間集的物件參考。物件參考通常是使用 <strong>Get-CsRgsHoursOfBusiness</strong> Cmdlet 來擷取，並將傳回的值指派至變數；例如，此命令將物件參考傳回至佇列 Help Desk 營業時間集，並將該物件參考儲存在名為 $x 的變數中：</p>
<p>$x = Get-CsRgsHoursOfBusiness -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name &quot;Help Desk&quot;</p></td>
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
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Rgs.Management.WritableSettings.BusinessHours 物件。**Set-CsRgsHoursOfBusiness** 接受管線傳送的回應群組營業時間物件執行個體。

## 傳回類型

修改現有的 Microsoft.Rtc.Rgs.Management.WriteableSettings.BusinessHours 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsRgsHoursOfBusiness](get-csrgshoursofbusiness.md)  
[New-CsRgsHoursOfBusiness](new-csrgshoursofbusiness.md)  
[New-CsRgsTimeRange](new-csrgstimerange.md)  
[Remove-CsRgsHoursOfBusiness](remove-csrgshoursofbusiness.md)

