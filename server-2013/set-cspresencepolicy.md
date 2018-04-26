---
title: Set-CsPresencePolicy
TOCTitle: Set-CsPresencePolicy
ms:assetid: 2d1f157b-d35d-402b-904d-281c013d2c30
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425782(v=OCS.15)
ms:contentKeyID: 49290456
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPresencePolicy

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的目前狀態原則。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsPresencePolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsPresencePolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-MaxCategorySubscription <UInt16>] [-MaxPromptedSubscriber <UInt16>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會修改個別使用者目前狀態原則 RedmondPresencePolicy。在此範例中，MaxPromptedSubscriber 屬性的值設為 300。

    Set-CsPresencePolicy -Identity "RedmondPresencePolicy" -MaxPromptedSubscriber 300

## 範例 2

範例 2 所示的命令是範例 1 中使用的命令變化；但此範例會針對設定為在組織中使用的所有目前狀態原則，將 MaxPromptedSubscriber 屬性設為 300。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsPresencePolicy** Cmdlet，這樣會傳回設定供組織使用之所有目前狀態原則的集合。然後，此集合會管線傳送到 **Set-CsPresencePolicy** Cmdlet，以將集合中每個原則的 MaxPromptedSubscriber 值變更為 300。

    Get-CsPresencePolicy | Set-CsPresencePolicy -MaxPromptedSubscriber 300

## 範例 3

範例 3 會示範如何設定組織中的目前狀態原則，以確保沒有原則允許 300 個以上的已提示訂閱者。為了執行此工作，此命令會先呼叫不含任何參數的 **Get-CsPresencePolicy** Cmdlet，以傳回組織中所有目前狀態原則的集合。然後再將集合管線傳送到 **Where-Object** Cmdlet，這會只挑出 MaxPromptedSubscriber 原則值大於 300 的原則。接著將篩選後的集合管線傳送到 **Set-CsPresencePolicy** Cmdlet，以取得集合中的每個原則，將提示的訂閱者數目上限設為 300。因此，不會有原則允許多於 300 個已提示的訂閱者，但會有些原則可能會允許少於 300 個訂閱者。

    Get-CsPresencePolicy | Where-Object {$_.MaxPromptedSubscriber -gt 300} | Set-CsPresencePolicy -MaxPromptedSubscriber 300

## 詳細描述

目前狀態資訊十分有價值，它可讓您知道連絡人是否可參與立即訊息交談。但同時，使用目前狀態資訊也是有代價的：目前狀態訂閱的愈多，則必須有更多專供更新目前狀態資訊使用的網路頻寬。如果您擔心網路頻寬的問題，可以限制每個人的目前狀態訂閱數。

**CsPresencePolicy** Cmdlet 可讓您管理目前狀態訂閱兩個重要的層面：已提示訂閱者與類別目錄訂閱。在將您新增到另一個人的 Lync 連絡人清單後，為您設定的預設行為是會收到快顯通知來告知已將您新增到該清單中。一直到您將顯示的對話方塊關閉後，每個通知才能算作已提示訂閱者。目前狀態原則的 MaxPromptedSubscriber 屬性可讓您指定使用者可擁有的未解決通知對話方塊數目上限(如果使用者到達上限，就不會再收到新的連絡人通知 - 至少在某些對話方塊已解決前不會)。

類別目錄訂閱代表要求特定的資訊目錄，例如要求行事曆資訊的應用程式。MaxCategorySubscription 屬性可讓您設定使用者可擁有的類別目錄訂閱數限制。

Lync Server 之前版本的已提示訂閱者與類別目錄訂閱是全域管理的。透過 **CsPresencePolicy** Cmdlet，您現在可以在全域範圍、網站範圍，甚至是個別使用者範圍管理目前狀態訂閱。這可讓您控制頻寬的使用，同時確保使用者能夠存取工作所需的目前狀態資訊。

**Set-CsPresencePolicy** Cmdlet 可讓您修改設定為在組織中使用的任何目前狀態原則。修改目前狀態原則僅表示變更 MaxPromptedSubscriber 屬性和/或 MaxCategorySubscription 屬性的值。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsPresencePolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPresencePolicy"}

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
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可讓系統管理員提供隨附於目前狀態原則的其他文字。例如，Description 可包含被指派原則的使用者相關資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要修改之目前狀態原則的唯一識別碼。若要修改全域原則，請使用下列語法：-Identity global。若要修改網站範圍的原則，請使用類似下列的語法：-Identity &quot;site:Redmond&quot;。若要修改個別使用者原則，請使用類似下列的語法：-Identity &quot;RedmondPresencePolicy&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>顯示狀態原則物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="even">
<td><p><em>MaxCategorySubscription</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>任何時候可以同時具有的類別訂閱數上限。類別訂閱代表要求取得某類資訊；例如，應用程式要求行事曆資料。</p>
<p>MaxCategorySubscription 可以設為任何介於 0 與 3000 之間的整數值；預設值為 1000。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxPromptedSubscriber</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>任何時候使用者可以同時具有的升級訂閱者數上限。根據預設，每次您被新增至其他使用者的連絡人清單時，都會顯示一個通知對話方塊告知您此情況，並提供您將該人員新增至自己的連絡人清單或是封鎖該人員檢視您目前狀態的機會。在您採取動作並關閉對話方塊之前，每個通知都會被視為一個已提示的訂閱者。</p>
<p>MaxPromptedSubscriber 可以設為任何介於 0 與 600 (含) 之間的整數值；預設值為 200。如果您將此值設為 0，則使用者將不會在被其他人新增至連絡人清單時收到任何通知。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Presence.PresencePolicy 物件。**Set-CsPresencePolicy** Cmdlet 會接受目前狀態原則物件的管線傳送資料。

## 傳回類型

**Set-CsPresencePolicy** Cmdlet 不會傳回任何值或物件，而會修改現有的 Microsoft.Rtc.Management.WritableConfig.Policy.Presence.PresencePolicy 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsPresencePolicy](get-cspresencepolicy.md)  
[Grant-CsPresencePolicy](grant-cspresencepolicy.md)  
[New-CsPresencePolicy](new-cspresencepolicy.md)  
[Remove-CsPresencePolicy](remove-cspresencepolicy.md)

