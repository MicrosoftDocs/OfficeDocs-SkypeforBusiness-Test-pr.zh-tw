---
title: Set-CsFIPSConfiguration
TOCTitle: Set-CsFIPSConfiguration
ms:assetid: 920f58ce-e175-41ac-b681-5ac873091593
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205084(v=OCS.15)
ms:contentKeyID: 49291678
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsFIPSConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改現有美國聯邦資訊處理標準 (FIPS) 組態設定資訊的集合。FIPS 標準美國政府所設定的安全性標準，所有由非軍方之政府機構與政府合約商維護的電腦中，都必須使用這套標準。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Set-CsFIPSConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsFIPSConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-RequireFIPSCompliantMedia <$true | $false>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

在範例 1 中，全域 FIPS 組態設定的 RequireFIPSCompliantMedia 屬性設為 True ($True)。

    Set-CsFIPSConfiguration -Identity "global" -RequireFIPSCompliantMedia $True

## 詳細描述

美國聯邦資訊處理標準 (FIPS) 是一系列的標準與準則，所有涉及美國政府工作的電腦，都必須加以遵循。例如管理密碼編譯、加密、數位簽章的 FIPS 標準 (如需詳細資訊，請參閱 <http://www.itl.nist.gov/fipspubs/by-num.htm>)。Lync Server 2013 可讓您選擇將軟體設成只使用符合 FIPS 標準的演算法。您如有參與美國政府 (或其他必須遵循 FIPS 的機構) 的工作，您可以啟用 Lync Server 2013 中的 FIPS 規範。

請注意，內部部署版的 Lync Server 只可有一個通用的 FIPS 組態設定集合，亦即您只可針對整個 Lync Server 實作啟用或停用 FIPS 規範，而無法只為像個別網站或個別的登錄器集區啟用或停用 FIPS 規範。啟用 FIPS 規範之後，有可能會在和未完全遵循 FIPS 標準的組織通訊時發生問題。

預設會停用 Lync Server 2013的 FIPS 規範。

**Set-CsFIPSConfiguration** Cmdlet 可用於啟用或停用 FIPS 規範。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsFIPSConfiguration"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Set-CsFIPSConfiguration** Cmdlet 所執行的功能。

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
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的任何非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>所要修改之 FIPS 組態設定的唯一識別碼。因為 Lync Server 2013僅支援 FIPS 設定的單一、全域集合，所以唯一可以修改的集合就是全域集合：</p>
<p>-Identity global</p>
<p>若未包含此參數，<strong>Set-CsFIPSConfiguration</strong> Cmdlet 將會修改全域集合。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>允許您將物件參照傳遞給 Cmdlet，而非設定個別參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>RequireFIPSCompliantMedia</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 True 時，Lync Server 2013只允許具有使用 FIPS 相容演算法供驗證及授權之實體的媒體工作階段。</p>
<p>請注意，若您需要 FIPS 規範，使用者將無法再使用 Microsoft Lync Server 2010 A/V Edge Server 來連接系統。您必須將所有 Edge Server 升級至 Lync 2013 才行。</p>
<p>預設值為 False。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要修改 FIPS 組態設定之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行此命令來傳回每位租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>描述執行命令後的結果，但無須實際執行命令。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

**Set-CsFIPSConfiguration** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Settings.FIPSConfiguration.FIPSConfiguration 物件執行個體。

## 傳回類型

無。反之，**Set-CsFIPSConfiguration** Cmdlet 會修改現有的 Microsoft.Rtc.Management.WritableConfig.Settings.FIPSConfiguration.FIPSConfiguration 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsFIPSConfiguration](get-csfipsconfiguration.md)  
[New-CsFIPSConfiguration](new-csfipsconfiguration.md)  
[Remove-CsFIPSConfiguration](remove-csfipsconfiguration.md)

