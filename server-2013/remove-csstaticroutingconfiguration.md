---
title: Remove-CsStaticRoutingConfiguration
TOCTitle: Remove-CsStaticRoutingConfiguration
ms:assetid: 844e849e-a2f6-42fd-a49c-1ab234a07a65
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398668(v=OCS.15)
ms:contentKeyID: 49291529
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsStaticRoutingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除指定的靜態路由組態設定集合。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsStaticRoutingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會移除 Identity 為 service:Registrar:atl-cs-001.litwareinc.com 的靜態路由組態集合。

    Remove-CsStaticRoutingConfiguration -Identity "service:Registrar:atl-cs-001.litwareinc.com"

## 範例 2

範例 2 會移除所有套用至服務範圍的靜態路由組態集合。為達成此目的，命令會先使用 **Get-CsStaticRoutingConfiguration** Cmdlet 並搭配 Filter 參數；篩選值 "service:\*" 可將傳回的資料限制在 Identity 開頭為字串值 "service:" 的集合。然後再將篩選後的集合管線傳送到 **Remove-CsStaticRoutingConfiguration** Cmdlet，以刪除集合中的每個項目。

    Get-CsStaticRoutingConfiguration -Filter "service:*" | Remove-CsStaticRoutingConfiguration

## 範例 3

範例 3 顯示如何刪除所有尚未指派任何實際路由的靜態路由組態集合。為了執行此工作，命令會先呼叫 **Get-CsStaticRoutingConfiguration** Cmdlet，以傳回組織中所使用之所有靜態路由集合的資訊。然後再將此集合管線傳送至 **Where-Object** Cmdlet，這會只挑出路由數目 (Route.Count) 等於 0 的集合。接著將篩選後的資訊管線傳送至 **Remove-CsStaticRoutingConfiguration** Cmdlet，以刪除每個未獲指派至少一個路由的集合。

    Get-CsStaticRoutingConfiguration | Where-Object {$_.Route.Count -eq 0} | Remove-CsStaticRoutingConfiguration

## 詳細描述

當您傳送 SIP 訊息給某人，該訊息可能需要在傳遞之前周遊多個子網路和網路；訊息所經歷的路徑通常稱為路由。網路中有兩種路由類型：動態和靜態。透過動態路由，伺服器使用演算法判斷訊息應轉送的下一個位置 (下一個躍點)。透過靜態路由，訊息路徑由系統管理員預先決定。當伺服器接收到訊息，伺服器會檢查訊息位址，然後將訊息轉送至已由管理員預先決定的下一個躍點伺服器。如果設定正確，靜態路由會協助確保及時並正確地傳遞訊息，且在伺服器上只要最小限度的監聽。靜態路由的缺點是在網路故障時，無法動態地重新路由傳送訊息。

安裝 Lync Server 時，會自動為您建立全域的靜態路由集合 (雖然會建立集合，但並不會指派任何路由給該集合)。此外，此軟體可讓您建立其他套用至服務範圍的集合 (這些新的集合只能指派給登錄器服務)。如果您稍後改變心意，可以使用 **Remove-CsStaticRoutingConfiguration** Cmdlet，刪除套用至服務範圍的集合。

您也可以對全域集合執行 **Remove-CsStaticRoutingConfiguration** Cmdlet。但在此狀況下不會移除全域集合；因為 Lync Server 不容許您移除全域集合。而是會將全域集合內的所有屬性都重設為預設值。這表示所有指派給全域集合的路由都將遭到刪除。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsStaticRoutingConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsStaticRoutingConfiguration"}

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
<td><p>要移除之靜態路由組態集合的唯一識別碼。若要移除在服務範圍設定的集合，請使用下列語法：-Identity &quot;service:Registrar:atl-cs-001.litwareinc.com&quot;。</p>
<p>您也可以對全域集合執行 <strong>Remove-CsStaticRoutingConfiguration</strong> Cmdlet；若要執行此工作，請使用下列語法：-Identity global。但是請記住，這樣並不會真的移除全域集合，而是將該集合中的屬性重設為預設值。這表示 Route 屬性中的所有項目都將遭到刪除。</p></td>
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
<td><p>隱藏顯示當執行命令時可能發生的任何非嚴重錯誤訊息。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.RoutingSettings 物件。**Remove-CsStaticRoutingConfiguration** Cmdlet 接受管線傳送的靜態路由設定物件執行個體。

## 傳回類型

**Remove-CsStaticRoutingConfiguration** Cmdlet 不會傳回值或物件，而會刪除 Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.RoutingSettings 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsStaticRoutingConfiguration](get-csstaticroutingconfiguration.md)  
[New-CsStaticRoutingConfiguration](new-csstaticroutingconfiguration.md)  
[Set-CsStaticRoutingConfiguration](set-csstaticroutingconfiguration.md)

