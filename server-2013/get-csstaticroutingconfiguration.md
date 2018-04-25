---
title: Get-CsStaticRoutingConfiguration
TOCTitle: Get-CsStaticRoutingConfiguration
ms:assetid: 94f126b4-b714-42ba-b9b6-81269634875f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398754(v=OCS.15)
ms:contentKeyID: 49291696
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsStaticRoutingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織所使用之靜態路由組態設定的資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsStaticRoutingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsStaticRoutingConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回您組織中使用之所有靜態路由組態集合的資訊。

    Get-CsStaticRoutingConfiguration

## 範例 2

範例 2 會傳回下列單一靜態路由組態集合 (即 Identity 為 service:Registrar:atl-cs-001.litwareinc.com 的集合) 的資訊。

    Get-CsStaticRoutingConfiguration -Identity "service:Registrar:atl-cs-001.litwareinc.com"

## 範例 3

範例 3 會使用 Filter 參數，傳回指派給服務範圍之靜態路由組態集合的資訊。篩選值 "service:\*" 會將傳回的資料限制在其 Identity 以字串值 "service:" 開頭的集合。

    Get-CsStaticRoutingConfiguration -Filter "service:*"

## 範例 4

範例 4 會針對組織中使用的所有靜態路由組態集合傳回詳細的路由資訊。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsStaticRoutingConfiguration** Cmdlet，以傳回每個靜態路由集合的完整資訊。然後再將此資訊管線傳送到 **Select-Object** Cmdlet，以使用 ExpandProperty 參數來「展開」Route 屬性的值。當您展開屬性時，該屬性內包含的所有物件與值都會以易讀的方式顯示於螢幕上。

    Get-CsStaticRoutingConfiguration | Select-Object -ExpandProperty Route

## 範例 5

範例 5 所示的命令會傳回所有設定為僅符合電話統一資源識別元 (URI) 之靜態路由的資訊。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsStaticRoutingConfiguration** Cmdlet，以傳回所有靜態路由組態集合及其相關路由。然後，此集合會管線傳送到 **Select-Object** Cmdlet，以使用 ExpandProperty 展開儲存在 Route 屬性中的所有物件。接著將這些路由物件管線傳送到 **Where-Object** Cmdlet，這會只挑出 MatchOnlyPhoneUri 屬性等於 True 的路由。

    Get-CsStaticRoutingConfiguration | Select-Object -ExpandProperty Route | Where-Object {$_.MatchOnlyPhoneUri -eq $True}

## 詳細描述

當您傳送 SIP 訊息給某人，該訊息可能需要在傳遞之前周遊多個子網路和網路；訊息所經歷的路徑通常稱為路由。網路中有兩種路由類型：動態和靜態。透過動態路由，伺服器使用演算法判斷訊息應轉送的下一個位置 (下一個躍點)。透過靜態路由，訊息路徑由系統管理員預先決定。當伺服器接收到訊息，伺服器會檢查訊息位址，然後將訊息轉送至已由管理員預先決定的下一個躍點伺服器。如果設定正確，靜態路由會協助確保及時並正確地傳遞訊息，且在伺服器上只要最小限度的監聽。靜態路由的缺點是在網路故障時，無法動態地重新路由傳送訊息。

安裝 Lync Server 時，會自動為您建立全域的靜態路由集合 (雖然會建立集合，但並不會指派任何路由給該集合)。此外，此軟體可讓您建立其他套用至服務範圍的集合 (這些新的集合只能指派給登錄器服務)。**Get-CsStaticRoutingConfiguration** Cmdlet 提供一種方法，可讓您傳回組織中使用之所有靜態路由組態集合的資訊。這包括能夠傳回指派給集合之每個路由的詳細資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsStaticRoutingConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsStaticRoutingConfiguration"}

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
<td><p>可讓您在指定要傳回的靜態路由組態集合時使用萬用字元。例如，此語法會傳回所有在服務範圍設定的靜態路由集合：-Filter &quot;service:*&quot;。</p>
<p>請注意，您不能在同一個命令中同時使用 Identity 和 Filter 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>靜態路由組態集合的唯一識別碼。若要傳回全域集合的資訊，請使用下列語法：-Identity global。若要擷取在服務範圍設定之集合的資訊，請使用下列語法：-Identity &quot;service:Registrar:atl-cs-001.litwareinc.com&quot;。請注意，如有指定 Identity，即無法使用萬用字元。如果您需要使用萬用字元，請改用 Filter 參數。</p>
<p>如果您未加入 Identity 或 Filter 參數，則 <strong>Get-CsStaticRoutingConfiguration</strong> Cmdlet 會傳回您所有靜態路由組態集合的資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區 的本機複本擷取靜態路由組態資料，而非從 中央管理存放區 本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsStaticRoutingConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsStaticRoutingConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.RoutingSettings 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsStaticRoutingConfiguration](new-csstaticroutingconfiguration.md)  
[Remove-CsStaticRoutingConfiguration](remove-csstaticroutingconfiguration.md)  
[Set-CsStaticRoutingConfiguration](set-csstaticroutingconfiguration.md)

