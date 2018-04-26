---
title: Get-CsMediaConfiguration
TOCTitle: Get-CsMediaConfiguration
ms:assetid: 071c1733-07c3-4075-8745-367634e37941
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398128(v=OCS.15)
ms:contentKeyID: 49289983
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsMediaConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回有關於媒體設定的資訊，包括支援的加密層級，中繼伺服器與 Lync Server 用戶端互動時是否可以使用 Siren 做為語音轉碼器，以及允許最高視訊解析度。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsMediaConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsMediaConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 只需叫用不含任何參數的 **Get-CsMediaConfiguration** Cmdlet，即可傳回組織中使用的所有媒體組態。

    Get-CsMediaConfiguration

## 範例 2

範例 2 只會傳回 Identity 為 site:Redmond1 的媒體組態。因為識別必須是唯一的，所以指定 Identity 可確保您不會擷取一個以上的項目。

    Get-CsMediaConfiguration -Identity site:Redmond1

## 範例 3

在範例 3 中，Filter 參數可用來傳回在網站範圍的所有媒體組態。萬用字元字串 site:\* 可確保 Windows PowerShell 只傳回識別身分開頭為字串值 site: 的媒體組態。

    Get-CsMediaConfiguration -Filter site:*

## 範例 4

在此範例中，**Get-CsMediaConfiguration** Cmdlet 和 **Where-Object** Cmdlet 用來傳回支援 (但不需要) 加密的所有媒體組態。作法為命令先使用 **Get-CsMediaConfiguration** Cmdlet 來擷取組織中使用的所有媒體組態。然後再將此資訊管線傳送到 **Where-Object** Cmdlet，以套用篩選，將傳回的資料限於 EncryptionLevel 屬性等於 (-eq) SupportEncryption 的組態。

    Get-CsMediaConfiguration | Where-Object {$_.EncryptionLevel -eq "SupportEncryption"}

## 範例 5

此範例會擷取名稱含有 "med" 字串的網站和服務已定義的所有媒體組態。例如，此命令會擷取針對網站 medford1、網站 TwoMedfordPlace 以及服務 MediationServer:redmond.litwareinc.com 定義的媒體組態設定。

    Get-CsMediaConfiguration -Filter *:*med*

## 詳細描述

此 Cmdlet 會擷取一或多個定義媒體互動之設定的集合。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsMediaConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsMediaConfiguration"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>您要擷取之媒體組態的唯一識別碼。此識別碼會指定套用此組態的範圍 (全域、網站或服務)。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取媒體組態資訊，而非從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

**Get-CsMediaConfiguration** Cmdlet 傳回 Microsoft.Rtc.Management.WritableConfig.Settings.Media.MediaSettings 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsMediaConfiguration](new-csmediaconfiguration.md)  
[Remove-CsMediaConfiguration](remove-csmediaconfiguration.md)  
[Set-CsMediaConfiguration](set-csmediaconfiguration.md)

