---
title: Set-CsMediaConfiguration
TOCTitle: Set-CsMediaConfiguration
ms:assetid: 768bc273-5253-4569-895d-5b1127386b92
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398580(v=OCS.15)
ms:contentKeyID: 49291358
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsMediaConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的媒體設定集合。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsMediaConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsMediaConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-EnableQoS <$true | $false>] [-EnableSiren <$true | $false>] [-EncryptionLevel <SupportEncryption | RequireEncryption | DoNotSupportEncryption>] [-Force <SwitchParameter>] [-MaxVideoRateAllowed <CIF250K | VGA600K | Hd720p15M>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會修改 Identity 為 site:Redmond1 的媒體設定集合；特別是命令會將 MaxVideoRateAllowed 屬性的值設為 Hd720p15M。請注意，傳遞給 MaxVideoRateAllowed 參數的值必須是參數描述中指定的其中一個值。也請注意，值不區分大小寫；此處輸入為 hd720p15m 的值會自動轉換成適當大小寫 (此範例中會轉換成 Hd720p15M)。

    Set-CsMediaConfiguration -Identity site:Redmond1 -MaxVideoRateAllowed hd720p15m

## 範例 2

此範例會將 Identity 為 site:Redmond1 的媒體組態集合修改為 EncryptionLevel 值等於 DoNotSupportEncryption。請注意，此值不區分大小寫；輸入的值為 donotsupportencryption，但該值可視為有效值，並會自動變更為混合大小寫 (DoNotSupportEncryption)。

    Set-CsMediaConfiguration site:Redmond1 -EncryptionLevel donotsupportencryption

## 詳細描述

此 Cmdlet 會修改定義媒體組態的設定集合。這些動作與用戶端端點之間的音訊和視訊呼叫相關。

誰可以執行這個 Cmdlet：根據預設，下列群組的成員經過授權，可在本機執行 **Set-CsMediaConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsMediaConfiguration"}

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
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableQoS</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>QoS 會監視網路上的語音訊號品質。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableSiren</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>根據預設，中繼伺服器不會為本身與其他 Lync 用戶端之間的通話協議 Siren 為可能的轉碼器。如果此設定為 True，會將 Siren 包含為可能的轉碼器，用於中繼伺服器和其他 Lync 用戶端之間。</p></td>
</tr>
<tr class="even">
<td><p><em>EncryptionLevel</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Media.EncryptionLevel</p></td>
<td><p>整合通訊裝置之間的加密層級。</p>
<p>有效值：</p>
<p>SupportEncryption - 如果可以交涉，則使用安全即時傳輸通訊協定 (SRTP)。</p>
<p>RequireEncryption - 必須交涉 SRTP。</p>
<p>DoNotSupportEncryption - 不得使用 SRTP。</p>
<p>此值不區分大小寫(如需詳細資訊，請參閱本主題中的範例)。</p>
<p>預設值：RequireEncryption</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>您要變更之媒體組態設定的唯一識別碼。此識別碼會指定套用此組態的範圍 (全域、網站或服務)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>MediaSettings</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Media.MediaSettings 物件的執行個體。您可以呼叫 <strong>Get-CsMediaConfiguration</strong> Cmdlet 並指定特定 Identity 來擷取此物件。接著將該物件傳遞至 <strong>Set-CsMediaConfiguration</strong> Cmdlet，即可將新的值指派給該物件的屬性並儲存變更。</p></td>
</tr>
<tr class="even">
<td><p><em>MaxVideoRateAllowed</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Media.MaxVideoRateAllowed</p></td>
<td><p>用戶端端點上傳送視訊訊號的最高速率。</p>
<p>有效值：Hd720p15M，VGA600K，CIF250K</p>
<p>Hd720p15M - 高畫質，解析度為 1280 x 720，長寬比為 16:9。</p>
<p>VGA600K - VGA，解析度為 640 x 480，25 fps，長寬比為 4:3。</p>
<p>CIF250K - Common Intermediate Format (CIF) 視訊格式，15 fps，解析度為 352 x 288。</p>
<p>請注意，這些值不區分大小寫；在建立組態時，值會轉換為適當大小寫。(如需詳細資訊，請參閱本主題中的範例)。</p>
<p>預設值：VGA600K</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Settings.Media.MediaSettings 物件。接受媒體組態物件的管線傳送資料。

## 傳回類型

**Set-CsMediaConfiguration** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Settings.Media.MediaSettings 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsMediaConfiguration](new-csmediaconfiguration.md)  
[Remove-CsMediaConfiguration](remove-csmediaconfiguration.md)  
[Get-CsMediaConfiguration](get-csmediaconfiguration.md)

