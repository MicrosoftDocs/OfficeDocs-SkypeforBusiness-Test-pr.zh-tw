---
title: Get-CsDialInConferencingConfiguration
TOCTitle: Get-CsDialInConferencingConfiguration
ms:assetid: 75a959f7-5712-4dbc-b7ac-5a15b9b2f404
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398575(v=OCS.15)
ms:contentKeyID: 49291342
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsDialInConferencingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

擷取使用者加入或離開撥入式會議時， Lync Server 之回應方式的資訊。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsDialInConferencingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsDialInConferencingConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 會傳回組織目前所使用之所有電話撥入式會議組態設定的集合。呼叫不含任何額外參數的 **Get-CsDialInConferencingConfiguration** Cmdlet 一律會傳回完整的電話撥入式會議設定集合。

    Get-CsDialInConferencingConfiguration

## 範例 2

範例 2 會傳回 Identity 為 site:Redmond 的電話撥入式會議組態設定。

    Get-CsDialInConferencingConfiguration -Identity site:Redmond

## 範例 3

在範例 3 中，Filter 參數會用來傳回在網站範圍設定的所有電話撥入式會議設定。篩選值 "site:\*" 會指示 **Get-CsDialInConferencingConfiguration** Cmdlet 僅傳回 Identity 開頭為字串值 "site:" 的設定。根據設計，所有 Identity 開頭為 "site:" 的撥號會議設定，都代表是在網站範圍設定的設定。

    Get-CsDialInConferencingConfiguration -Filter "site:*"

## 範例 4

範例 4 會使用 **Get-CsDialInConferencingConfiguration** Cmdlet 和 **Where-Object** Cmdlet，以傳回 EnableNameRecording 屬性設為 False 之所有電話撥入式會議組態設定的集合。為達成此目的，會先呼叫不含任何參數的 **Get-CsDialInConferencingConfiguration** Cmdlet，以傳回所有電話撥入式會議設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 EnableNameRecording 屬性等於 False 的設定。

    Get-CsDialInConferencingConfiguration | Where-Object {$_.EnableNameRecording -eq $False}

## 詳細描述

當使用者加入 (或離開) 電話撥入式會議時， Lync Server 可以有不同的回應方式。例如，參與者在進入會議本身前，可能會被要求記錄他們的姓名。同樣的，系統管理員可決定他們是否要讓 Lync Server 宣告電話撥入式參與者已離開或加入會議。

這些會議「加入行為」是使用電話撥入式會議組態設定進行管理；這些設定可以在全域範圍或網站範圍設定 (在網站範圍設定的設定優先於在全域範圍設定的設定)。 **Get-CsDialInConferencingConfiguration** Cmdlet 可讓您擷取組織中目前使用中之電話撥入式會議組態設定的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsDialInConferencingConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsDialInConferencingConfiguration"}

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
<td><p>可讓您在指定電話撥入式會議組態設定時使用萬用字元。例如，若要傳回已在網站範圍套用之所有組態設定的集合，請使用下列語法：-Filter &quot;site:*&quot;。若要傳回 Identity 包含 &quot;EMEA&quot; 一詞的所有設定，請使用下列語法：-Filter &quot;*EMEA*&quot;。請注意，Filter 參數只可用於 Identity 而無法用於篩選其他電話撥入式會議組態屬性。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>表示要擷取之電話撥入式會議組態設定的 Identity。若要參考全域設定，請使用下列語法：-Identity global。若要參考網站設定，請使用類似下列的語法：-Identity site:Redmond。您無法在指定 Identity 時使用萬用字元。若執行該作業，請改用 Filter 參數。</p>
<p>如果呼叫不含任何參數的 <strong>Get-CsDialInConferencingConfiguration</strong> Cmdlet，將會傳回組織中使用之所有電話撥入式會議組態設定的資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區 的本機複本擷取電話撥入式會議資料，而不從 中央管理存放區 本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Get-CsDialInConferencingConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsDialInConferencingConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.DialInConferencingConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsDialInConferencingConfiguration](new-csdialinconferencingconfiguration.md)  
[Remove-CsDialInConferencingConfiguration](remove-csdialinconferencingconfiguration.md)  
[Set-CsDialInConferencingConfiguration](set-csdialinconferencingconfiguration.md)

