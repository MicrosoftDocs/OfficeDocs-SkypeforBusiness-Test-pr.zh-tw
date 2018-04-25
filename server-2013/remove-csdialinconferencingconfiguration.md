---
title: Remove-CsDialInConferencingConfiguration
TOCTitle: Remove-CsDialInConferencingConfiguration
ms:assetid: 0c7f2a69-eeed-41bf-8ba7-5cc36dfdfa3c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398174(v=OCS.15)
ms:contentKeyID: 49290068
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsDialInConferencingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除一或多個電話撥入式會議組態設定的集合。這些設定可決定使用者參與或離開電話撥入式會議時，Lync Server 的回應方式。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsDialInConferencingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會刪除 Redmond 網站的電話撥入式會議組態設定。

    Remove-CSDialInConferencingConfiguration -Identity "site:Redmond"

## 範例 2

範例 2 會刪除網站範圍所設定的所有電話撥入式會議設定。為達成此目的，命令會先使用 **Get-CSDialInConferencingConfiguration** Cmdlet 搭配 Filter 參數，傳回已在網站範圍設定之所有電話撥入式會議設定的集合 (篩選值 "site:\*" 可確保只會傳回 Identity 開頭為 "site:" 字串值的設定)。然後再將篩選後的集合管線傳送到 **Remove-CSDialInConferencingConfiguration** Cmdlet，以移除集合中的每個項目。

    Get-CSDialInConferencingConfiguration -Filter "site:*" | Remove-CSDialInConferencingConfiguration

## 範例 3

範例 3 會刪除不使用名稱記錄的所有電話撥入式會議組態設定。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CSDialInConferencingConfiguration** Cmdlet，以傳回組織目前所使用之所有電話撥入式會議組態設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 EnableNameRecording 屬性等於 False 的設定。接著將篩選後的集合管線傳送到 **Remove-CSDialInConferencingConfiguration** Cmdlet，以刪除集合中的每個項目。

    Get-CSDialInConferencingConfiguration | Where-Object {$_.EnableNameRecording -eq $False} | Remove-CSDialInConferencingConfiguration

## 詳細描述

當使用者加入 (或離開) 電話撥入式會議時，Lync Server 可以使用不同方式回應。例如，可能會要求參與者必須在進入會議前記錄他們的名字。同樣地，系統管理員可以決定是否要讓 Lync Server 宣告電話撥入式參與者已離開或加入會議。

這些會議「加入行為」是使用電話撥入式會議組態設定進行管理；這些設定可以在全域範圍或網站範圍設定 (在網站範圍設定的設定優先於在全域範圍設定的設定)。當您安裝 Lync Server 時，會為您建立全域的電話撥入式會議組態設定集合。如果您希望網站 (或一組網站) 具有不同的設定，您可以使用 **New-CSDialInConferencingConfiguration** Cmdlet 建立這些集合。

**Remove-CSDialInConferencingConfiguration** Cmdlet 會刪除已在網站範圍設定的任何電話撥入式會議設定。刪除這些網站專屬的設定時，位於受影響網站之使用者的電話撥入式會議行為會由全域設定管理。

您也可以針對全域電話撥入式會議設定執行 **Remove-CSDialInConferencingConfiguration** Cmdlet。如果您這樣做，將不會移除全域設定；那是因為您無法移除全域設定，而是將該設定之集合中的所有屬性重設為其預設值。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsDialInConferencingConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsDialInConferencingConfiguration"}

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
<td><p>表示要移除之電話撥入式會議組態設定的 Identity。若要參考全域設定，請使用下列語法：-Identity global。若要參照網站設定，請使用類似下列的語法：-Identity site:Redmond。請注意，如有指定 Identity，即無法使用萬用字元。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.DialInConferencingConfiguration 物件。**Remove-CSDialInConferencingConfiguration** Cmdlet 接受管線傳送的電話撥入式會議組態物件執行個體。

## 傳回類型

無。反之， **Remove-CSDialInConferencingConfiguration** Cmdlet 會刪除 Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.DialInConferencingConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsDialInConferencingConfiguration](get-csdialinconferencingconfiguration.md)  
[New-CsDialInConferencingConfiguration](new-csdialinconferencingconfiguration.md)  
[Set-CsDialInConferencingConfiguration](set-csdialinconferencingconfiguration.md)

