---
title: Remove-CsUCPhoneConfiguration
TOCTitle: Remove-CsUCPhoneConfiguration
ms:assetid: 1b2d9601-3206-48d9-a846-4486b606aad0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398249(v=OCS.15)
ms:contentKeyID: 49290255
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsUCPhoneConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除指定的 Lync Phone Edition 組態設定集合。這些設定的內容包括了所需要的安全性模式，以及是否應在指定的閒置時間後自動鎖定電話等等。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsUCPhoneConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會移除 Redmond 網站的 UC 電話組態設定 (-Identity site:Redmond)。從網站範圍移除設定時，該網站中使用者的 UC 電話會由全域電話組態設定管理。

    Remove-CsUCPhoneConfiguration -Identity site:Redmond

## 範例 2

範例 2 會移除已經在網站範圍設定的所有 UC 電話設定。為達成此目的，命令會先使用 **Get-CsUCPhoneConfiguration** Cmdlet 搭配 Filter 參數傳回在網站範圍設定的所有設定；篩選值 "site:\*" 可將傳回的資料限制在 Identity 屬性 (唯一可用的篩選屬性) 開頭為字串值 "site:" 的設定。然後再將篩選後的集合管線傳送到 **Remove-CsUCPhoneConfiguration** Cmdlet，以刪除集合中的每一個項目。

    Get-CsUCPhoneConfiguration -Filter site:* | Remove-CsUCPhoneConfiguration

## 範例 3

範例 3 會移除不強制執行電話鎖定的所有 UC 電話設定。為了執行此工作，命令會先使用不含任何參數的 **Get-CsUCPhoneConfiguration** Cmdlet，以傳回組織中目前所使用之所有 UC 電話設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 EnforceLockProperty 等於 False 的設定。接著將篩選後的集合管線傳送到 **Remove-CsUCPhoneConfiguration** Cmdlet，以移除集合中的每一個項目。

    Get-CsUCPhoneConfiguration | Where-Object {$_.EnforcePhoneLock -eq $False} | Remove-CsUCPhoneConfiguration

## 範例 4

範例 4 會刪除 SIP 安全性模式設為 Low 或 Medium 的所有 UC 電話組態設定。為達成此目的，會先呼叫 **Get-CsUCPhoneConfiguration** Cmdlet 以傳回設定供組織使用之所有 UC 電話設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 SIPSecurityMode 屬性設為 Low 或 Medium 的設定；作法是選取 SIPSecurityMode 不等於 High 的設定 (SIPSecurityMode 有三種可能的值：Low、Medium 以及 High)。接著將篩選後的集合管線傳送到 **Remove-CsUCPhoneConfiguration** Cmdlet，以刪除 SIPSecurityMode 不等於 High 的所有設定。

    Get-CsUCPhoneConfiguration | Where-Object {$_.SIPSecurityMode -ne "High"} | Remove-CsUCPhoneConfiguration

## 詳細描述

Lync Phone Edition 代表電話與 Lync Server 合併。Lync Phone Edition 會使用功能如同 Voice over Internet Protocol (VoIP) 電話的特殊硬體 (亦即與 Lync 相容的電話)。此外，此硬體也會充當類似 Lync 的端點：您可以設定目前的狀態、檢查 Lync 連絡人的狀態、搜尋新的連絡人，並執行許多其他您過去使用 Lync 執行的作業。

Lync Server 隨附許多 Cmdlet 可供您管理執行 Lync Phone Edition 的電話，例如您可以控制登入電話所使用的個人識別碼 (PIN) 長度下限，以及電話在未使用一段時間後是否會自動自行鎖住。

整合通訊 (UC) 電話組態設定可套用於全域範圍或網站範圍 (在網站範圍套用的設定優先於在全域範圍套用的設定)。當您首次安裝 Lync Server 時，會在全域範圍建立與套用單一的 UC 電話組態設定集。不過，在此之後，您隨時都可以使用 **New-CsUCPhoneConfiguration** Cmdlet 來建立在網站範圍套用的設定集合。這可讓您量身打造 UC 電話管理，以符合每個個別網站的獨特需求。

使用 **New-CsUCPhoneConfiguration** Cmdlet 建立的設定，稍後可以使用 **Remove-CsUCPhoneConfiguration** Cmdlet 加以移除。當您從網站移除設定時，該網站中執行 Lync Phone Edition 的電話並不會變成無人管理，而是自動由全域設定管轄。

您也可以針對全域設定執行 **Remove-CsUCPhoneConfiguration** Cmdlet。但是，這樣做實際上並不會移除全域設定：您無法移除全域 UC 電話設定，而是將全域設定中的屬性重設為其預設值。例如，如果您已經將電話鎖定時間間隔變更為 30 分鐘，「移除」全域設定會將間隔重設為預設值 10 分鐘。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsUCPhoneConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsUCPhoneConfiguration"}

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
<td><p>要移除之 UC 電話組態設定集合的唯一識別碼。若要移除網站集合，請使用類似下列的語法：-Identity &quot;site:Redmond&quot;。若要移除 (重設) 全域集合，請使用下列語法：-Identity global。請注意，指定原則 Identity 時，無法使用萬用字元。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.UcPhoneSettings 物件。**Remove-CsUCPhoneConfiguration** Cmdlet 接受管線傳送的 UC 電話設定物件執行個體。

## 傳回類型

無。反之，此 Cmdlet 會移除 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.UcPhoneSettings 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsUCPhoneConfiguration](get-csucphoneconfiguration.md)  
[New-CsUCPhoneConfiguration](new-csucphoneconfiguration.md)  
[Set-CsUCPhoneConfiguration](set-csucphoneconfiguration.md)

