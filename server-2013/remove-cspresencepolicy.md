---
title: Remove-CsPresencePolicy
TOCTitle: Remove-CsPresencePolicy
ms:assetid: ecdbfef8-2b7c-4bd7-bf01-7fb230eefe9f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399070(v=OCS.15)
ms:contentKeyID: 49292713
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPresencePolicy

 

_**上次修改主題的時間：** 2015-03-09_

移除指定的目前狀態原則。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsPresencePolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會刪除 Identity 為 RedmondPresencePolicy 的個別使用者目前狀態原則。

    Remove-CsPresencePolicy -Identity "RedmondPresencePolicy"

## 範例 2

範例 2 所示的命令會移除所有在個別使用者範圍中設定的目前狀態原則 (這些原則的 Identity 都會以前置詞 "tag:" 開頭)。為了執行此工作，命令會先使用 **Get-CsPresencePolicy** Cmdlet 搭配 Filter 參數，以傳回所有個別使用者目前狀態原則；篩選值 "tag:\*" 可將傳回的資料限制在 Identity 開頭為字串值 "tag:" 開頭的原則。然後再將篩選後的集合管線傳送到 **Remove-CsPresencePolicy** Cmdlet，這會刪除集合中的每個原則。

    Get-CsPresencePolicy -Filter "tag:*" | Remove-CsPresencePolicy

## 範例 3

範例 3 會刪除所有允許超過 500 位提示訂閱者的目前狀態原則。為達成此目的，命令會呼叫不含任何參數的 **Get-CsPresencePolicy** Cmdlet，以傳回設定供組織使用之所有目前狀態原則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這只會挑出 MaxPromptedSubscriber 屬性大於 500 的原則。接著將篩選後的集合管線傳送到 **Remove-CsPresencePolicy** Cmdlet，這會刪除所有允許超過 500 位提示訂閱者的目前狀態原則。

    Get-CsPresencePolicy | Where-Object {$_.MaxPromptedSubscriber -gt 500} | Remove-CsPresencePolicy

## 詳細描述

目前狀態資訊十分有價值，它可讓您知道連絡人是否可參與立即訊息交談。但同時，使用目前狀態資訊也是有代價的：目前狀態訂閱的愈多，則必須有更多專供更新目前狀態資訊使用的網路頻寬。如果您擔心網路頻寬的問題，可以限制每個人的目前狀態訂閱數。

**CsPresencePolicy** Cmdlet 可讓您管理目前狀態資訊兩個重要的層面：已提示訂閱者與類別目錄訂閱。在將您新增到另一個人的 Lync 連絡人清單後，為您設定的預設行為是會收到快顯通知來告知已將您新增到該清單中。一直到您將快顯方塊關閉後，每個通知才能計算為一個已提示訂戶。目前狀態原則的 MaxPromptedSubscriber 屬性可讓您指定使用者可擁有的未解決通知對話方塊數目上限(如果使用者到達上限，就不會再收到新的連絡人通知，至少在某些對話方塊已關閉前不會)。

類別目錄訂閱代表要求特定的資訊目錄，例如要求行事曆資訊的應用程式。MaxCategorySubscription 屬性可讓您設定使用者可擁有的類別目錄訂閱數限制。

Lync Server 之前版本的已提示訂閱者與類別目錄訂閱是全域管理的。透過 **CsPresencePolicy** Cmdlet，您現在可以在全域範圍、網站範圍，甚至是個別使用者範圍管理目前狀態訂閱。這可讓您控制頻寬的使用，同時確保使用者能夠存取工作所需的目前狀態資訊。

在網站範圍或個別使用者範圍內建立的原則，隨時都可藉由執行 **Remove-CsPresencePolicy** Cmdlet 來移除。此 Cmdlet 也可以根據全域原則來執行；但如果這麼做，並不會真的移除全域原則 ( Lync Server 不允許您移除全域原則)。而是將全域原則的兩個屬性 (MaxPromptedSubscriber 和 MaxCategorySubscription) 重設為預設值。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsPresencePolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPresencePolicy"}

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
<td><p>要移除之目前狀態原則的唯一識別碼。若要移除已設定於網站範圍內的原則，可使用類似下列的語法：-Identity &quot;site:Redmond&quot;。若要移除已設定於個別使用者範圍內的原則，請使用類似下列的語法：-Identity &quot;RedmondPresencePolicy&quot;。</p>
<p><strong>Remove-CsPresencePolicy</strong> Cmdlet 也可以根據全域原則來執行；若要執行這項操作，可使用下列語法：-Identity global。但是，請注意，系統不會移除全域原則。而是將該原則內的屬性重設為其預設值。</p></td>
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
<td><p>如果存在，將導致 <strong>Remove-CsPresencePolicy</strong> Cmdlet 刪除個別使用者原則，即使原則目前已指派給至少一位使用者也一樣。如果不存在，系統將要求您在移除仍在使用中的原則之前，先確認刪除要求。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Presence.PresencePolicy 物件。**Remove-CsPresencePolicy** Cmdlet 會接受目前狀態原則物件的管線傳送資料。

## 傳回類型

無。反之， **Remove-CsPresencePolicy** Cmdlet 會刪除 Microsoft.Rtc.Management.WritableConfig.Policy.Presence.PresencePolicy 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsPresencePolicy](get-cspresencepolicy.md)  
[Grant-CsPresencePolicy](grant-cspresencepolicy.md)  
[New-CsPresencePolicy](new-cspresencepolicy.md)  
[Set-CsPresencePolicy](set-cspresencepolicy.md)

