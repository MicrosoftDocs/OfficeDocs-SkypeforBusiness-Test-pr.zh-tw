---
title: Remove-CsFIPSConfiguration
TOCTitle: Remove-CsFIPSConfiguration
ms:assetid: b7e43419-0154-4fed-bfc6-9053335ce5d8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205201(v=OCS.15)
ms:contentKeyID: 49292107
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsFIPSConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除一或多個美國聯邦資訊處理標準 (FIPS) 組態設定資訊集合。FIPS 標準美國政府所設定的安全性標準，所有由非軍方之政府機構與政府合約商維護的電腦中，都必須使用這套標準。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Remove-CsFIPSConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會將 FIPS 組態設定全域集合中的屬性重設為其預設值。

    Remove-CsFIPSConfiguration -Identity "Global"

## 詳細描述

美國聯邦資訊處理標準 (FIPS) 是一系列的標準與準則，所有涉及美國政府工作的電腦都必須加以遵循；例如，管理密碼編譯、加密、數位簽章的 FIPS 標準 (如需詳細資訊，請參閱 <http://www.itl.nist.gov/fipspubs/by-num.htm>)。Lync Server 2013 可讓您選擇將軟體設成只使用符合 FIPS 標準的演算法。您如有參與美國政府 (或其他必須遵循 FIPS 的機構) 的工作，您可以啟用 Lync Server 2013 中的 FIPS 規範。

請注意，內部部署版的 Lync Server 只可有一個通用的 FIPS 組態設定集合，亦即您只能針對整個 Lync Server 實作啟用或停用 FIPS 規範，而無法只為個別網站或個別的登錄器集區啟用或停用 FIPS 規範。啟用 FIPS 規範之後，有可能會在嘗試與未遵循 FIPS 標準的組織進行通訊時發生問題。

預設會停用 Lync Server 2013的 FIPS 規範。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsFIPSConfiguration

**Lync Server 控制台：**Lync Server 控制台不提供 Remove-CsFIPSConfiguration Cmdlet 所執行的功能。

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
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要移除之 FIPS 組態設定的唯一識別。由於 Lync Server 2013只支援 FIPS 設定的單一全域集合，因此唯一可以刪除的集合是全域集合：</p>
<p>-Identity global</p>
<p>請注意，在此範例中，不會從系統實際移除全域集合；Lync Server 2013不支援刪除全域集合。而是將該集合中的唯一屬性 (RequireFIPSCompliantMedia) 重設為其預設值 False。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>所刪除的 FIPS 組態設定之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行下列命令傳回每個租用戶的租用戶識別碼：</p>
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

**Remove-CsFIPSConfiguration** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Settings.FIPSConfiguration.FIPSConfiguration 物件執行個體

## 傳回類型

無。反之，**Remove-CsFIPSConfiguration** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.WritableConfig.Settings.FIPSConfiguration.FIPSConfiguration 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsFIPSConfiguration](get-csfipsconfiguration.md)  
[New-CsFIPSConfiguration](new-csfipsconfiguration.md)  
[Set-CsFIPSConfiguration](set-csfipsconfiguration.md)

