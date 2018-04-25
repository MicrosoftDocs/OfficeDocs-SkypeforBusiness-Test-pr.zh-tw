---
title: New-CsNetworkMediaBypassConfiguration
TOCTitle: New-CsNetworkMediaBypassConfiguration
ms:assetid: 24055ae5-7fc8-4ca5-9e65-ac3a1f17b405
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425718(v=OCS.15)
ms:contentKeyID: 49290347
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkMediaBypassConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

為媒體旁路建立新的全域設定。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsNetworkMediaBypassConfiguration [-AlwaysBypass <$true | $false>] [-BypassID <String>] [-Enabled <$true | $false>] [-EnableDefaultBypassID <$true | $false>] [-EnabledForAudioVideoConferences <$true | $false>] [-ExternalBypassMode <Off | ICE | Any>] [-InternalBypassMode <Off | ICE | Any>]

## 範例

## 範例 1

此範例中的命令可啟用媒體旁路，並設定為永遠嘗試旁路。範例的第一行會呼叫 **New-CsNetworkMediaBypassConfiguration** Cmdlet。我們傳遞兩個參數到此 Cmdlet：AlwaysBypass 和 Enabled，將兩者都設為 True ($true)。Enabled 設為 True 可啟用媒體旁路，AlwaysBypass 設為 True 可確保嘗試對所有通話執行媒體旁路 (請注意，設定這兩個參數會自動產生 BypassID 屬性值)。**New-CsNetworkMediaBypassConfiguration** Cmdlet 只會在記憶體中建立物件，所以我們將該物件指派至變數 $a。

媒體旁路組態會與網路組態設定一起儲存。因此，在範例的第 2 行，利用呼叫 **Set-CsNetworkConfiguration** Cmdlet，將第 1 行所建立之媒體旁路組態物件 ($a) 傳遞給 MediaBypassSettings 參數，以將媒體旁路組態變更儲存至網路組態。

    $a = New-CsNetworkMediaBypassConfiguration -AlwaysBypass $true -Enabled $true
    Set-CsNetworkConfiguration -MediaBypassSettings $a

## 範例 2

Lync Server 不提供 **Set-CsNetworkMediaBypassConfiguration** Cmdlet，所以為了修改現有設定，您必須建立新組態 (如範例 1 所示) 來取代現有組態，或是修改現有設定。作法是擷取現有設定加以修改，然後使用 **Set-CsNetworkConfiguration** Cmdlet 儲存變更。此範例示範會使用後者關閉 Always Bypass 選項。

範例的第一行會擷取現有的媒體旁路設定。作法是呼叫 **Get-CsNetworkConfiguration** Cmdlet。在括弧內呼叫此 Cmdlet，以確保在執行命令的所有其他部分之前，已先完成該 Cmdlet。**Get-CsNetworkConfiguration** Cmdlet 會擷取整個網路組態的所有設定。因為我們只需要媒體旁路設定，所以我們指定 MediaBypassSettings 屬性，以便只擷取那些設定。將那些設定指派至變數 $a。

在第二行中，我們利用指派 False ($false) 值給 AlwaysBypass 屬性來修改儲存在變數 $a 中的設定。最後，在第 3 行中呼叫 **Set-CsNetworkConfiguration** Cmdlet，將 MediaBypassSettings 參數傳遞給變數 $a，來儲存我們對 AlwaysBypass 屬性所做的變更。

    $a = (Get-CsNetworkConfiguration).MediaBypassSettings
    $a.AlwaysBypass = $false
    Set-CsNetworkConfiguration -MediaBypassSettings $a

## 詳細描述

這個 Cmdlet 會建立音訊連線媒體旁路的全域設定。

與 Lync Server 中的 New- Cmdlet 不同，此 Cmdlet 不會立即儲存新組態，它只會在記憶體中建立設定。此 Cmdlet 所建立的物件必須儲存到變數，然後指派至網路組態的 MediaBypassSettings 屬性 (如需更多詳細資料，請參閱本主題中的＜範例＞一節)。

