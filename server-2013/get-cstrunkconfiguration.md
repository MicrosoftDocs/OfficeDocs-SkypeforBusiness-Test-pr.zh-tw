---
title: Get-CsTrunkConfiguration
TOCTitle: Get-CsTrunkConfiguration
ms:assetid: 15951113-5f96-4f44-8cad-9ff97fb5dfd6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398224(v=OCS.15)
ms:contentKeyID: 49290188
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTrunkConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

擷取一或多個描述對等主幹實體之設定 (例如服務提供者的公用交換電話網路 (PSTN) 閘道、IP 專用交換機 (PBX) 或工作階段邊界控制器 (SBC)) 的主幹組態。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsTrunkConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsTrunkConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

此範例會擷取 Lync Server 部署的所有主幹組態。

    Get-CsTrunkConfiguration

## 範例 2

此範例會擷取 Identity site:Redmond 的主幹組態。因為識別是唯一的，所以此命令最多只會傳回一個物件。

    Get-CsTrunkConfiguration -Identity site:Redmond

## 範例 3

範例 3 會擷取在網站層級定義的所有主幹組態。**Get-CsTrunkConfiguration** Cmdlet 會使用 Filter 參數擷取 Identity 開頭為 site: (表示在網站層級定義的所有主幹組態) 的所有主幹組態。

    Get-CsTrunkConfiguration -Filter site:*

## 詳細描述

使用此 Cmdlet 可擷取適用於 PSTN 閘道實體的一或多個主幹組態。每個組態均含有對等主幹實體 (例如，服務提供者的 PSTN 閘道、IP-PBX 或 SBC) 的專屬設定。這些設定所設定的項目包括此主幹是否啟用媒體旁路、是否在特定情況下傳送即時傳輸控制通訊協定 (RTCP) 封包，以及是否需要安全即時通訊協定 (SRTP) 加密。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsTrunkConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsTrunkConfiguration"}

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
<td><p>此參數接受萬用字元字串，並傳回識別符合該字串的所有主幹組態。例如，Filter 值為 site:* 會傳回網站層級上定義的所有主幹組態。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>您要擷取之主幹組態的唯一識別碼。主幹組態可在全域範圍、網站範圍或 PSTN 閘道服務的服務範圍上加以定義。例如，site:Redmond (網站) 或 PstnGateway:Redmond.litwareinc.com (服務)。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區本機複本擷取主幹組態，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

此 Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration 類型的物件。

## 請參閱

#### 其他資源

[New-CsTrunkConfiguration](new-cstrunkconfiguration.md)  
[Remove-CsTrunkConfiguration](remove-cstrunkconfiguration.md)  
[Set-CsTrunkConfiguration](set-cstrunkconfiguration.md)  
[Test-CsTrunkConfiguration](test-cstrunkconfiguration.md)

