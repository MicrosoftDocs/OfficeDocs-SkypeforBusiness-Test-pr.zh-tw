---
title: 在 Lync Server 2013 中啟用位置基礎路由
TOCTitle: 在 Lync Server 2013 中啟用位置基礎路由
ms:assetid: 029ede7e-0c4e-4ad2-af99-909ae674d6fe
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994014(v=OCS.15)
ms:contentKeyID: 52056042
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中啟用位置基礎路由

 

_**上次修改主題的時間：** 2015-03-09_

一旦 企業語音 完成部署且定義了網路區域、網站和子網路，您就可以啟用位置基礎路由。必須為下列 企業語音 元素啟用位置基礎路由：

  - 網站

  - 主幹組態

  - 語音原則

  - 路由組態

## 對網站啟用位置基礎路由

在您部署 企業語音 且設定網站後，就可以設定位置基礎路由。首先，您需要建立語音路由原則，以將網站與適當的 PSTN 使用方式建立關聯。指派 PSTN 使用方式給語音路由原則時，請務必採用與下列語音路由關聯的 PSTN 使用方式：使用網站之本機 PSTN 閘道，或位於不需位置基礎路由相關限制之區域的 PSTN 閘道。使用 Lync ServerWindows PowerShell 命令、New-CsVoiceRoutingPolicy 或 Lync Server 控制台 建立語音路由原則。

    New-CsVoiceRoutingPolicy -Identity <voice routing policy ID> -Name <voice routing policy name> -PstnUsages <usages>

如需詳細資訊，請參閱＜[New-CsVoiceRoutingPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsVoiceRoutingPolicy)＞。

就此範例而言，下表和 Windows PowerShell 命令說明了此案例中定義的兩種語音路由原則及關聯的 PSTN 使用方式。表中只包括位置基礎路由的特有設定，做為說明之用。

    New-CsVoiceRoutingPolicy -Identity "DelhiVoiceRoutingPolicy" -Name "Delhi voice routing policy" -PstnUsages @{add="Delhi usage", "PBX Del usage", "PBX Hyd usage"}
    New-CsVoiceRoutingPolicy -Identity "HyderabadVoiceRoutingPolicy" -Name " Hyderabad voice routing policy" -PstnUsages @{add="Hyderabad usage", "PBX Del usage", "PBX Hyd usage"}


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>語音路由原則 1</th>
<th>語音路由原則 2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>語音原則識別碼</p></td>
<td><p>Delhi 語音路由原則</p></td>
<td><p>Hyderabad 語音路由原則</p></td>
</tr>
<tr class="even">
<td><p>PSTN 使用方式</p></td>
<td><p>Delhi 使用方式、PBX Del 使用方式、PBX Hyd 使用方式</p></td>
<td><p>Hyderabad 使用方式、PBX Hyd 使用方式、PBX Del 使用方式</p></td>
</tr>
</tbody>
</table>

  

接下來，為適用的網站設定位置基礎路由，並將您的語音路由原則與這些網站建立關聯。使用 Lync ServerWindows PowerShell 命令 New-CsNetworkSite 啟用位置基礎路由，並將語音路由原則與必須執行路由限制的網站建立關聯。

    Set-CsNetworkSite -Identity <site ID> -EnableLocationBasedRouting <$true|$false> -VoiceRoutingPolicy <voice routing policy ID>

就此範例而言，下表說明此案例中使用 Lync ServerWindows PowerShell 所定義之兩個不同網站 (Delhi 與 Hyderabad) 的位置基礎路由。表中只包括位置基礎路由的特有設定，做為說明之用。

    Set-CsNetworkSite -Identity "Delhi" -EnableLocationBasedRouting $true -VoiceRoutingPolicy "DelhiVoiceRoutingPolicy"
    Set-CsNetworkSite -Identity "Hyderabad" -EnableLocationBasedRouting $true -VoiceRoutingPolicy "HyderabadVoiceRoutingPolicy"


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>網站 1 (Delhi)</th>
<th>網站 2 (Hyderabad)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>網站名稱</p></td>
<td><p>網站 1 (Delhi)</p></td>
<td><p>網站 2 (Hyderabad)</p></td>
</tr>
<tr class="even">
<td><p>EnableLocationBasedRouting</p></td>
<td><p>True</p></td>
<td><p>True</p></td>
</tr>
<tr class="odd">
<td><p>語音路由原則</p></td>
<td><p>Delhi 語音路由原則</p></td>
<td><p>Hyderabad 語音路由原則</p></td>
</tr>
<tr class="even">
<td><p>子網路</p></td>
<td><p>子網路 1 (Delhi)</p></td>
<td><p>子網路 2 (Hyderabad)</p></td>
</tr>
</tbody>
</table>



