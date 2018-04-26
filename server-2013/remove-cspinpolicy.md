---
title: Remove-CsPinPolicy
TOCTitle: Remove-CsPinPolicy
ms:assetid: 60bebb77-4181-4c5c-9c0e-dd1ece71f1d2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398431(v=OCS.15)
ms:contentKeyID: 49291081
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPinPolicy

 

_**上次修改主題的時間：** 2015-03-09_

移除指定的個人識別碼 (PIN) 原則。PIN 驗證及 PIN 原則讓使用者在存取 Lync Server 時只需提供 PIN 而無須提供使用者名稱與密碼。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsPinPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會移除 Identity 為 RedmondUsersPinPolicy 的個別使用者 PIN 原則。

    Remove-CsPinPolicy -Identity RedmondUsersPinPolicy

## 範例 2

範例 2 所示的命令會移除在網站範圍設定的所有 PIN 原則。為達成此目的，命令會使用 **Get-CsPinPolicy** Cmdlet 並搭配 Filter 參數，以傳回 Identity 開頭為字元 "site:" 之所有原則的集合。然後，此集合會管線傳送到 **Remove-CsPinPolicy** Cmdlet，以刪除集合中的每個原則。

    Get-CsPinPolicy -Filter "site:*" | Remove-CsPinPolicy

## 範例 3

在範例 3 中， **Get-CsPinPolicy** Cmdlet、 **Where-Object** Cmdlet 以及 **Remove-CsPinPolicy** Cmdlet 是用來刪除 AllowCommonPatterns 屬性為 True 的所有 PIN 原則。為達成此目的，會先使用 **Get-CsPinPolicy** Cmdlet 傳回設定供組織使用之所有 PIN 原則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 AllowCommonPatterns 屬性等於 True 的原則。最後，將篩選後的集合管線傳送到 **Remove-CsPinPolicy** Cmdlet，以刪除集合中的每個原則。

    Get-CsPinPolicy | Where-Object {$_.AllowCommonPatterns -eq $True} | Remove-CsPinPolicy

## 範例 4

範例 4 所示的命令會刪除在個別使用者和網站範圍設定的所有 PIN 原則；作法是使用 **Get-CsPinPolicy** Cmdlet 傳回設定供組織使用之所有 PIN 原則的集合，然後將該整個集合以管線傳送到 **Remove-CsPinPolicy** Cmdlet。請注意全琙原則也會包含在此集合中。不過將不會刪除全琙原則，而是將全域原則中的所有屬性重設為預設值。

    Get-CsPinPolicy | Remove-CsPinPolicy

## 詳細描述

Lync Server 可讓使用者透過電話來連接系統或加入公用交換電話網路 (PSTN) 會議。一般說來，在登入系統或加入會議時，使用者必須輸入使用者名稱和密碼。然而很遺憾地，如果您使用的是沒有英數字元鍵盤的電話，輸入使用者名稱和密碼將會是一大難題。基於上述考量， Lync Server 可讓您將僅由數字組成的 PIN 提供給使用者。當出現提示時，使用者只要輸入 PIN 便能登入系統或加入會議，完全不需要使用者名稱和密碼。

Lync Server 使用 PIN 原則來管理 PIN 驗證屬性。例如，您可以指定 PIN 的長度下限，以及決定是否將允許使用「共同模式」(例如，連續數字) 的 PIN (例如，像是 123456 的 PIN)。除了您在安裝 Lync Server 時系統為您建立的全域 PIN 原則外，您可以建立套用至網站或個別使用者範圍的自訂 PIN 原則。

**Remove-CsPinPolicy** Cmdlet 可讓您移除已在網站範圍或個別使用者範圍設定的 PIN 原則。當您移除網站範圍原則或個別使用者原則時，將會刪除這些原則，而且無法再使用。此外，已指派這些原則的任何使用者將會自動繼承原則階層 (全域、網站、服務、個別使用者) 中的下一個原則。例如，如果您移除網站原則，則先前受該原則影響的所有使用者，其 PIN 原則將會由全域原則管理。

您還可以針對全域原則執行 **Remove-CsPinPolicy** Cmdlet。不過，在該情況下不會移除原則，因為您無法刪除全域原則。而是會將全域原則的所有屬性重設為預設值。例如，假設您已設定全域原則以使用最小 PIN 長度為 11 位數。如果您移除全域原則，PIN 長度下限將會重設為預設長度 5 位數。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsPinPolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPinPolicy"}

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
<td><p>建立原則時指派給原則的唯一識別碼。PIN 原則可以在全域、網站或個別使用者範圍指派。若要參考全域執行個體，請使用下列語法：-Identity global。若要參考網站範圍的原則，請使用以下的語法：-Identity site:Redmond。若要在每個使用者範圍上參考原則，請使用類似下列的語法：-Identity RedmondPINPolicy。</p>
<p></p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.UserPin.UserPolicy 物件。 **Remove-CsPinPolicy** Cmdlet 會接受 PIN 原則物件的管線傳送資料。

## 傳回類型

**Remove-CsPinPolicy** Cmdlet 不會傳回值或物件，而會移除 Microsoft.Rtc.Management.WritableConfig.Policy.UserPin.UserPolicy 物件的一或多個執行個體。

## 請參閱

#### 其他資源

[Get-CsPinPolicy](get-cspinpolicy.md)  
[Grant-CsPinPolicy](grant-cspinpolicy.md)  
[New-CsPinPolicy](new-cspinpolicy.md)  
[Set-CsPinPolicy](set-cspinpolicy.md)

