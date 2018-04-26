---
title: Set-CsVoiceConfiguration
TOCTitle: Set-CsVoiceConfiguration
ms:assetid: dbab35ac-9a55-41d2-a726-9a26b2ff8e85
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398967(v=OCS.15)
ms:contentKeyID: 49292519
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoiceConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改語音測試組態的清單。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsVoiceConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsVoiceConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-VoiceTestConfigurations <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

在語音組態內修改測試語音組態需要數個步驟。在此範例中，一開始會先呼叫 **Get-CsVoiceConfiguration** Cmdlet 來擷取語音組態物件。然後將擷取的物件 (只會有一個) 指派給變數 $a。

我們在此範例的第 2 行中擷取了 VoiceTestConfigurations 內容的內容，其是來自變數 $a 的語音測試組態物件集合。接著將該集合傳送到 **Where-Object** Cmdlet，我們會在此處搜尋 Name 等於字串 TestConfig2 的語音測試組態物件集合。我們將該物件指定到變數 $b。

接下來，藉由將新值指派給 DialedNumber 和 ExpectedTranslatedNumber 屬性，來修改 TestConfig2 語音測試組態物件。更新該物件，即可更新變數 $a 中的物件。但是該物件仍然只留在記憶體中。最後一個步驟是，需要將 $a 傳遞給 **Set-CsVoiceConfiguration** Cmdlet，來儲存這些變更。

這不是修改語音組態的建議方式。若要修改語音組態，只需使用 **Set-CsVoiceTestConfiguration** Cmdlet 來變更個別語音測試組態，如下所示：

Set-CsVoiceTestConfiguration -Identity TestConfig2 -DialedNumber 5551212 -ExpectedTranslatedNumber +5551212

這一行會完成範例 1 所示的相同工作。

    $a = Get-CsVoiceConfiguration
    $b = $a.VoiceTestConfigurations | Where-Object {$_.Name -eq "TestConfig2"}
    $b.DialedNumber = "5551212"
    $b.ExpectedTranslatedNumber = "+5551212"
    Set-CsVoiceConfiguration -Instance $a

## 詳細描述

語音測試設定可根據特定語音原則、路由和撥號對應表，用來測試電話號碼。這個 Cmdlet 可以用來對 Lync Server 部署修改語音測試設定（從包含所有語音測試設定的清單）。

這個 Cmdlet 會修改屬於 VoiceConfiguration 類型的物件。由於此物件只是語音測試組態的容器物件，因此我們不建議使用這個 Cmdlet。若要修改語音設定，可呼叫 **Set-CsVoiceTestConfiguration** Cmdlet，修改個別的語音測試設定。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsVoiceConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoiceConfiguration"}

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
<td><p>SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>XdsIdentity</p></td>
<td><p>這個物件的範圍。此參數唯一可能的值是 Global。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>VoiceConfiguration</p></td>
<td><p>語音設定 (Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceConfiguration) 物件的參照。您可以呼叫 <strong>Get-CsVoiceConfiguration</strong> Cmdlet 來擷取此類型物件。</p></td>
</tr>
<tr class="odd">
<td><p><em>VoiceTestConfigurations</em></p></td>
<td><p>選用</p></td>
<td><p>PSListModifier</p></td>
<td><p>針對 Lync Server 部署定義的所有語音測試設定 (Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration 物件) 清單。</p>
<p>您應該使用 <strong>Set-CsVoiceTestConfiguration</strong> Cmdlet，修改個別的語音測試設定物件。那是修改此清單中之設定的建議方式。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceConfiguration 物件。**Set-CsVoiceConfiguration** Cmdlet 接受管線傳送的語音組態物件輸入。

## 傳回類型

**Set-CsVoiceConfiguration** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[Remove-CsVoiceConfiguration](remove-csvoiceconfiguration.md)  
[Get-CsVoiceConfiguration](get-csvoiceconfiguration.md)  
[New-CsVoiceTestConfiguration](new-csvoicetestconfiguration.md)  
[Set-CsVoiceTestConfiguration](set-csvoicetestconfiguration.md)  
[Get-CsVoiceTestConfiguration](get-csvoicetestconfiguration.md)

