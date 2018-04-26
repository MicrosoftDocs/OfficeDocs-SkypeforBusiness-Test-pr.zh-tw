---
title: Get-CsTrustedApplicationComputer
TOCTitle: Get-CsTrustedApplicationComputer
ms:assetid: 360796d8-48c7-4ce2-9bb4-1f8967562f24
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425843(v=OCS.15)
ms:contentKeyID: 49290566
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTrustedApplicationComputer

 

_**上次修改主題的時間：** 2015-03-09_

擷取一或多部代管信任之應用程式的電腦的資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsTrustedApplicationComputer [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsTrustedApplicationComputer [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Local <SwitchParameter>] [-Pool <String>]

## 範例

## 範例 1

範例 1 會擷取已指派給 Lync Server 部署內任何一個信任的應用程式集區之所有電腦。

    Get-CsTrustedApplicationComputer

## 範例 2

範例 2 擷取 FQDN 為 Trust1.litwareinc.com 的電腦相關資訊。

    Get-CsTrustedApplicationComputer -Identity Trust1.litwareinc.com

## 範例 3

本範例使用 Filter 參數進行萬用字元搜尋，搜尋 FQDN 開頭為 Trust 字串且已指派給信任的應用程式集區的所有電腦。Filter 參數會搜尋所有信任的應用程式電腦的 Identity 屬性。字串結尾的萬用字元 (\*) 表示 Filter 應尋找開頭為 Trust 字串，字串後再加上任何其他字元的識別。

    Get-CsTrustedApplicationComputer -Filter Trust*

## 範例 4

範例 4 擷取已指派給信任的應用程式集區 TrustPool.litwareinc.com 的所有電腦清單。

    Get-CsTrustedApplicationComputer -Pool TrustPool.litwareinc.com

## 範例 5

在範例 3 中，我們使用 Filter 參數來根據 Identity (電腦的 FQDN) 進行萬用字元搜尋。在本範例中，我們會再次進行萬用字元搜尋，但這次我們在集區 (而非識別碼) 上搜尋。我們會先呼叫 **Get-CsTrustedApplicationComputer** Cmdlet 來擷取所有信任的應用程式電腦的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet。**Where-Object** Cmdlet 可讓我們縮小已管線傳送給它的集合範圍。在此範例中，我們只要保留在 litwareinc.com 網域中任何一個集區內的信任的應用程式電腦。為達成此目的，我們會檢查集合 ($\_.Pool) 中每個項目的 Pool 屬性，確認其是否符合 (-like) 萬用字元字串 \*.litwareinc.com。如果值的開頭是任何一組結尾是 .litwareinc.com 字串的字元，便符合萬用字元字串。

    Get-CsTrustedApplicationComputer | Where-Object {$_.Pool -like "*.litwareinc.com"}

## 詳細描述

建議您應該將 Lync Server 部署內執行信任的應用程式之電腦，新增至信任的應用程式專用的集區。不過，您也可以將信任的應用程式電腦新增至用於其他用途的現有集區。使用此 Cmdlet 可擷取 Identity (FQDN)，以及一或多部包含信任的應用程式之電腦所在的集區。

您可以使用此 Cmdlet 根據電腦 FQDN 擷取電腦，或擷取指定集區一部分的所有電腦。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsTrustedApplicationComputer** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsTrustedApplicationComputer"}

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
<td><p>包含萬用字元的字串，可讓您根據符合指定萬用字元字串的 Identity 值來擷取信任的電腦。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>您要擷取之電腦的完整網域名稱 (FQDN)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Local</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定此參數，只會傳回本機電腦的資訊。</p></td>
</tr>
<tr class="even">
<td><p><em>Pool</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要擷取電腦資訊之信任的應用程式集區的 FQDN。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

擷取 Microsoft.Rtc.Management.Xds.DisplayComputer 類型的一或多個物件。

## 請參閱

#### 其他資源

[New-CsTrustedApplicationComputer](new-cstrustedapplicationcomputer.md)  
[Remove-CsTrustedApplicationComputer](remove-cstrustedapplicationcomputer.md)

