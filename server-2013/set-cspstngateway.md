---
title: Set-CsPstnGateway
TOCTitle: Set-CsPstnGateway
ms:assetid: 5d61e7e5-dacb-4dd3-bdd5-b757d98181d3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398408(v=OCS.15)
ms:contentKeyID: 49291053
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPstnGateway

 

_**上次修改主題的時間：** 2015-03-09_

修改公用交換電話網路 (PSTN) 閘道的屬性。PSTN 閘道可路由外部 PSTN 網路上之裝置與內部 Enterprise Voice 網路上之裝置間的通話。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsPstnGateway [-Identity <XdsGlobalRelativeIdentity>] [-AlternateByPassId <String>] [-Confirm [<SwitchParameter>]] [-Default <$true | $false>] [-Force <SwitchParameter>] [-GatewaySipClientTcpPort <UInt16>] [-GatewaySipClientTlsPort <UInt16>] [-MediationServer <String>] [-RepresentativeMediaIP <String>] [-Routable <$true | $false>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將閘道 PstnGateway:192.168.0.240 設定為預設閘道。也就是說，PstnGateway:192.168.0.240 可用來處理來自 Office Communications Server 2007 R2 的通話。

    Set-CsPstnGateway -Identity "PstnGateway:192.168.0.240" -Default $True

## 範例 2

範例 2 會設定組織中的所有 PSTN 閘道，讓每一個閘道都可以在輸出路由中使用。為達成此目的，命令會先使用 **Get-CsService** Cmdlet 和 PstnGateway 參數，以傳回目前所使用之所有 PSTN 閘道的集合。然後，此集合會管線傳送到 **ForEach-Object** Cmdlet。**ForEach-Object** Cmdlet 會對集合中的每個閘道執行 **Set-CsPstnGateway** Cmdlet，以將每個閘道的 Routable 屬性設為 True。

    Get-CsService -PstnGateway | ForEach-Object {Set-CsPstnGateway -Identity $_.Identity -Routable $True}

## 詳細描述

PSTN 閘道可讓您的 Enterprise Voice 使用者撥打電話給 PSTN 網路上的人員，以及接收 PSTN 網路上人員的電話。這些閘道充當中繼伺服器與 PSTN 網路之間的橋接器。

當您使用分時多工公用交換機 (PBX) 電話系統時，通常需要 PSTN 閘道；在此情況下，您通常需要採用 PSTN 閘道和中繼伺服器，才能將 Enterprise Voice 來電路由傳送到 PSTN 網路。相反地，如果使用 IP-PBX 系統，則可以在 PBX 與中繼伺服器之間建立直接 SIP 連線，而不必使用 PSTN 閘道。

在安裝及設定 PSTN 閘道之後，可以使用 **Set-CsPstnGateway** Cmdlet 進行管理。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsPstnGateway** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPstnGateway"}

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
<td><p><em>AlternateByPassId</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>代表替代旁路識別碼的全域唯一識別碼 (GUID)。這個 ID 由 Lync Server 自動產生，並有助於減少髮夾呼叫。視您設定系統的方式而定，這可讓髮夾呼叫自動略過中繼伺服器，不需要您定義並將個別子網路與所有網站和區域建立關聯。</p>
<p>為達此目的，您通常需要全域啟用旁路以使用網路組態網站與區域，然後針對 PSTN 閘道在主幹組態上啟用旁路。</p>
<p>當來自 PSTN 網路的傳入呼叫藉由來電轉接或同時電話響鈴而路由回到該網路時，就會發生髮夾呼叫。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Default</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果設為 True，此閘道會處理從 Office Communications Server 2007 R2 傳來的通話。由單一中繼伺服器管理的閘道集合中，只能有一個預設閘道。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏當執行 Cmdlet 時可能發生的任何確認提示或非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>GatewaySipClientTcpPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>使用傳輸控制通訊協定 (TCP) 與中繼伺服器進行通訊時所使用的聆聽連接埠。預設值為 5066。</p></td>
</tr>
<tr class="even">
<td><p><em>GatewaySipClientTlsPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>使用傳輸層安全性 (TLS) 通訊協定與中繼伺服器進行通訊時所使用的聆聽連接埠。預設值為 5067。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要修改之 PSTN 閘道的服務識別。例如：-Identity &quot;PstnGateway:192.168.0.240&quot;。</p>
<p>請注意，指定 PSTN 閘道時，您可以省略首碼 &quot;PstnGatewayServer:&quot;。例如：-Identity &quot;atl-cs-001.litwareinc.com&quot;。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>MediationServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要與 PSTN 閘道相關聯之中繼伺服器的服務識別。例如：-MediationServer &quot;MediationServer:atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>RepresentativeMediaIP</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>如果處理器位置與發出訊號的位址不同，則為與閘道相關聯的媒體處理器 IP 位址。媒體旁路與通話許可控制 (CAC) 都以閘道的媒體處理器位置為依據；根據預設，這個位置與發出訊號的位址相同。如果這兩個位置不同 (例如，媒體處理器在遠端網站，而發出訊號的對等端在中央網站)，則必須使用媒體處理器的 IP 位址來設定 RepresentativeMediaIP。</p>
<p>如果您在相同網站上部署多個媒體處理器，每個各有自己的 IP 位址，則在設定 RepresentativeMediaIP 內容時，可以使用其中任何一個 IP 位址。</p></td>
</tr>
<tr class="even">
<td><p><em>Routable</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果設為 True，閘道可在輸出路由中使用。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsPstnGateway** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Set-CsPstnGateway** Cmdlet 不會傳回任何物件或值，而會修改現有的 Microsoft.Rtc.Management.Xds.DisplayPstnGateway 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsService](get-csservice.md)