## 對主幹啟用位置基礎路由

您需要先為每個主幹或每個網站建立主幹組態，才能為位置基礎路由啟用主幹組態。使用 Lync ServerWindows PowerShell 命令 New-CsTrunkConfiguration 建立主幹組態。如果有多個主幹已與指定系統 (亦即閘道或 PBX) 建立關聯，則必須修改每個主幹組態，才能啟用位置基礎路由限制。

    New-CsTrunkConfiguration -Identity < trunk configuration ID>

如需詳細資訊，請參閱＜[New-CsTrunkConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsTrunkConfiguration)＞。

就此範例而言，下列 Windows PowerShell 命令說明了如何為此案例中定義之部署的每個主幹建立主幹組態。

    New-CsTrunkConfiguration -Identity Service:PstnGateway:"<Trunk 1 DEL-GW>"
    New-CsTrunkConfiguration -Identity Service:PstnGateway:"<Trunk 2 HYD-GW>"
    New-CsTrunkConfiguration -Identity Service:PstnGateway:"<Trunk 3 DEL-PBX>"
    New-CsTrunkConfiguration -Identity Service:PstnGateway:"<Trunk 4 HYD-PBX>"

為每個主幹設定主幹組態後，您可以使用 Lync ServerWindows PowerShell 命令 Set-CsTrunkConfiguration 對必須執行路由限制的主幹啟用位置基礎路由。對將通話路由傳送到 (將通話路由傳送到 PSTN 之) PSTN 閘道的主幹啟用位置基礎路由，並與閘道所在的網站相關聯。

    Set-CsTrunkConfiguration -Identity <trunk configuration ID> -EnableLocationRestriction $true -NetworkSiteID <site ID>

如需詳細資訊，請參閱＜[New-CsTrunkConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsTrunkConfiguration)＞。

在此範例中，會為已與 Delhi 和 Hyderabad 之 PSTN 閘道建立關聯的每個主幹啟用位置基礎路由。

    Set-CsTrunkConfiguration -Identity Service:PstnGateway:Trunk 1 DEL-GW -EnableLocationRestriction $true -NetworkSiteID "Delhi"
    Set-CsTrunkConfiguration -Identity Service:PstnGateway:Trunk 2 HYD-GW -EnableLocationRestriction $true -NetworkSiteID "Hyderabad"

  

請勿為不會將通話路由傳送到 PSTN 的主幹啟用位置基礎路由；然而，您必須仍將主幹與系統所在之網站建立關聯，因為需要為連線到透過此主幹連接之端點的 PSTN 通話執行位置基礎路由限制。就此範例而言，並未為已與 Delhi 和 Hyderabad 之 PBX 系統建立關聯的每個主幹啟用位置基礎路由：

    Set-CsTrunkConfiguration -Identity Service:PstnGateway:Trunk 3 DEL-PBX -EnableLocationRestriction $false -NetworkSiteID "Delhi"
    Set-CsTrunkConfiguration -Identity Service:PstnGateway:Trunk 4 HYD-PBX -EnableLocationRestriction $false -NetworkSiteID "Hyderabad"

  
