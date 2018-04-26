---
title: Get-CsOutboundTranslationRule
TOCTitle: Get-CsOutboundTranslationRule
ms:assetid: 0564df17-dcca-44e1-9341-15521e0fa14b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398104(v=OCS.15)
ms:contentKeyID: 49289955
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsOutboundTranslationRule

 

_**上次修改主題的時間：** 2015-03-09_

擷取一或多項外撥轉譯規則。外撥轉譯規則會將電話號碼轉換為區域撥號格式，以與專用交換機 (PBX) 系統和公用交換電話網路 (PSTN) 閘道互動。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsOutboundTranslationRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsOutboundTranslationRule [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

此範例會擷取 Lync Server 部署的所有外撥轉譯規則。

    Get-CsOutboundTranslationRule

## 範例 2

此範例會擷取單一外撥轉譯規則，也就是 Identity site:Redmond/Prefix Redmond 的規則。

    Get-CsOutboundTranslationRule -Identity "site:Redmond/Prefix Redmond"

## 範例 3

此範例會擷取所有網站層級的外撥轉譯規則。命令會呼叫 **Get-CsOutboundTranslationRule** Cmdlet 並搭配 site:\* 的 Filter，這會傳回 Identity 值以字串 site: 為開頭的所有規則集合。

    Get-CsOutboundTranslationRule -Filter site:*

## 詳細描述

呼叫此 Cmdlet 以擷取現有的外撥轉譯規則。Lync Server 會將電話號碼正規化成 E.164 格式。但是，有許多專用交換機 (PBX) 系統無法使用這個格式。將號碼傳送到 中繼伺服器 或閘道之前，外撥轉譯規則會將號碼轉譯為區域撥號格式。

每個外撥轉譯規則會與主幹組態相關聯。每個主幹組態都可以與多個外撥轉譯規則相關聯。因此，每個規則識別是由一個範圍以及在此範圍內之唯一名稱 (格式為「範圍/名稱」，例如 site:Redmond/OBR1) 所組成。規則會自動與同一個範圍的主幹組態產生關聯。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsOutboundTranslationRule** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsOutboundTranslationRule"}

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
<td><p>執行萬用字元搜尋，它允許您將結果縮減為只有識別符合指定萬用字元字串的外撥轉譯規則。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>您要擷取之外撥轉譯規則的唯一識別碼。Identity 是由範圍後面加上在每個範圍內的唯一名稱所組成 (例如 site:Redmond/OutboundRule1)。指定 Identity 的值會傳回最多一個外撥轉譯規則。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區 的本機複本擷取外撥轉譯規則，而非從 中央管理存放區 本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

此 Cmdlet 會擷取 Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TranslationRule 類型的一或多個物件。

## 請參閱

#### 其他資源

[New-CsOutboundTranslationRule](new-csoutboundtranslationrule.md)  
[Remove-CsOutboundTranslationRule](remove-csoutboundtranslationrule.md)  
[Set-CsOutboundTranslationRule](set-csoutboundtranslationrule.md)

