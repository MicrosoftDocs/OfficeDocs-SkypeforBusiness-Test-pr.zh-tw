---
title: Get-CsPresencePolicy
TOCTitle: Get-CsPresencePolicy
ms:assetid: 65880bdb-4482-4cfb-83de-19b239784fe5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398463(v=OCS.15)
ms:contentKeyID: 49291139
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPresencePolicy

 

_**上次修改主題的時間：** 2015-03-09_

傳回設定供組織使用之目前狀態原則的資訊。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsPresencePolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsPresencePolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回設定供組織使用之所有目前狀態原則的資訊。這是透過呼叫不含任何參數的 **Get-CsPresencePolicy** Cmdlet。

    Get-CsPresencePolicy

## 範例 2

範例 2 會傳回單一個別使用者目前狀態原則：Identity 為 RedmondPresencePolicy 的原則。

    Get-CsPresencePolicy -Identity "RedmondPresencePolicy"

## 範例 3

範例 3 會傳回所有已在網站範圍設定的目前狀態原則相關資訊。為達此目的，命令會使用 Filter 參數搭配篩選值 "site:\*" (此篩選值可將傳回的資料限制在 Identity 開頭為 "site:" 字串值的目前狀態原則)。

    Get-CsPresencePolicy -Filter "site:*"

## 範例 4

範例 4 會傳回所有將提示的訂閱者數上限限制在 100 或以下之目前狀態原則的資訊。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsPresencePolicy** Cmdlet，以傳回設定供組織使用之所有目前狀態原則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 MaxPromptedSubscriber 屬性小於或等於 100 的原則。

    Get-CsPresencePolicy | Where-Object {$_.MaxPromptedSubscriber -le 100}

## 詳細描述

目前狀態資訊十分有價值，它可讓您知道連絡人是否可參與立即訊息交談。但同時，使用目前狀態資訊也是有代價的：目前狀態訂閱的愈多，則必須有更多專供更新目前狀態資訊使用的網路頻寬。如果您擔心網路頻寬的問題，可以限制每個人的目前狀態訂閱數。

**CsPresencePolicy** Cmdlet 可讓您管理目前狀態訂閱兩個重要的層面：已提示訂閱者與類別目錄訂閱。在將您新增到另一個人的 Lync 連絡人清單後，為您設定的預設行為是會收到快顯通知來告知已將您新增到該清單中。一直到您將顯示的對話方塊關閉後，每個通知才能算作已提示訂閱者。目前狀態原則的 MaxPromptedSubscriber 屬性可讓您指定使用者可擁有的未解決通知對話方塊數目上限(如果使用者到達上限，就不會再收到新的連絡人通知 - 至少在某些對話方塊已解決前不會)。

類別目錄訂閱代表要求特定的資訊目錄，例如要求行事曆資訊的應用程式。MaxCategorySubscription 屬性可讓您設定使用者可擁有的類別目錄訂閱數限制。

Lync Server 之前版本的已提示訂閱者與類別目錄訂閱是全域管理的。透過 **CsPresencePolicy** Cmdlet，您現在可以在全域範圍、網站範圍，甚至是個別使用者範圍管理目前狀態訂閱。這可讓您控制頻寬的使用，同時確保使用者能夠存取工作所需的目前狀態資訊。

**Get-CsPresencePolicy** Cmdlet 提供一種方法，讓您能夠傳回設定供組織使用之所有目前狀態原則的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsPresencePolicy** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPresencePolicy"}

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
<td><p>System.Strkng</p></td>
<td><p>可讓您在指定要傳回的一或多個原則時使用萬用字元。例如，下列語法會傳回在網站範圍設定的所有目前狀態原則：-Filter &quot;site:*&quot;。</p>
<p>不能在同一個命令中同時使用 Filter 與 Identity 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要擷取之目前狀態原則的唯一識別碼。若要傳回全域原則，請使用下列語法：-Identity global。若要傳回在網站範圍設定的原則，請使用下列語法：-Identity &quot;site:Redmond&quot;。若要傳回在個別使用者範圍設定的原則，請使用下列語法：-Identity &quot;RedmondPresencePolicy&quot;。指定 Identity 時，您無法使用萬用字元。</p>
<p>如果 Identity 和 Filter 參數皆未指定，則 <strong>Get-CsPresencePolicy</strong> Cmdlet 會傳回設定供組織使用的所有目前狀態原則。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區本機複本擷取目前狀態原則資料，而不從 中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsPresencePolicy** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsPresencePolicy** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Policy.Presence.PresencePolicy 物件的執行個體。

## 請參閱

#### 其他資源

[Grant-CsPresencePolicy](grant-cspresencepolicy.md)  
[New-CsPresencePolicy](new-cspresencepolicy.md)  
[Remove-CsPresencePolicy](remove-cspresencepolicy.md)  
[Set-CsPresencePolicy](set-cspresencepolicy.md)

