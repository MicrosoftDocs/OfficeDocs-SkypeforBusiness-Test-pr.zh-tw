---
title: Set-CsDialPlan
TOCTitle: Set-CsDialPlan
ms:assetid: 80277dc6-8853-4cbd-87cb-e64f9e135d5f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398644(v=OCS.15)
ms:contentKeyID: 49291472
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsDialPlan

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的撥號對應表。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsDialPlan [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsDialPlan [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-City <String>] [-Confirm [<SwitchParameter>]] [-CountryCode <String>] [-Description <String>] [-DialinConferencingRegion <String>] [-ExternalAccessPrefix <String>] [-Force <SwitchParameter>] [-NormalizationRules <PSListModifier>] [-OptimizeDeviceDialing <$true | $false>] [-SimpleName <String>] [-State <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

在範例 1 中，**Set-CsDialPlan** Cmdlet 可用來修改 Identity 為 RedmondDialPlan 的撥號對應表。在此範例中，唯一修改的屬性是 Description；修改方式是指定 Description 參數，後面加上新的描述文字。

    Set-CsDialPlan -Identity RedmondDialPlan -Description "This plan is for Redmond-based users only."

## 範例 2

此範例使用 **Set-CsDialPlan** Cmdlet 變更設定供組織使用之所有撥號對應表的 ExternalAccessPrefix 屬性值。為達成此目的，命令會先使用 **Get-CsDialPlan** Cmdlet 傳回組織中所有撥號對應表的集合。然後將該集合管線傳送至 **Set-CsDialPlan** Cmdlet，以將集合中每個設定檔的 ExternalAccessPrefix 屬性的值指定為 8。

    Get-CsDialPlan | Set-CsDialPlan -ExternalAccessPrefix 8

## 詳細描述

此 Cmdlet 會修改現有的撥號對應表 (又稱為位置設定檔)。撥號對應表可提供 Enterprise Voice 使用者撥打電話所需的資訊。會議服務員應用程式也會在執行電話撥入式會議時使用撥號對應表。撥號對應表可指定所要套用的正規化規則，以及撥打外線時是否需要先撥首碼。

附註：雖然可以使用這個 Cmdlet 來修改撥號對應表的正規化規則，不過建議您改用 **New-CsVoiceNormalizationRule** Cmdlet、**Set-CsVoiceNormalizationRule** Cmdlet 或 **Remove-CsVoiceNormalizationRule** Cmdlet。使用那些 Cmdlet 所進行的變更會反映在對應的撥號對應表中。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsDialPlan** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsDialPlan"}

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
<td><p><em>City</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此參數不會搭配這個 Cmdlet 使用。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>CountryCode</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此參數不會搭配這個 Cmdlet 使用。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此撥號對應表的描述：用途、適用的使用者類型，或有助於識別撥號對應表用途的其他任何資訊。</p>
<p>字元數上限：512</p></td>
</tr>
<tr class="odd">
<td><p><em>DialinConferencingRegion</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>與此撥號對應表相關聯的區域名稱。如果撥號對應表要用於電話撥入式會議，請指定此參數的值。如此可在會議召集人設定會議時讓系統指派正確的存取號碼。您可以呼叫 <strong>Get-CsNetworkRegion</strong> Cmdlet 來擷取可用的區域。</p>
<p>字元數上限：512</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalAccessPrefix</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>一個號碼 (或一組號碼)，指定組織外部的電話(例如，若要撥外線，請先按 9)。正規化規則會忽略此首碼，但這些規則會套用至號碼的其餘部分。</p>
<p>OptimizeDeviceDialing 參數必須設為 True，此值才會生效。</p>
<p>此參數的值必須符合規則運算式 [0-9]{1,4}。這表示它必須是長度為一至四位數的值，每個數字必須是 0 至 9 的數字。</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏進行變更前的任何確認提示。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>指定範圍，或指定各使用者對應表名稱之唯一識別碼，以識別您要修改的撥號對應表。例如，網站 Identity 是以 site:&lt;網站名稱&gt; 格式輸入，其中網站名稱是網站的名稱。在服務範圍的撥號對應表將是登錄器服務或 PSTN 閘道服務，其中的 Identity 值格式如下：Registrar:Redmond.litwareinc.com。個別使用者 Identity 將是唯一的字串值。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>LocationProfile</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。您可以呼叫 <strong>Get-CsDialPlan</strong> Cmdlet 擷取此物件參考。</p></td>
</tr>
<tr class="even">
<td><p><em>NormalizationRules</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>套用至此撥號對應表的正規化規則清單。</p>
<p>雖然可以直接使用此 Cmdlet 來修改此清單和這些規則，但建議您使用 <strong>New-CsVoiceNormalizationRule</strong> Cmdlet 來建立正規化規則，這樣會建立規則並將它指派給指定的撥號對應表，並利用 <strong>Set-CsVoiceNormalizationRule</strong> Cmdlet 來修改他們。</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>OptimizeDeviceDialing</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>將此參數設為 True 可將 ExternalAccessPrefix 參數中的首碼套用至從組織外撥打的電話。唯有在已指定 ExternalAccessPrefix 參數值的情況下才能將這個值設為 True。</p></td>
</tr>
<tr class="even">
<td><p><em>SimpleName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>撥號對應表的易記名稱。撥號對應表名稱在 Lync Server 部署內的所有撥號對應表之間必須是唯一的。</p>
<p>這個字串最長可為 256 個字元。有效字元是字母或數值字元、連字號 (-)、點 (.)、加號 (+)、底線 (_) 和括弧 (())。</p>
<p></p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.LocationProfile 物件。接受撥號對應表物件管線傳送的輸入。

## 傳回類型

**Set-CsDialPlan** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.LocationProfile 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsDialPlan](new-csdialplan.md)  
[Remove-CsDialPlan](remove-csdialplan.md)  
[Get-CsDialPlan](get-csdialplan.md)  
[Grant-CsDialPlan](grant-csdialplan.md)  
[Test-CsDialPlan](test-csdialplan.md)  
[New-CsVoiceNormalizationRule](new-csvoicenormalizationrule.md)  
[Set-CsVoiceNormalizationRule](set-csvoicenormalizationrule.md)  
[Remove-CsVoiceNormalizationRule](remove-csvoicenormalizationrule.md)  
[Get-CsVoiceNormalizationRule](get-csvoicenormalizationrule.md)

