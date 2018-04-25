---
title: Get-CsVoiceNormalizationRule
TOCTitle: Get-CsVoiceNormalizationRule
ms:assetid: 59fe1370-1cec-4cf9-8f65-029a7c2454d1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398393(v=OCS.15)
ms:contentKeyID: 49291016
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsVoiceNormalizationRule

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織所使用之語音正規化規則的資訊。語音正規化規則可將電話撥號需求 (例如撥打外線前先撥 9) 轉換為 Lync Server 所使用的 E.164 電話號碼格式。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsVoiceNormalizationRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsVoiceNormalizationRule [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

此範例會擷取組織已定義的所有語音正規化規則。

    Get-CsVoiceNormalizationRule

## 範例 2

範例 2 會擷取所有網站已指定的所有語音正規化規則。

    Get-CsVoiceNormalizationRule -Filter site*

## 範例 3

範例 3 會擷取範圍中任何出現字母 s 之處的所有語音正規化規則。例如，這樣會傳回範圍名稱中出現 s (例如 RedmondEastUsers) 的所有網站層級、服務層級以及個別使用者的規則。

    Get-CsVoiceNormalizationRule -Filter *s*

## 範例 4

範例 2 和 3 中使用的 Filter 參數只比對 Identity 的範圍部分。此範例會在名稱部分執行比對，以傳回名稱中含有 "seattle" 字串的所有規則。為達成此目的，會先呼叫 **Get-CsVoiceNormalizationRule** Cmdlet 擷取組織的所有正規化規則。然後，此集合會管線傳送到 **Where-Object** Cmdlet，以尋找集合中所有 Name 屬性符合 "seattle" 字串的項目。

    Get-CsVoiceNormalizationRule | Where-Object {$_.Name -match "seattle"}

## 詳細描述

此 Cmdlet 會傳回具名的語音正規化規則或語音正規化規則的集合。這些規則是電話授權和電話路由的必要部分。它們定義將號碼從內部 Lync Server 格式轉換 (或轉譯) 為標準 (E.164) 格式的需求。了解規則運算式對於定義將要轉譯的號碼模式很有幫助。

此 Cmdlet 所存取的相同規則，也可以透過呼叫 **Get-CsDialPlan** Cmdlet 所傳回的 NormalizationRules 屬性來存取。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsVoiceNormalizationRule** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsVoiceNormalizationRule"}

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
<td><p>使用萬用字串，以根據 Identity 傳回正規化規則的集合。請注意，Filter 僅適用於 Identity 的範圍部分，不適用於名稱部分。例如，篩選值 *lob* 會傳回全域範圍 (含字母 lob 的範圍) 的所有規則，而不是 Identity 為 site:Redmond/lobby 的規則，其中 lob 只會位於 Identity 的名稱部分，而不會在範圍部分。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>規則的唯一識別碼。如果指定此參數的值，它必須是「範圍/名稱」格式；例如，site:Redmond/Rule1，其中 site:Redmond是範圍，Rule1 是名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區 的本機複本擷取語音正規化規則，而非從 中央管理存放區 本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

**Get-CsVoiceNormalizationRule** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.NormalizationRule 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsVoiceNormalizationRule](new-csvoicenormalizationrule.md)  
[Remove-CsVoiceNormalizationRule](remove-csvoicenormalizationrule.md)  
[Set-CsVoiceNormalizationRule](set-csvoicenormalizationrule.md)  
[Test-CsVoiceNormalizationRule](test-csvoicenormalizationrule.md)  
[Get-CsDialPlan](get-csdialplan.md)

