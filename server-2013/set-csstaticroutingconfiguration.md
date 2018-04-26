---
title: Set-CsStaticRoutingConfiguration
TOCTitle: Set-CsStaticRoutingConfiguration
ms:assetid: 8f3e923e-f1e1-4a22-8252-5ef24fbc3cb3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398724(v=OCS.15)
ms:contentKeyID: 49291643
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsStaticRoutingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的靜態路由組態設定集合。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsStaticRoutingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsStaticRoutingConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Route <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會從全域靜態路由集合複製路由，然後將該路由指派給另一個靜態路由集合 (也就是 Identity 為 service:Registrar:atl-cs-001.litwareinc.com 的靜態路由集合)。若要執行此工作，範例中的第一個命令會連線到全域集合，並傳回具有 MatchUri litwareinc.com 且 MatchOnlyPhoneUri 等於 True 之路由的物件參考。

為達成此目的，命令會呼叫 **Get-CsStaticRoutingConfiguration** Cmdlet 傳回全域路由靜態組態集合的資訊。然後再將該資料管線傳送到 **Select-Object** Cmdlet，以使用 ExpandProperty 參數展開 Route 屬性中的值。接著將展開後的值 (亦即指派給集合的個別路由) 管線傳送到 **Where-Object** Cmdlet，這會挑出 MatchUri 屬性等於 litwareinc.com 且 MatchOnlyPhoneUri 屬性等於 True 的路由。傳回的路由會儲存在名為 $x 的變數中。

擷取路由之後，範例中的第二個命令會將該路由新增至服務：Registrar:atl-cs-001.litwareinc.com 集合。為達成此目的，會呼叫 **Set-CsStaticRoutingConfiguration** Cmdlet 並搭配 Route 參數；參數值 @{Add=$x} 會指示 **Set-CsStaticRoutingConfiguration** Cmdlet 將儲存在變數 $x 中的路由附加到 Route 屬性所維護之路由的集合。

    $x = Get-CsStaticRoutingConfiguration -Identity global | Select-Object -ExpandProperty Route | Where-Object {$_.MatchUri -eq "litwareinc.com" -and $_.MatchOnlyPhoneUri -eq $True}
    
    Set-CsStaticRoutingConfiguration -Identity service:Registrar:atl-cs-001.litwareinc.com -Route @{Add=$x}

## 範例 2

範例 2 所示的命令會從靜態路由集合中刪除路由。為達成此目的，範例中的第一個命令會連線到 Identity 為 service:Registrar:atl-cs-001.litwareinc.com 的集合，並傳回 MatchUri 等於 litwareinc.com 且 MatchOnlyPhoneUri 等於 True 之路由的物件參考。為達成此目的，命令會呼叫 **Get-CsStaticRoutingConfiguration** Cmdlet，以從 service:Registrar:atl-cs-001.litwareinc.com 集合傳回資訊。然後再將該資料管線傳送到 **Select-Object** Cmdlet，以使用 ExpandProperty 參數展開 Route 屬性中的值。接著將展開後的值 (亦即指派給集合的個別路由) 管線傳送到 **Where-Object** Cmdlet，這會挑出 MatchUri 屬性等於 litwareinc.com 且 MatchOnlyPhoneUri 屬性等於 True 的路由。傳回的路由會儲存在名為 $x 的變數中。

擷取路由之後，第二個命令會從集合中刪除該路由。為達成此目的，會呼叫 **Set-CsStaticRoutingConfiguration** Cmdlet 並搭配 Route 參數；參數值 @{Remove=$x} 會指示 **Set-CsStaticRoutingConfiguration** Cmdlet 刪除變數 $x 中所儲存的路由。

    $x = Get-CsStaticRoutingConfiguration -Identity service:Registrar:atl-cs-001.litwareinc.com | Select-Object -ExpandProperty Route | Where-Object {$_.MatchUri -eq "litwareinc.com" -and $_.MatchOnlyPhoneUri -eq $True}
    
    Set-CsStaticRoutingConfiguration -Identity service:Registrar:atl-cs-001.litwareinc.com -Route @{Remove=$x}

## 範例 3

範例 3 會示範如何刪除指派給靜態路由組態集合的所有路由。若要執行此作業，只要加入 Route 參數，並將參數值設為 Null 即可。當命令完成後，集合依舊存在，但不再會有任何路由指派。

    Set-CsStaticRoutingConfiguration -Identity service:Registrar:atl-cs-001.litwareinc.com -Route $Null

## 詳細描述

當您傳送 SIP 訊息給某人，該訊息可能需要在傳遞之前周遊多個子網路和網路；訊息所經歷的路徑通常稱為路由。在網路中，有兩種路由類型：動態及靜態。使用動態路由時，伺服器會使用演算法來決定應該將訊息轉送到的下一個位置 (下一個躍點)。使用靜態路由時，訊息路徑是由系統管理員預先決定的。當伺服器收到訊息時，該伺服器會檢查訊息位址，然後將該訊息轉送到系統管理員預先設定的下一個躍點伺服器。如果設定正確，靜態路由有助於確保訊息即時且準確送達，而且可將伺服器竊聽減到最少。靜態路由的缺點是在網路故障時，無法動態地重新路由傳送訊息。

安裝 Lync Server 時，會自動為您建立全域的靜態路由集合 (該集合已建立，但沒有指派給該集合的路由)。此外，此軟體也可讓您建立套用至服務範圍的其他集合 (這些新集合只能指派給登錄程式服務)。**Set-CsStaticRoutingConfiguration** Cmdlet 可讓您修改現有靜態路由集合的屬性值。也就是說，您可以使用該 Cmdlet 將新路由新增至集合，或從集合刪除現有的路由。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsStaticRoutingConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsStaticRoutingConfiguration"}

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
<td><p>隱藏顯示當執行命令時可能發生的任何非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要修改之靜態路由組態集合的唯一識別碼。若要修改全域集合，請使用下列語法：-Identity global。若要修改套用至服務範圍的集合，請使用類似下列的語法：-Identity &quot;service:Registrar:atl-cs-001.litwareinc.com&quot; 您無法在指定 Identity 時使用萬用字元。</p>
<p>若未加入此參數，<strong>Set-CsStaticRoutingConfiguration</strong> Cmdlet 將自動修改全域集合。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>RoutingSettings 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>Route</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>集合中保持的個別靜態路由。要新增至集合的路由必須從其他集合複製，或使用 <strong>New-CsStaticRoute</strong> Cmdlet 建立；若要從集合刪除路由，必須先建立該路由的物件參考。如需詳細資訊，請參閱說明主題中的＜範例＞區段。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.RoutingSettings 物件。**Set-CsStaticRoutingConfiguration** Cmdlet 接受管線傳送的靜態路由設定物件執行個體。

## 傳回類型

**Set-CsStaticRoutingConfiguration** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.RoutingSettings 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsStaticRoutingConfiguration](get-csstaticroutingconfiguration.md)  
[New-CsStaticRoute](new-csstaticroute.md)  
[New-CsStaticRoutingConfiguration](new-csstaticroutingconfiguration.md)  
[Remove-CsStaticRoutingConfiguration](remove-csstaticroutingconfiguration.md)