連接到不會將通話路由傳送到 PSTN (亦即 PBX) 之系統的端點，會和已啟用位置基礎路由的 Lync 使用者端點具有類似限制。也就是說，不論位於何處，這些使用者都將能夠撥打電話給 Lync 使用者以及接聽來自對方的電話。而不論與系統建立關聯的網站為何，這些使用者也將能夠撥打電話給其他不會將通話路由傳送到 PSTN 網路 (亦即連接到不同 PBX 的端點) 的系統，以及接聽來自對方的電話。所有涉及 PSTN 的撥入通話、撥出通話、通話轉接和來電轉接都將受到強制位置基礎路由限制。此類通話僅能使用已定義為此類系統本機之 PSTN 閘道。

下表說明兩個不同網站中四個主幹的主幹組態：兩個連接到 PSTN 閘道，另外兩個連接到 PBX 系統。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>名稱</th>
<th>EnableLocationRestriction</th>
<th>NetworkSiteID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PstnGateway：主幹 1 DEL-GW</p></td>
<td><p>True</p></td>
<td><p>網站 1 (Delhi)</p></td>
</tr>
<tr class="even">
<td><p>PstnGateway：主幹 2 HYD-GW</p></td>
<td><p>True</p></td>
<td><p>網站 2 (Hyderabad)</p></td>
</tr>
<tr class="odd">
<td><p>PstnGateway：主幹 3 DEL-PBX</p></td>
<td><p>False</p></td>
<td><p>網站 1 (Delhi)</p></td>
</tr>
<tr class="even">
<td><p>PstnGateway：主幹 4 HYD-PBX</p></td>
<td><p>False</p></td>
<td><p>網站 2 (Hyderabad)</p></td>
</tr>
</tbody>
</table>



## 對語音原則啟用位置基礎路由

若要對特定使用者執行位置基礎路由，請設定這些使用者的語音原則以禁止 PSTN 免話費機制。使用 Lync ServerWindows PowerShell 命令 New-CsVoicePolicy 建立新的語音原則，或以 Set-CsVoicePolicy (如果使用現有原則) 透過防止 PSTN 免話費機制啟用位置基礎路由。

    Set-CsVoicePolicy -Identity <voice policy ID> -PreventPSTNTollBypass <$true|$false>

如需詳細資訊，請參閱＜[New-CsVoicePolicy](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsVoicePolicy)＞。

就此範例而言，下表和 Windows PowerShell 命令說明如何對此案例中定義之 Delhi 和 Hyderabad 語音原則禁止 PSTN 免話費機制。表中只包括位置基礎路由的特有設定，做為說明之用。

    Set-CsVoicePolicy -Identity "Delhi voice policy" -PreventPSTNTollBypass $true
    Set-CsVoicePolicy -Identity "Hyderabad voice policy" -PreventPSTNTollBypass $true


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>語音原則 1</th>
<th>語音原則 2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>語音原則識別碼</p></td>
<td><p>Delhi 語音原則</p></td>
<td><p>Hyderabad 語音原則</p></td>
</tr>
<tr class="even">
<td><p>PSTN 使用方式</p></td>
<td><p>Delhi 使用方式、PBX Del 使用方式、PBX Hyd 使用方式</p></td>
<td><p>Hyderabad 使用方式、PBX Hyd 使用方式、PBX Del 使用方式</p></td>
</tr>
<tr class="odd">
<td><p>PreventPSTNTollBypass</p></td>
<td><p>True</p></td>
<td><p>True</p></td>
</tr>
</tbody>
</table>



## 在路由組態中啟用位置基礎路由

最後，對您的路由組態全域啟用位置基礎路由。使用 Lync ServerWindows PowerShell 命令 New-CsRoutingConfiguration 啟用位置基礎路由。

    Set-CsRoutingConfiguration -EnableLocationBasedRouting $true

如需詳細資訊，請參閱＜[Set-CsRoutingConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsRoutingConfiguration)＞。

> [!NOTE]  
> 雖然位置基礎路由必須透過全域組態啟用，要套用的整組規則將只會針對已按照本說明文件中指定內容設定的網站、使用者和主幹執行。




## 請參閱

#### 其他資源

[在 Lync Server 2013 中設定位置基礎路由](lync-server-2013-configuring-location-based-routing.md)

