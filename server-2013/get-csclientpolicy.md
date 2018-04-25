---
title: Get-CsClientPolicy
TOCTitle: Get-CsClientPolicy
ms:assetid: c8e1cb96-2bf7-447c-b41c-d896fe85e349
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398830(v=OCS.15)
ms:contentKeyID: 49292286
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsClientPolicy

 

_**上次修改主題的時間：** 2015-03-09_

傳回設定供組織使用之用戶端原則的資訊。除了在其他方面的功用之外，用戶端原則還能用來決定供使用者使用的 Lync 功能。例如，您可能會將傳輸檔案的權限授與某些使用者，然而卻拒絕將相同權限授與其他使用者。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsClientPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsClientPolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 會呼叫不含任何其他參數的 **Get-CsClientPolicy** Cmdlet，以傳回設定供組織使用之所有用戶端原則的集合。

    Get-CsClientPolicy

## 範例 2

範例 2 會使用 **Get-CsClientPolicy** Cmdlet，以傳回 Identity 為 SalesPolicy 的個別使用者用戶端原則。由於 Identity 是唯一的，因此此命令永遠只會傳回一個項目。

    Get-CsClientPolicy -Identity SalesPolicy

## 範例 3

範例 3 使用 Filter 參數來傳回所有在個別使用者範圍內設定的用戶端原則。篩選值 "tag:\*" 會指示 **Get-CsClientPolicy** Cmdlet 只傳回 Identity 開頭為字串值 "tag:" 的原則。

    Get-CsClientPolicy -Filter "tag:*"

## 範例 4

範例 4 會傳回所有 DisableSavingIM 屬性為 True 的用戶端原則集合。為達此目的，命令會先不使用任何參數而直接呼叫 **Get-CsClientPolicy** Cmdlet，以傳回設定供組織使用之所有用戶端原則的集合。然後再將該集合管線傳送到 **Where-Object** Cmdlet，以選取 DisableSavingIM 屬性等於 True 的原則。

    Get-CsClientPolicy | Where-Object {$_.DisableSavingIM -eq $True}

## 範例 5

在範例 5 中，只會傳回滿足下列兩個準則的用戶端原則：DisableSavingIM 屬性必須為 True 且 EnableIMAutoArchiving 屬性必須為 False。為達此目的，命令會先呼叫 **Get-CsClientPolicy** Cmdlet，以傳回設定供組織使用之所有用戶端原則的集合。然後再將該集合管線傳送到 **Where-Object** Cmdlet，以選取同時符合下列準則的原則：DisableSavingIM 必須等於 True 且 EnableIMAutoArchiving 必須等於 False。-and 運算子會指示 **Where-Object** Cmdlet 只選取符合所有指定準則的物件。

    Get-CsClientPolicy | Where-Object {$_.DisableSavingIM -eq $True -and $_.EnableIMAutoArchiving -eq $False}

## 範例 6

範例 6 是範例 5 所示命令的變化。但在此範例中，只要符合下列至少一項準則的原則，即會加以選取：DisableSavingIM 內容為 True 和/或 EnableIMAutoArchiving 內容為 False。為達此目的，命令會先呼叫 **Get-CsClientPolicy** Cmdlet，以傳回設定供組織使用之所有用戶端原則的集合。然後再將該集合管線傳送到 **Where-Object** Cmdlet，以選取至少符合下列其中一項準則的原則：DisableSavingIM 等於 True 和/或 EnableIMAutoArchiving 等於 False。-or 運算子會要求 **Where-Object** Cmdlet 選取所有至少符合一項指定條件的物件。

## 詳細描述

在 Lync Server 中，用戶端原則取代了舊版產品中所使用的「群組原則」設定。在 Microsoft Office Communicator 2007 和 Microsoft Office Communicator 2007 R2 中，可使用「群組原則」協助決定使用者可以用 Communicator 及其他用戶端做些什麼；例如，「群組原則」設定決定使用者是否可以儲存其立即訊息交談的記錄、來自 Microsoft Outlook 的資訊是否整合到他們的目前狀態資訊，以及使用者是否可以在立即訊息中加入表情或格式化文字。

儘管「群組原則」如此有用，它在技術上仍有限制，尤其是在套用到 Lync Server 時。首先，「群組原則」的設計是根據個別網域或個別組織單位 (OU) 而套用原則；這使得它很難將原則套用到更精確選取的使用者群組 (例如，在特定部門工作的所有使用者，或是所有有特定工作職稱的使用者)。另一方面，\[群組原則\] 只會套用到登入網域的使用者，以及使用電腦登入的使用者；\[群組原則\] 不會套用到透過網際網路或使用行動電話存取系統的使用者。這就表示，同一名使用者隨著登入裝置以及登入位置的不同，就會有不同的使用經驗。

為了解決這些不一致的問題，Lync Server 用戶端原則會在使用者每一次存取系統時套用，不管使用者從何處登入以及使用何種裝置登入。此外，用戶端原則 (如同其他 Lync Server 原則) 很容易便可套用到選取的使用者群組。您甚至可以建立指派給單一使用者的自訂原則。

用戶端原則可在全域、網站和個別使用者範圍設定。 **Get-CsClientPolicy** Cmdlet 可讓您傳回設定供組織使用之所有用戶端原則的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsClientPolicy** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsClientPolicy"}

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
<td><p>可讓您在指定要傳回的原則時使用萬用字元。例如，若要傳回所有在網站範圍內設定的原則，請使用下列語法：-Filter &quot;site:*&quot;。若要傳回所有個別使用者原則的集合，請使用下列語法：-Filter &quot;tag:*&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要傳回之用戶端原則的唯一識別碼。若要參考全域原則，請使用下列語法：-Identity global。若要參考網站原則，請使用類似下列的語法：-Identity site:Redmond。若要參考個別使用者原則，請使用類似下列的語法：-Identity SalesDepartmentPolicy。</p>
<p>若省略此參數，將會傳回設定供組織使用的所有用戶端原則。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區 本機複本擷取用戶端原則資料，而不從 中央管理存放區 本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsClientPolicy** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsClientPolicy** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Policy.Client.ClientPolicy 物件的執行個體。

## 請參閱

#### 其他資源

[Grant-CsClientPolicy](grant-csclientpolicy.md)  
[New-CsClientPolicy](new-csclientpolicy.md)  
[Remove-CsClientPolicy](remove-csclientpolicy.md)  
[Set-CsClientPolicy](set-csclientpolicy.md)

