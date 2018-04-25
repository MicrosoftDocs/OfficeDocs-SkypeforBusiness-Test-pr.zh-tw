---
title: Get-CsArchivingConfiguration
TOCTitle: Get-CsArchivingConfiguration
ms:assetid: e4951b81-2738-4cc2-87be-f8ee79da6c09
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399012(v=OCS.15)
ms:contentKeyID: 49292609
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsArchivingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織如何 (或是否要) 封存立即訊息 (IM) 工作階段的資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsArchivingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsArchivingConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回您組織中使用之所有封存組態設定的集合。

    Get-CsArchivingConfiguration

## 範例 2

在範例 2 中，Identity 參數是用來將傳回的封存組態設定集合限制於 Identity 為 site:Redmond 的那些設定。

    Get-CsArchivingConfiguration -Identity site:Redmond

## 範例 3

在範例 3 中，Filter 參數是用來將傳回的封存組態設定集合，限制為已在網站範圍進行設定的相關設定。參數值 "site:\*" 可將傳回的項目限制為 Identity 是以字串值 "site:" 開頭的項目。

    Get-CsArchivingConfiguration -Filter site:*

## 範例 4

此範例會使用 **Get-CsArchivingConfiguration** Cmdlet，以傳回已在組織中啟用之所有封存組態設定的集合。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsArchivingConfiguration** Cmdlet，以傳回所有封存組態設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet 套用篩選，以將傳回的資料限制在 EnableArchiving 屬性等於 "None" 的集合。若將 EnableArchiving 設為 "None"，將會停用封存。若將此屬性設為其他任意值 ("IMOnly" 或 "ImAndWebConf")，就表示已啟用該封存。

    Get-CsArchivingConfiguration | Where-Object {$_.EnableArchiving -ne "None"}

## 詳細描述

許多組織發現保留其使用者 (或所選取使用者的子集) 進行之所有 IM 工作階段的記錄非常有用。對於其他組織而言，保留這樣的記錄是必要的。例如，許多在金融界的組織依法規定須保留其所有的電子通訊副本。

就封存 IM 和網路會議工作階段而言，Lync Server 可讓您根據需求彈性地選擇。若您已部署了封存伺服器，便能使用各種 **CsArchivingConfiguration** Cmdlet 來啟用及停用立即訊息的封存功能，以及管理您的封存資料庫。而在封存失敗時，您也可以藉由暫停 IM 來確保所有電子通訊均能納入記錄。

為了封存 IM 工作階段，您必須至少設定一個封存伺服器。設定封存伺服器之後，您必須執行兩個額外的步驟。首先，需要在適當的範圍啟用封存 (如需詳細資訊，請參閱 **Set-CsArchivingConfiguration** Cmdlet 說明主題)。這可能是全域範圍；但是您也可以針對不同網站設定自訂封存設定。

其次，您必須使用封存原則，指出將要封存其 IM 工作階段的使用者。如果您啟用封存，但未針對任何使用者指派應封存其 IM 工作階段的原則時，會發生什麼事？其實，並不會發生任何事：不會封存 IM 工作階段，除非使用需要封存 IM 工作階段的原則。

利用 **Get-CsArchivingConfiguration** Cmdlet，您可決定如何在您組織中設定 IM 工作階段封存。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsArchivingConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsArchivingConfiguration"}

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
<td><p>可讓您使用萬用字元傳回一或多個封存組態設定的集合。若要傳回在網站範圍所設定之所有設定集合，請使用下列語法：-Filter site:*。如果要傳回在其 Identity (您可篩選的唯一屬性) 某處具有字串值 &quot;Canada&quot; 的所有設定集合，請使用下列語法：-Filter &quot;*Canada*&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>表示要傳回之封存設定集合的唯一識別碼。若要參考全域設定，請使用下列語法：-Identity global。若要在網站範圍內參照設定的集合，請使用如下語法：-Identity site:Redmond。若要傳回指派給個別登錄器集區之設定的資訊，請使用如下語法：</p>
<p>-Identity &quot;service:Registrar:atl-cs-001.litwareinc.com&quot;</p>
<p>集區層級的設定僅適用於 Lync Server 2013。</p>
<p>請注意，如有指定 Identity，即無法使用萬用字元。如果您必須使用萬用字元，請改為加入 Filter 參數。</p>
<p>如果未指定此參數，則 <strong>Get-CsArchivingConfiguration</strong> Cmdlet 會傳回組織使用之所有封存組態設定的集合。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區 的本機複本擷取封存組態資料，而非從 中央管理存放區 本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsArchivingConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsArchivingConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.Archiving.ArchivingSettings 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsArchivingConfiguration](new-csarchivingconfiguration.md)  
[Remove-CsArchivingConfiguration](remove-csarchivingconfiguration.md)  
[Set-CsArchivingConfiguration](set-csarchivingconfiguration.md)  
[Set-CsArchivingServer](set-csarchivingserver.md)

