---
title: Get-CsVoiceRoute
TOCTitle: Get-CsVoiceRoute
ms:assetid: 422abb2d-bff3-4b9a-b18c-d8202b01f69b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425926(v=OCS.15)
ms:contentKeyID: 49290731
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsVoiceRoute

 

_**上次修改主題的時間：** 2015-03-09_

傳回已設定供組織使用之語音路由的資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsVoiceRoute [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsVoiceRoute [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

擷取組織內定義的所有語音路由的屬性。

    Get-CsVoiceRoute

## 範例 2

擷取 Route1 語音路由的屬性。

    Get-CsVoiceRoute -Identity Route1

## 範例 3

此命令會顯示 Identity 值內任何位置含有 "test" 字串的語音路由設定。若只要尋找 Identity 尾端的 test 字串，請使用 \*test 值。同樣地，若只要尋找 Identity 開頭出現的 test 字串，請指定 test\* 值。

    Get-CsVoiceRoute -Filter *test*

## 範例 4

此命令會擷取尚未指派任何 PSTN 閘道的所有語音路由，首先會使用 **Get-CsVoiceRoute** Cmdlet 以擷取所有語音路由。然後，將這些語音路由傳送給 **Where-Object** Cmdlet。**Where-Object** Cmdlet 會縮減 Get 作業的結果。在此案例中，我們查看每一個語音路由 (也就是 $\_ 所代表的意義)，並檢查 PstnGatewayList 屬性的 Count 屬性。如果 PSTN 閘道的計數是 0，清單為空白，表示路由未定義任何閘道。

    Get-CsVoiceRoute | Where-Object {$_.PstnGatewayList.Count -eq 0}

## 詳細描述

使用此 Cmdlet 來擷取一或多個現有的語音路由。語音路由包含一些指示，告知 Lync Server 如何將 Enterprise Voice 使用者的來電轉接至公用交換電話網路 (PSTN) 或專用交換機 (PBX) 上的電話號碼。

此 Cmdlet 可用來擷取語音路由的資訊，例如：與路由相關聯的 PSTN 閘道 (若有的話)、與路由相關聯的 PSTN 使用方式、識別套用路由之電話號碼的模式 (格式為規則運算式)，以及來電者識別碼設定。PSTN 使用方式會讓語音路由與語音原則產生關聯。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsVoiceRoute** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsVoiceRoute"}

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
<td><p>此參數會根據傳遞給此參數的萬用字元值，篩選 Get 作業的結果。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>可唯一識別語音路由的字串。若未提供識別，會傳回組織的所有語音路由。</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區 的本機複本擷取語音路由，而非從 中央管理存放區 本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

此 Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsVoiceRoute](new-csvoiceroute.md)  
[Remove-CsVoiceRoute](remove-csvoiceroute.md)  
[Set-CsVoiceRoute](set-csvoiceroute.md)  
[Test-CsVoiceRoute](test-csvoiceroute.md)

