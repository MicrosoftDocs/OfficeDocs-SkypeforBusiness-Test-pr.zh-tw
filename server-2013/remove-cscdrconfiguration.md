---
title: Remove-CsCdrConfiguration
TOCTitle: Remove-CsCdrConfiguration
ms:assetid: 64352746-a03c-434a-9baf-4d9cd630e9da
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398451(v=OCS.15)
ms:contentKeyID: 49291125
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsCdrConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除指定的通話詳細記錄 (CDR) 設定集合。CDR 可讓您追蹤對等立即訊息工作階段、Voice over Internet Protocol (VoIP) 電話及會議電話等的使用狀況。這項使用狀況資料包括了誰撥電話給誰、撥話時間，以及通話時間長度等資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsCdrConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會使用 **Remove-CsCdrConfiguration** Cmdlet 移除指派給 Redmond 網站的 CDR 設定。使用 Identity 參數可確保只移除指派給指定網站的設定。

    Remove-CsCdrConfiguration -Identity site:Redmond

## 範例 2

範例 2 所示命令會移除已在網站範圍指派的所有 CDR 設定。為達成此目的，命令會先使用 **Get-CsCdrConfiguration** Cmdlet 並搭配 Filter 參數，以擷取適當的 CDR 設定；字串值 "site:\*" 可確保只會傳回 Identity 開頭為字元 "site:" 的設定。然後再將篩選後的集合管線傳送到 **Remove-CsCdrConfiguration** Cmdlet，以刪除集合中的所有項目。

    Get-CsCdrConfiguration -Filter site:* | Remove-CsCdrConfiguration

## 範例 3

範例 3 中會刪除任何 KeepCallDetailForDays 屬性小於 30 天的 CDR 設定。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsCdrConfiguration** Cmdlet，以傳回組織中目前使用的所有 CDR 設定集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 KeepCallDetailForDays 屬性小於 30 天的設定。接著將篩選後的集合管線傳送到 **Remove-CsCdrConfiguration** Cmdlet，以刪除集合中的每一個項目。

    Get-CsCdrConfiguration | Where-Object {$_.KeepCallDetailForDays -lt 30} | Remove-CsCdrConfiguration

## 詳細描述

通話詳細記錄 (CDR) 讓您能夠追蹤 Lync Server 功能的使用狀況，這些功能包括 Voice over Internet Protocol (VoIP) 通話、立即訊息、檔案傳輸、音訊/視訊 (A/V) 會議，以及應用程式分享工作階段。CDR (只有在您有部署監視服務時才能使用) 會保留使用狀況資訊：CDR 會記錄通話方、通話長度、是否傳輸任何檔案等資訊 (但 CDR 不會記錄通話本身)。

CDR 也會追蹤通話錯誤資訊：點對點工作階段與會議電話的詳細診斷資料。

做為系統管理員，您可以決定是否要在組織中使用 CDR。如果已部署監視服務，您便可以很輕鬆的啟用或停用 CDR。此外，您還可以依全域 (在整個組織啟用或停用 CDR) 或個別網站的基礎來進行此決策；例如，您可以在 Redmond 網站使用 CDR，但在 Paris 網站不使用 CDR。

使用 **New-CsCdrConfiguration** Cmdlet 建立的網站特定設定，之後可使用 **Remove-CsCdrConfiguration** Cmdlet 來移除。當您移除網站特定的設定時，受到影響之網站的 CDR 會自動由全域 CDR 組態設定來管理。

您也可以針對全域 CDR 設定執行 **Remove-CsCdrConfiguration** Cmdlet。然而，由於全域設定無法移除，因此這些設定將重設為預設值。例如，假設您將全域設定中的 KeepCallDetailForDays 屬性值設為 90。如果您針對全域設定執行 **Remove-CsCdrConfiguration** Cmdlet，則該屬性將重設為預設值 60。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsCdrConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsCdrConfiguration"}

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
<td><p>要移除的 CDR 組態設定的唯一識別碼。若要「移除」全域設定，請使用下列語法：-Identity global。(請再次注意，您無法真正移除全域設定，您所能做的只有將屬性重設回預設值)。若要將設定從網站範圍移除，請使用如下語法：-Identity site:Redmond。您無法在指定 Identity 時使用萬用字元。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CdrSettings。**Remove-CsCdrConfiguration** Cmdlet 接受管線傳送的 CDR 組態物件輸入。

## 傳回類型

無。反之，此 Cmdlet 會刪除 Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CdrSettings 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsCdrConfiguration](get-cscdrconfiguration.md)  
[New-CsCdrConfiguration](new-cscdrconfiguration.md)  
[Set-CsCdrConfiguration](set-cscdrconfiguration.md)

