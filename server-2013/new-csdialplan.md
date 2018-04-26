---
title: New-CsDialPlan
TOCTitle: New-CsDialPlan
ms:assetid: 3889c696-1070-47bd-beb9-da7e18ec90f0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425860(v=OCS.15)
ms:contentKeyID: 49290606
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsDialPlan

 

_**上次修改主題的時間：** 2015-03-09_

建立新的撥號對應表。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsDialPlan -Identity <XdsIdentity> [-City <String>] [-Confirm [<SwitchParameter>]] [-CountryCode <String>] [-Description <String>] [-DialinConferencingRegion <String>] [-ExternalAccessPrefix <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-NormalizationRules <PSListModifier>] [-OptimizeDeviceDialing <$true | $false>] [-SimpleName <String>] [-State <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會建立 Identity 為 RedmondDialPlan 的新撥號對應表(如果 Identity 值中缺少範圍，則表示這是個別使用者原則。個別使用者範圍中建立的撥號對應表可以直接指派給使用者和群組)。撥號對應表的所有其他屬性會指派預設值。

    New-CsDialPlan -Identity RedmondDialPlan

## 範例 2

範例 2 所示的命令會建立其 Identity 為 site:Redmond 的新撥號對應表 (這表示撥號對應表會套用到 Redmond 網站上未指派有個別使用者或服務層級撥號對應表的所有使用者) 與 SimpleName RedmondSiteDialPlan。範例中的下一行接著會建立與該對應表相關聯的新正規化規則。儘管已針對撥號對應表建立預設的正規化規則，但在大部分的情況下這都是為預留位置而建立的 - 值的用途有限。因此，在呼叫 **New-CsDialPlan** Cmdlet 來建立新的撥號對應表之後，您應該呼叫 **New-CsVoiceNormalizationRule** Cmdlet 以建立適用於組織的具名規則。這就是此範例第 2 行的確實用途：呼叫 **New-CsVoiceNormalizationRule** Cmdlet 為 Redmond 網站建立名為 SeattlePrefix 的規則，並指定規則的 Pattern 和 Translation 內容。不需要採取其他步驟來修改撥號對應表；對正規化規則所進行的變更會自動套用至識別符合正規化規則的撥號對應表 (Identity 的 site:Redmond 部分符合撥號對應表 Identity；SeattlePrefix 是正規化規則的名稱。多個正規化規則可以套用至一個撥號對應表，因此每一個正規化規則在指定的範圍內都需要唯一的名稱)。

    New-CsDialPlan -Identity site:Redmond -SimpleName RedmondSiteDialPlan
    New-CsVoiceNormalizationRule -Identity "site:Redmond/SeattlePrefix" -Pattern "^9(\d*){1,5}$" -Translation "+1206$1"

## 範例 3

範例 3 所示的命令會建立 Identity 為 RedmondDialPlan 的新撥號對應表，並指定 Description 來說明撥號對應表的用途為何(個別使用者範圍中建立的撥號對應表可以直接指派給使用者和群組)。其他所有參數中會指派預設值。

    New-CsDialPlan -Identity RedmondDialPlan -Description "Dial plan for Redmond users"

## 詳細描述

此 Cmdlet 會建立新的撥號對應表 (又稱為位置設定檔)。撥號對應表可提供 Enterprise Voice 使用者撥打電話所需的資訊。會議服務員應用程式也會在執行電話撥入式會議時使用撥號對應表。撥號對應表可指定所要套用的正規化規則，以及撥打外線時是否需要先撥首碼。

建立撥號對應表時也會自動建立預設的語音正規化規則。您可以呼叫 **Set-CsVoiceNormalizationRule** Cmdlet 來修改語音正規化規則，也可以呼叫 **New-CsVoiceNormalizationRule** Cmdlet 將新的正規化規則新增至撥號對應表。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsDialPlan** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsDialPlan"}

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
<td><p>指定用來識別撥號對應表之範圍和名稱 (網站)、服務角色和 FQDN 或名稱 (每個使用者) 的唯一識別碼。例如，網站 Identity 是以 site:&lt;網站名稱&gt; 格式輸入，其中網站名稱是網站的名稱。在服務範圍的撥號對應表必須是登錄器服務或 PSTN 閘道服務，其中的 Identity 值格式如下：Registrar:Redmond.litwareinc.com。個別使用者 Identity 只要以唯一字串值的形式輸入即可。</p></td>
</tr>
<tr class="even">
<td><p><em>City</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此參數不會搭配這個 Cmdlet 使用。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>CountryCode</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此參數不會搭配這個 Cmdlet 使用。</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此撥號對應表的描述：用途、適用的使用者類型，或有助於識別撥號對應表用途的其他任何資訊。</p>
<p>字元數上限：512</p></td>
</tr>
<tr class="even">
<td><p><em>DialinConferencingRegion</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>與此撥號對應表相關聯的區域名稱。如果撥號對應表要用於電話撥入式會議，請指定此參數的值。如此可在會議召集人設定會議時讓系統指派正確的存取號碼。您可以呼叫 <strong>Get-CsNetworkRegion</strong> Cmdlet 來擷取可用的區域。</p>
<p>字元數上限：512</p></td>
</tr>
<tr class="odd">
<td><p><em>ExternalAccessPrefix</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>一個號碼 (或一組號碼)，指定組織外部的電話(例如，若要撥外線，請先按 9)。正規化規則會忽略此首碼，但這些規則會套用至號碼的其餘部分。</p>
<p>OptimizeDeviceDialing 參數必須設為 True，此值才會生效。</p>
<p>此參數必須符合規則運算式 [0-9]{1,4}。這表示它必須是 0 至 9 的值，長度為一至四位數。</p>
<p>預設值：9</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏進行變更前的任何確認提示。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="even">
<td><p><em>NormalizationRules</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>套用至此撥號對應表的正規化規則清單。</p>
<p>雖然可以直接使用此 Cmdlet 來建立此清單和這些規則，但建議您使用 <strong>New-CsVoiceNormalizationRule</strong> Cmdlet 來建立正規化規則，這樣會建立規則並將它指派給指定的撥號對應表。</p>
<p>每次建立新的撥號對應表時，系統會對該網站、服務或個別使用者撥號對應表，建立具有預設設定的新語音正規則化規則。新語音正規化規則的 Identity 預設為撥號對應表的 Identity，後面加上斜線，再加上名稱 Prefix All。例如 site:Redmond/Prefix All。</p>
<p>預設值：{Description=;Pattern=^(\d11)$;Translation=+$1;Name=Prefix All;IsInternalExtension=False } 注意：此預設值只是預留位置。若要讓撥號對應表的實用性高，您應修改撥號對應表建立的正規化規則，或為網站、服務或使用者建立新的規則。您可以呼叫 <strong>New-CsVoiceNormalizationRule</strong> Cmdlet 來建立新的正規化規則，呼叫 <strong>Set-CsVoiceNormalizationRule</strong> Cmdlet 來修改正規化規則。</p></td>
</tr>
<tr class="odd">
<td><p><em>OptimizeDeviceDialing</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>將此參數設為 True 可將 ExternalAccessPrefix 參數中的首碼套用至從組織外撥打的電話。唯有在已指定 ExternalAccessPrefix 參數值的情況下才能將這個值設為 True。</p>
<p>預設值：False</p></td>
</tr>
<tr class="even">
<td><p><em>SimpleName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>撥號對應表的顯示名稱。此名稱在 Lync Server 部署內的所有撥號對應表之間必須是唯一的。</p>
<p>這個字串最長可為 256 個字元。有效字元是字母或數值字元、連字號 (-)、點 (.)、加號 (+)、底線 (_) 和括弧 (())。</p>
<p>此參數必須包含值。然而，如果您未在呼叫 <strong>New-CsDialPlan</strong> Cmdlet 時提供值，則會提供預設值。全域撥號對應表的預設值是 Prefix All。網站層級撥號對應表的預設值是網站的名稱。服務的預設值是服務 (登錄器服務或 PSTN 閘道服務) 的名稱，後面加上底線，然後再加上服務完整網域名稱 (FQDN)。例如 Registrar_pool0.litwareinc.com。個別使用者撥號對應表的預設值是撥號對應表的 Identity。</p></td>
</tr>
<tr class="odd">
<td><p><em>State</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此參數不會搭配這個 Cmdlet 使用。</p></td>
</tr>
<tr class="even">
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

此 Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.LocationProfile 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsDialPlan](remove-csdialplan.md)  
[Set-CsDialPlan](set-csdialplan.md)  
[Get-CsDialPlan](get-csdialplan.md)  
[Grant-CsDialPlan](grant-csdialplan.md)  
[Test-CsDialPlan](test-csdialplan.md)  
[New-CsVoiceNormalizationRule](new-csvoicenormalizationrule.md)  
[Set-CsVoiceNormalizationRule](set-csvoicenormalizationrule.md)  
[Remove-CsVoiceNormalizationRule](remove-csvoicenormalizationrule.md)  
[Get-CsVoiceNormalizationRule](get-csvoicenormalizationrule.md)

