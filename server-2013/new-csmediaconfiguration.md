---
title: New-CsMediaConfiguration
TOCTitle: New-CsMediaConfiguration
ms:assetid: 3b60c36f-f824-4948-aa46-6745b40b9641
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425881(v=OCS.15)
ms:contentKeyID: 49290646
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsMediaConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

建立新媒體設定的集合。這些設定可用於指定支援的加密層級及允許的最高視訊解析度等等。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsMediaConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-EnableQoS <$true | $false>] [-EnableSiren <$true | $false>] [-EncryptionLevel <SupportEncryption | RequireEncryption | DoNotSupportEncryption>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-MaxVideoRateAllowed <CIF250K | VGA600K | Hd720p15M>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 使用 **New-CsMediaConfiguration** Cmdlet 來建立 Identity 為 site:Redmond1 的新媒體組態。此新組態要求參與多媒體交談的雙方都使用加密。該需求是經由新增 EncryptionLevel 參數並將參數值設為 RequireEncryption 而建立。

    New-CsMediaConfiguration -Identity site:Redmond1 -EncryptionLevel RequireEncryption

## 範例 2

此範例會使用 **New-CsMediaConfiguration** Cmdlet 建立 Identity 為 MediationServer:pool0.litwareinc.com 的新媒體組態。這個新組態的 EnableSiren 值為 True，表示已針對與此中繼伺服器相關的電話啟用 Siren。

    New-CsMediaConfiguration -Identity MediationServer:pool0.litwareinc.com -EnableSiren $True

## 詳細描述

此 Cmdlet 會建立針對特定媒體動作定義行為的新設定集合。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsMediaConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsMediaConfiguration"}

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
<td><p>指定套用此組態之範圍 (網站或服務) 的唯一識別碼。網站範圍的組態應輸入為 site:&lt;網站名稱&gt;，例如 site:Redmond。服務應輸入為 &lt;伺服器角色&gt;:&lt;fqdn&gt;，例如 MediationServer:pool0.litwareinc.com。在全域範圍內應永遠存在媒體組態，而且不能移除，因此無法建立新的全域組態。</p>
<p>在服務範圍內建立的媒體組態只能針對音訊/視訊會議服務、中繼伺服器及應用程式伺服器建立。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableQoS</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>QoS 會監視網路上的語音訊號品質。</p>
<p>預設值：False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableSiren</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>根據預設，中繼伺服器不會為本身與其他 Lync 用戶端之間的通話協議 Siren 為可能的轉碼器。如果此設定為 True，會將 Siren 包含為可能的轉碼器，用於中繼伺服器和其他 Lync 用戶端之間。</p>
<p>預設值：False</p></td>
</tr>
<tr class="odd">
<td><p><em>EncryptionLevel</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Media.EncryptionLevel</p></td>
<td><p>整合通訊裝置之間的加密層級。</p>
<p>有效值：</p>
<p>SupportEncryption - 如果可以交涉，則使用安全即時傳輸通訊協定 (SRTP)。</p>
<p>RequireEncryption - 必須交涉 SRTP。</p>
<p>DoNotSupportEncryption - 不得使用 SRTP。</p>
<p>預設值：RequireEncryption</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="even">
<td><p><em>MaxVideoRateAllowed</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Media.MaxVideoRateAllowed</p></td>
<td><p>用戶端端點上傳送視訊訊號的最高速率。</p>
<p>有效值：Hd720p15M、VGA600K、CIF250K</p>
<p>Hd720p15M - 高畫質，解析度為 1280 x 720，長寬比為 16:9。</p>
<p>VGA600K - VGA，解析度為 640 x 480，25 fps，長寬比為 4:3。</p>
<p>CIF250K - Common Intermediate Format (CIF) 視訊格式，15 fps，解析度為 352 x 288。</p>
<p>請注意，這些值不區分大小寫；在建立組態時，值會轉換為適當大小寫。</p>
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

無。

## 傳回類型

建立 Microsoft.Rtc.Management.WritableConfig.Settings.Media.MediaSettings 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsMediaConfiguration](remove-csmediaconfiguration.md)  
[Set-CsMediaConfiguration](set-csmediaconfiguration.md)  
[Get-CsMediaConfiguration](get-csmediaconfiguration.md)

