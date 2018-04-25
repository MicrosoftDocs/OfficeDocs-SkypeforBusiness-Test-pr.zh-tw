---
title: Get-CsSite
TOCTitle: Get-CsSite
ms:assetid: 0e5fd5b8-17aa-433d-9915-3b88281fa2c2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398185(v=OCS.15)
ms:contentKeyID: 49290092
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsSite

 

_**上次修改主題的時間：** 2015-03-09_

傳回在 Lync Server 基礎結構中所建立之網站的資訊。網站代表 Lync Server 集區的集合，通常會根據地理區域設計。Lync Server 包括兩種網站類型：資料中心網站和遠端網站 (分支網站)。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsSite [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsSite [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS:

## 範例

## 範例 1

範例 1 會擷取所有 Lync Server 網站的資訊。

    Get-CsSite

## 範例 2

範例 2 會傳回單一網站 (即 Identity 為 Redmond 的網站) 的資訊。

    Get-CsSite -Identity "Redmond"

## 範例 3

範例 3 所示的命令會傳回您中央網站的資訊。為了執行此工作，命令會先呼叫 **Get-CsSite** Cmdlet 以傳回設定供組織使用之所有網站的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，以挑出 SiteType 屬性等於 "CentralSite" 的網站。

    Get-CsSite | Where-Object {$_.SiteType -eq "CentralSite"}

## 範例 4

範例 4 會顯示在 Redmond 網站中找到之集區的清單。為達成此目的，命令會先擷取 Redmond 網站的完整資訊，接著將該資料管線傳送到 **Select-Object** Cmdlet。然後，**Select-Object** Cmdlet 會使用 ExpandProperty 參數來「展開」Pools 屬性的值。展開屬性值表示在畫面上以易於閱讀的格式，顯示該屬性中儲存的所有值。

    Get-CsSite -Identity "Redmond" | Select-Object -ExpandProperty Pools

## 詳細描述

Lync Server 2010 引進 Lync Server 拓撲的新概念：網站。網站 (請勿與 Active Directory 網站或 Microsoft Exchange Server 網站混淆) 是指通常根據地理和網路頻寬來組織的 Lync Server 集區和伺服器的集合。例如，如果您在 Redmond 的所有電腦均位於具備高速、低延遲連線的相同區域網路上，則可能會指定包含這些電腦的 Redmond 網站。如果您在 Dublin 的電腦位於自己的區域網路中，並共用高速、低延遲的連線，則您也可以建立一個獨立的 Dublin 網站。網站在 Lync Server 管理中扮演了一個關鍵角色：大多數的原則和設定都可在網站範圍設定，以方便進行像是將一組撥號對應表套用至位於 Redmond 的使用者，並將完全不同的另一組撥號對應表套用至位於 Dublin 之使用者的作業。

**Get-CsSite** Cmdlet 可讓您傳回關於組織中所有網站的資訊，包括關於組成這些每個網站之集區的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsSite** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsSite"}

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
<td><p>可讓您在指定要傳回的網站 Identity 時使用萬用字元。例如，此語法會傳回 Identity 包含字串值 &quot;Dublin&quot; 的所有集區：-Filter &quot;*Dublin*&quot;。</p>
<p>請注意，您無法在同一個命令中使用 Filter 和 Identity。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要傳回之網站的名稱。請注意，您應該只指定網站名稱；例如：-Identity &quot;Redmond&quot;。在指定 Identity 時，請勿使用 &quot;site:Redmond&quot; 的格式。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsSite** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsSite** Cmdlet 會傳回 Microsoft.Rtc.Management.Deploy.Internal.Site+CentralSite 物件的執行個體。

## 請參閱

#### 其他資源

[Set-CsSite](set-cssite.md)

