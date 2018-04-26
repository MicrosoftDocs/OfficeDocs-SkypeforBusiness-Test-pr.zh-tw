---
title: New-CsStaticRoutingConfiguration
TOCTitle: New-CsStaticRoutingConfiguration
ms:assetid: 30d1736f-990f-46e8-931f-9247cd988244
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425811(v=OCS.15)
ms:contentKeyID: 49290498
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsStaticRoutingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

建立新的靜態路由組態設定集合。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsStaticRoutingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Route <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會建立 Identity 為 service:Registrar:atl-cs-001.litwareinc.com 的新靜態路由組態集合。因為未在命令中加入 Route 參數，因此不會將任何靜態路由指派給新集合。

    New-CsStaticRoutingConfiguration -Identity "service:Registrar:atl-cs-001.litwareinc.com" 

## 範例 2

範例 2 所示的命令會建立使用 TCP 做為其傳輸的新 SIP Proxy 路由；然後，這個新路由會新增至新的靜態路由組態集合。為達成此目的，範例中的第一個命令會使用 **New-CsStaticRoute** Cmdlet 建立一個指向下一個躍點伺服器，且 IP 位址為 192.168.1.100 的新路由。這個新路由 (以名稱為 $x 的變數儲存) 也會使用連接埠 8025 以及 MatchUri "\*.litwareinc.com"。

然後再呼叫 **New-CsStaticRoutingConfiguration** Cmdlet 建立新的集合 (Identity 為 service:Registrar:atl-cs-001.litwareinc.com)，並將儲存在變數 $x 中的路由指派給新集合的 Route 屬性。

    $x = New-CsStaticRoute -TCPRoute -Destination "192.168.0.100" -Port 8025 -MatchUri "*.litwareinc.com"
    
    New-CsStaticRoutingConfiguration -Identity "service:Registrar:atl-cs-001.litwareinc.com" -Route $x

## 詳細描述

當您傳送 SIP 訊息給某人，該訊息可能需要在傳遞之前周遊多個子網路和網路；訊息所經歷的路徑通常稱為路由。在網路中，有兩種路由類型：動態及靜態。使用動態路由時，伺服器會使用演算法來決定應該將訊息轉送到的下一個位置 (下一個躍點)。使用靜態路由時，訊息路徑是由系統管理員預先決定的。當伺服器收到訊息時，該伺服器會檢查訊息位址，然後將該訊息轉送到系統管理員預先設定的下一個躍點伺服器。如果設定正確，靜態路由有助於確保訊息即時且準確送達，而且可將伺服器竊聽減到最少。靜態路由的缺點是在網路故障時，無法動態地重新路由傳送訊息。

安裝 Lync Server 時，會自動為您建立全域的靜態路由集合。除此之外，您可以使用 **New-CsStaticRoutingConfiguration** Cmdlet 來建立其他集合以及網站範圍或服務範圍 (僅適用於登錄器服務)。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsStaticRoutingConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsStaticRoutingConfiguration"}

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
<td><p>要建立之新靜態路由集合的唯一識別碼。新的集合只能在服務範圍建立，而且只能指派給登錄程式服務。因此，新集合的 Identity 看起來必須類似如下：-Identity &quot;service:Registrar:atl-cs-001.litwareinc.com&quot;。</p></td>
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
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="odd">
<td><p><em>Route</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>集合中保持的個別靜態路由。要新增至集合的路由必須是從另一個集合複製而來，或是使用 <strong>New-CsStaticRoute</strong> 建立。如需詳細資訊，請參閱本主題中的＜範例＞區段。</p></td>
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

無。**New-CsStaticRoutingConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsStaticRoutingConfiguration** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.RoutingSettings 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsStaticRoutingConfiguration](get-csstaticroutingconfiguration.md)  
[New-CsStaticRoute](new-csstaticroute.md)  
[Remove-CsStaticRoutingConfiguration](remove-csstaticroutingconfiguration.md)  
[Set-CsStaticRoutingConfiguration](set-csstaticroutingconfiguration.md)

