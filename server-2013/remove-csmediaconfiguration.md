---
title: Remove-CsMediaConfiguration
TOCTitle: Remove-CsMediaConfiguration
ms:assetid: 8af2b8cb-4d58-4f8a-9acb-9b5104880bc9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398705(v=OCS.15)
ms:contentKeyID: 49291601
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsMediaConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除指定的媒體組態設定集合。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsMediaConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 使用 **Remove-CsMediaConfiguration** Cmdlet 刪除 Identity 為 site:Redmond1 的媒體組態集合。從網站範圍中移除媒體設定時，該網站會自動開始使用全域媒體設定。

    Remove-CsMediaConfiguration -Identity site:Redmond1

## 範例 2

範例 2 使用 **Get-CsMediaConfiguration** Cmdlet、**Where-Object** Cmdlet 和 **Remove-CsMediaConfiguration** Cmdlet 三個 Cmdlet，以移除參與交談的各方都需要加密的所有媒體組態集合。為達成此目的，會先使用 **Get-CsMediaConfiguration** Cmdlet 以傳回組織中的所有媒體組態集合。然後再將該資訊管線傳送到 **Where-Object** Cmdlet，以套用篩選將管線資料限制在 EncryptionLevel 屬性等於 (-eq) RequireEncryption 的集合。最後，會將篩選後的資料集傳遞到 **Remove-CsMediaConfiguration** Cmdlet，以刪除資料集中的每個項目。

    Get-CsMediaConfiguration | Where-Object {$_.EncryptionLevel -eq "RequireEncryption"} | Remove-CsMediaConfiguration

## 範例 3

此範例會移除在服務範圍定義的所有媒體組態 (亦即套用至特定服務的組態)。作法是先呼叫 **Get-CsMediaConfiguration** Cmdlet 並使用 Filter service:\* 。此篩選會擷取 Identity 開頭為 service 的所有媒體組態集合，亦即在服務範圍的所有集合。然後再將該集合組管線傳送到 **Remove-CsMediaConfiguration** Cmdlet，以移除所有集合。

    Get-CsMediaConfiguration -Filter service:* | Remove-CsMediaConfiguration

## 詳細描述

此 Cmdlet 會移除媒體設定的集合。這些設定與用戶端端點間的音訊和視訊通話有關。

此 Cmdlet 也用來移除全域媒體設定。但在此情況下，不會實際移除設定；而只是重設為其預設值。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsMediaConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsMediaConfiguration"}

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
<td><p>您要移除之媒體組態設定的唯一識別碼。此識別碼會指定套用此組態的範圍 (全域、網站或服務)。</p></td>
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
<td><p>隱藏變更前所顯示的確認提示。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.Media.MediaSettings 物件。接受媒體組態物件的管線傳送資料。

## 傳回類型

移除 Microsoft.Rtc.Management.WritableConfig.Settings.Media.MediaSettings 類型的物件。

## 請參閱

#### 其他資源

[New-CsMediaConfiguration](new-csmediaconfiguration.md)  
[Set-CsMediaConfiguration](set-csmediaconfiguration.md)  
[Get-CsMediaConfiguration](get-csmediaconfiguration.md)

