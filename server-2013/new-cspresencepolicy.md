---
title: New-CsPresencePolicy
TOCTitle: New-CsPresencePolicy
ms:assetid: a0b54f25-db48-4797-8f0e-0e826830217c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412747(v=OCS.15)
ms:contentKeyID: 49291840
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPresencePolicy

 

_**上次修改主題的時間：** 2015-03-09_

在網站範圍或個別使用者範圍建立新的目前狀態原則。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsPresencePolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-MaxCategorySubscription <UInt16>] [-MaxPromptedSubscriber <UInt16>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會建立其 Identity 為 RedmondPresencePolicy 的新個別使用者目前狀態原則。在此範例中，MaxPromptedSubscriber 屬性值會設為 400，而 MaxCategorySubscription 屬性值會設為 500。

    New-CsPresencePolicy -Identity "RedmondPresencePolicy" -MaxPromptedSubscriber 400 -MaxCategorySubscription 500

## 範例 2

在範例 2 中，新的個別使用者目前狀態原則一開始會建立在記憶體中，稍後才會轉換為實際的目前狀態原則。為達此目的，此範例中的第一個命令會建立 Identity 為 RedmondPresencePolicy 的目前狀態原則，並將此原則儲存於名為 $x 的變數中。InMemory 參數可確保原則只會建立在記憶體中，而不會立即新增至 Lync Server。

命令 2 和命令 3 會接著被用來設定虛擬原則的 MaxPromptedSubscriber 和 MaxCategorySubscription 屬性。在設定原則值之後，第 4 行使用 **Set-CsPresencePolicy** Cmdlet 和 Instance 參數來根據 $x 中儲存的資訊，建立實際的目前狀態原則。最後這一個步驟很重要：如果您未呼叫 **Set-CsPresencePolicy** Cmdlet，則原則只會存在記憶體中，只要您結束 Windows PowerShell 工作階段或刪除變數 $x，此原則就會消失不見。

    $x = New-CsPresencePolicy -Identity "RedmondPresencePolicy" -InMemory
    $x.MaxPromptedSubscriber = 400
    $x.MaxCategorySubscription = 500
    Set-CsPresencePolicy -Instance $x

## 詳細描述

目前狀態資訊十分有價值，它可讓您知道連絡人是否可參與立即訊息交談。但同時，使用目前狀態資訊也是有代價的：目前狀態訂閱的愈多，則必須有更多專供更新目前狀態資訊使用的網路頻寬。如果您擔心網路頻寬的問題，可以限制每個人的目前狀態訂閱數。

**CsPresencePolicy** Cmdlet 可讓您管理目前狀態訂閱兩個重要的層面：已提示訂閱者與類別目錄訂閱。在將您新增到另一個人的 Lync 連絡人清單後，為您設定的預設行為是會收到快顯通知來告知已將您新增到該清單中。一直到您將顯示的對話方塊關閉後，每個通知才能算作已提示訂閱者。目前狀態原則的 MaxPromptedSubscriber 屬性可讓您指定使用者可擁有的未解決通知對話方塊數目上限(如果使用者到達上限，就不會再收到新的連絡人通知 - 至少在某些對話方塊已解決前不會)。

類別目錄訂閱代表要求特定的資訊目錄，例如要求行事曆資訊的應用程式。MaxCategorySubscription 屬性可讓您設定使用者可擁有的類別目錄訂閱數限制。

Lync Server 之前版本的已提示訂閱者與類別目錄訂閱是全域管理的。透過 **CsPresencePolicy** Cmdlet，您可以在全域範圍、網站範圍，甚至是個別使用者範圍管理這些目前狀態訂閱。這可讓您控制頻寬的使用，同時確保使用者能夠存取工作所需的目前狀態資訊。

**New-CsPresencePolicy** Cmdlet 提供一種方法，可讓您在網站範圍或個別使用者範圍建立自訂目前狀態原則。在網站範圍建立的原則會自動套用至該網站；在個別使用者範圍建立的原則就必須藉由執行 **Grant-CsPresencePolicy** Cmdlet 來指派給使用者。請注意，您既無法在全域範圍建立新的目前狀態原則，也無法在個別網站建立第二個目前狀態原則 (例如，Redmond 網站只能裝載一個目前狀態原則)。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsPresencePolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsPresencePolicy"}

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
<td><p>新目前狀態原則的唯一識別碼。若要建立新的個別使用者原則，請使用下列語法：-Identity &quot;RedmondPresencePolicy&quot;。若要在網站範圍建立新的原則，請使用下列語法：-Identity &quot;site:Redmond&quot;。</p>
<p>請注意，您無法在全域範圍建立新的目前狀態原則。此外，如果有問題的網站已裝載目前狀態原則，或如果您嘗試使用現有個別使用者原則的 Identity，則您的命令也將失敗。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可讓系統管理員提供隨附於目前狀態原則的其他文字。例如，Description 可包含被指派原則的使用者相關資訊。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
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
<td><p>任何時候使用者可以同時具有的升級訂閱者數上限。根據預設，每次您被新增至其他使用者的連絡人清單時，畫面上都會顯示一個通知對話方塊告知您此情況，並提供您將該人員新增至自己的連絡人清單或是封鎖該人員檢視您目前狀態的機會。除非您採取動作並關閉對話方塊，否則每個通知都會算作一個提示的訂閱者。</p>
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

無。**New-CsPresencePolicy** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsPresencePolicy** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Policy.Presence.PresencePolicy 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsPresencePolicy](get-cspresencepolicy.md)  
[Grant-CsPresencePolicy](grant-cspresencepolicy.md)  
[Remove-CsPresencePolicy](remove-cspresencepolicy.md)  
[Set-CsPresencePolicy](set-cspresencepolicy.md)

