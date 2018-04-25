---
title: Get-CsFIPSConfiguration
TOCTitle: Get-CsFIPSConfiguration
ms:assetid: 56d29011-187f-4034-a5ed-71625087bf36
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204904(v=OCS.15)
ms:contentKeyID: 49290971
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsFIPSConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織目前所使用之美國聯邦資訊處理標準 (FIPS) 組態設定的資訊。FIPS 標準美國政府所設定的安全性標準，所有由非軍方之政府機構與政府合約商維護的電腦中，都必須使用這套標準。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsFIPSConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsFIPSConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>] [-Tenant <Guid>]

## 範例

## 範例 1

範例 1 所示的命令會傳回組織目前所使用之所有 FIPS 組態設定的資訊。請注意，只有單一、全域的 FIPS 組態設定執行個體。

    Get-CsFIPSConfiguration

## 詳細描述

美國聯邦資訊處理標準 (FIPS) 是一系列的標準與準則，所有涉及美國政府工作的電腦，都必須加以遵循。例如管理密碼編譯、加密、數位簽章的 FIPS 標準 (如需詳細資訊，請參閱 <http://www.itl.nist.gov/fipspubs/by-num.htm>)。Lync Server 2013 可讓您選擇將軟體設成只使用符合 FIPS 標準的演算法。您如有參與美國政府 (或其他必須遵循 FIPS 的機構) 的工作，您可以啟用 Lync Server 2013 中的 FIPS 規範。

請注意，內部部署版的 Lync Server 只可有一個全域的 FIPS 組態設定集合，亦即您只可針對整個 Lync Server 實作啟用或停用 FIPS 規範，而無法只為個別網站或個別的登錄器集區啟用或停用 FIPS 規範。啟用 FIPS 規範之後，有可能會在和未遵循 FIPS 標準的組織通訊時發生問題。

預設會停用 Lync Server 2013的 FIPS 規範。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsFIPSConfiguration"}

**Lync Server 控制台：**Lync Server 控制台不提供 Get-CsFIPSConfiguration Cmdlet 所執行的功能。

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
<td><p>可讓您在參照 FIPS 組態設定集合時，使用萬用字元值。因為您只能有這些設定的單一、全域執行個體，所以沒有理由使用 Filter 參數。不過，如果您想要，可以使用下列語法來參照全域設定：</p>
<p>-Filter &quot;g*&quot;</p>
<p>該語法會傳回 Identity 以字母 &quot;g&quot; 為開頭的所有 FIPS 組態設定。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>FIPS 組態設定的唯一 Identity。因為您只能有這些設定的單一、全域執行個體，所以在呼叫 <strong>Get-CsFIPSConfiguration</strong> Cmdlet 時，不需要指定 Identity。但是，您可以視需要使用下列語法來參照全域設定：</p>
<p>-Identity global</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取 FIPS 組態資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要擷取其 FIPS 組態設定之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。</p>
<p>例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行此命令來傳回每位租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsFIPSConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsFIPSConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.FIPSConfiguration.FIPSConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsFIPSConfiguration](new-csfipsconfiguration.md)  
[Remove-CsFIPSConfiguration](remove-csfipsconfiguration.md)  
[Set-CsFIPSConfiguration](set-csfipsconfiguration.md)

