---
title: Get-CsTrustedApplicationPool
TOCTitle: Get-CsTrustedApplicationPool
ms:assetid: f8dc4ad7-fc32-482b-a1cb-5ba106df3344
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413055(v=OCS.15)
ms:contentKeyID: 49292867
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTrustedApplicationPool

 

_**上次修改主題的時間：** 2015-03-09_

擷取一或多個集區的設定；這些集區中包含代管信任之應用程式的電腦。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsTrustedApplicationPool [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsTrustedApplicationPool [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-PoolFqdn <String>]

## 範例

## 範例 1

範例 1 會擷取 Lync Server 部署內已定義為受信任應用程式集區的所有集區。

    Get-CsTrustedApplicationPool

## 範例 2

在此範例中，我們使用 Identity 參數來確定只會擷取一個受信任應用程式集區，在此範例中是 FQDN 為 TrustPool.litwareinc.com 的集區。

    Get-CsTrustedApplicationPool -Identity TrustPool.litwareinc.com

## 範例 3

此範例會擷取集區 FQDN 中包含網站 TrustPool 的所有受信任應用程式集區。Filter 參數可與 \*:TrustPool.\* 的值搭配使用。此篩選字串會針對包含字串 “:TrustPool.” 的 Identity 值，搜尋所有受信任應用程式集區的 Identity 值。例如，此命令會擷取 Identity 值為 TrustedApplicationPool:TrustPool.litwareinc.com 的集區。

    Get-CsTrustedApplicationPool -Filter *:TrustPool.*

## 範例 4

Filter 參數只會搜尋 Identity，但前提是受信任應用程式集區是服務 ID，格式為 TrustedApplicationPool:\<FQDN\>。此範例會根據服務 ID 以 \<site\>-ExternalServer-\<id\> 格式搜尋集區，例如 Redmond1-ExternalServer-1。如此一來我們可以尋找隸屬於特定網站上的受信任集區。此範例會先不使用任何參數而呼叫不含任何參數的 **Get-CsTrustedApplicationPool** Cmdlet，以擷取所有受信任應用程式集區的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，以將集合範圍限制在 service ID ($\_.ServiceId) 符合萬用字元字串 (-like) Redmond1\* 的集區。這會產生所有 FQDN 開頭為字串 Redmond1 之受信任應用程式集區的集合，例如 Redmond1-ExternalServer-1、Redmond1-ExternalServer-2 及 Redmond1-ExternalServer-3。

    Get-CsTrustedApplicationPool | Where-Object {$_.ServiceId -like "Redmond1*"}

## 詳細描述

建議您應該將 Lync Server 部署內執行信任的應用程式的電腦，新增至信任的應用程式專用的集區。不過，您也可以將信任的應用程式電腦新增至用於其他用途的現有集區。此 Cmdlet 會擷取已定義為受信任應用程式集區的一或多個集區。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsTrustedApplicationPool** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。執行 Windows PowerShell 提示字元提供的下列命令，即可傳回指派給此 Cmdlet (包括您自行建立的任何自訂 RBAC 角色) 的所有角色型存取控制 (RBAC) 角色清單：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsTrustedApplicationPool"}

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
<td><p>包含可用來搜尋 Identity (服務識別碼) 符合該萬用字元字串之集區的一或多個萬用字元的字串。例如，指定字串 *Redmond* 會擷取識別身分包含字串 Redmond 的所有受信任應用程式集區，例如 TrustedApplicationPool:Redmond.litwareinc.com。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>您要擷取其設定之集區的完整網域名稱 (FQDN) 或服務識別碼。</p></td>
</tr>
<tr class="odd">
<td><p><em>PoolFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>您要擷取之集區的 FQDN。此運作方式與 Identity 參數相同，唯一差異在於該 Identity 也接受服務 ID。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

擷取 Microsoft.Rtc.Management.Xds.DisplayExternalServer 類型的一個或多個物件。

## 請參閱

#### 其他資源

[New-CsTrustedApplicationPool](new-cstrustedapplicationpool.md)  
[Remove-CsTrustedApplicationPool](remove-cstrustedapplicationpool.md)  
[Set-CsTrustedApplicationPool](set-cstrustedapplicationpool.md)

