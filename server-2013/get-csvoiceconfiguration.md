---
title: Get-CsVoiceConfiguration
TOCTitle: Get-CsVoiceConfiguration
ms:assetid: c5e7afa3-28d3-4bf9-a2f2-c34932c9a3cd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398815(v=OCS.15)
ms:contentKeyID: 49292255
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsVoiceConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

擷取包含 Lync Server 部署所定義之所有語音測試設定完整清單的語音設定物件。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsVoiceConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsVoiceConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

這個範例會擷取語音設定。若要擷取語音測試設定，請使用 **Get-CsVoiceTestConfiguration** Cmdlet。

    Get-CsVoiceConfiguration

## 詳細描述

語音測試設定可根據特定語音原則、路由和撥號對應表，用來測試電話號碼。使用這個 Cmdlet 可擷取全域執行個體，這個執行個體保留 Lync Server 部署內定義之所有語音測試設定的清單。若要擷取個別語音測試設定，或以個別物件而非清單形式來擷取這些設定，請使用 **Get-CsVoiceTestConfiguration** Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsVoiceConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsVoiceConfiguration"}

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
<td><p>此物件只能有一個執行個體，所以此參數不會進行任何動作。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要擷取之語音設定的範圍。唯一可能的值是 Global。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區本機複本擷取語音組態，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

此 Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[Remove-CsVoiceConfiguration](remove-csvoiceconfiguration.md)  
[Set-CsVoiceConfiguration](set-csvoiceconfiguration.md)  
[Get-CsVoiceTestConfiguration](get-csvoicetestconfiguration.md)