使用這個 Cmdlet 所建立的設定，只能透過存取全域網路組態的 MediaBypassSettings 屬性來擷取。若要擷取這些設定，請執行此命令：(Get-CsNetworkConfiguration).MediaBypassSettings。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsNetworkMediaBypassConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkMediaBypassConfiguration"}

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
<td><p><em>AlwaysBypass</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>將此參數設為 True，將嘗試對所有通話執行媒體旁路。</p>
<p>只有在停用通話許可控制 (CAC) 時，才將此參數值設為 True。僅在用於滿足下列條件的部署時，才將此參數設為 True：</p>
<p>- 不需要頻寬控制。</p>
<p>- 不需要精細的組態來決定旁路的發生時機。</p>
<p>- 閘道和用戶端之間有完整的連線能力。</p>
<p>如果將 Enabled 參數設為 True 並且將 AlwaysBypass 設為 False，旁路邏輯會使用網路組態網站和地區來決定旁路的發生時機。</p>
<p>如果您將 AlwaysBypass 設為 True，但沒有將 Enabled 參數的值也設為 True，則會收到警告訊息：將 Enabled 設為 False 會略過 AlwaysBypass 設定。</p>
<p>同時將 AlwaysBypass 和 Enabled 設為 True 會自動產生旁路 ID，這個旁路 ID 會儲存在 BypassID 屬性中。</p>
<p>預設值：False</p></td>
</tr>
<tr class="even">
<td><p><em>BypassID</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>媒體旁路 ID。如果將 AlwaysBypass 參數設為 True 並提供此參數的值，BypassID 將和所有子網路相關聯。如果 AlwaysBypass 為 False，BypassID 值會和所有位在網路組態網站及區域之外的子網路相關聯。</p>
<p>ID 的格式必須為 GUID (例如，96f14dea-5170-429a-b92b-f1cb909c4bb6)。不過您通常不需要設定或變更此參數。當 Enabled 設為 True 或下列情況下，會自動產生這個值：1) AlwaysBypass 設為 True，或 2) EnableDefaultBypassID 參數設為 True。</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>將此參數設為 True 以啟用媒體旁路。此時，旁路決策將取決於 AlwaysBypass 設定的值，如下所示：</p>
<p>- 如果 AlwaysBypass 為 True，則嘗試對所有通話執行旁路。</p>
<p>- 如果 AlwaysBypass 為 False，則會使用網路組態網站和區域來決定執行旁路的時機。</p>
<p>預設值：False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableDefaultBypassID</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>此值僅適用於當 AlwaysBypass 已設為 False 時。</p>
<p>將這個值設為 True 會自動產生預設旁路 ID。這個自動產生的值會儲存在 BypassID 屬性。</p>
<p>當連線良好的核心包含有頻寬限制連結的遠端網站時，此參數就很有用。系統管理員只需要透過網路組態網站及區域來定義和遠端網站相關聯的子網路，而不需要定義任何和核心相關聯的子網路。系統會自動在這些子網路之間嘗試執行旁路。</p>
<p>預設值：False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnabledForAudioVideoConferences</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>指出是否應該為音訊/視訊會議使用媒體旁路。預設值為 False ($False)。</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalBypassMode</em></p></td>
<td><p>選用</p></td>
<td><p>BypassModeEnumType</p></td>
<td><p>保留供未來使用。Lync Server 不支援外部媒體旁路。</p>
<p>預設值：Off</p></td>
</tr>
<tr class="odd">
<td><p><em>InternalBypassMode</em></p></td>
<td><p>選用</p></td>
<td><p>BypassModeEnumType</p></td>
<td><p>此參數的值會控制從組織網路內部進行連線之用戶端能嘗試執行媒體旁路的時機。如果 Enabled 設為 True，這個值會自動變更為 Any。此參數的其他值已獲得保留，以供未來之用。</p>
<p>預設值：Off</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

建立 Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.MediaBypassSettingsType 類型的物件參考。

## 請參閱

#### 其他資源

[Get-CsNetworkConfiguration](get-csnetworkconfiguration.md)  
[Set-CsNetworkConfiguration](set-csnetworkconfiguration.md)

