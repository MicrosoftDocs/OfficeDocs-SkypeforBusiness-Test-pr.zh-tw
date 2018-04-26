---
title: Remove-CsClientPolicy
TOCTitle: Remove-CsClientPolicy
ms:assetid: 2beb1557-8397-493e-be87-910ce01ba8f5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425772(v=OCS.15)
ms:contentKeyID: 49290438
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsClientPolicy

 

_**上次修改主題的時間：** 2015-03-09_

移除現有的用戶端原則。除了在其他方面的功用之外，用戶端原則還能用來決定供使用者使用的 Lync 功能。例如，您可能會將傳輸檔案的權限授與某些使用者，卻拒絕將相同權限授與其他使用者。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsClientPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

在範例 1 中， **Remove-CsClientPolicy** Cmdlet 用來刪除 Identity 為 SalesPolicy 的用戶端原則。

    Remove-CsClientPolicy -Identity SalesPolicy

## 範例 2

在範例 2 中， **Get-CsClientPolicy** Cmdlet 和 **Remove-CsClientPolicy** Cmdlet 用來刪除已在個別使用者範圍設定的所有用戶端原則。此命令會使用 **Get-CsClientPolicy** Cmdlet 與 Filter 參數，傳回在個別使用者範圍內設定的所有用戶端原則集合；篩選值 "tag:\*" 會告知 **Get-CsClientPolicy** Cmdlet 將擷取的資料限制為具有開頭字串值 "tag:" 之 Identity 的用戶端原則。然後，篩選過的集合會管線傳送到 **Remove-CsClientPolicy** Cmdlet，以移除集合中的每個原則。

    Get-CsClientPolicy -Filter "tag:*" | Remove-CsClientPolicy

## 範例 3

範例 3 會刪除 EnableAppearOffline 屬性設為 True 的所有用戶端原則。為達成此目的，會先呼叫不含任何額外參數的 **Get-CsClientPolicy** Cmdlet，這樣會傳回設定供組織使用之所有用戶端原則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 EnableAppearOffline 屬性等於 True 的原則。接著將篩選後的集合管線傳送到 **Remove-CsClientPolicy** Cmdlet，以刪除集合中的每一個原則。

    Get-CsClientPolicy | Where-Object {$_.EnableAppearOffline -eq $True} | Remove-CsClientPolicy

## 詳細描述

在 Lync Server 中，用戶端原則取代了舊版產品中所使用的「群組原則」設定。在 Microsoft Office Communicator 2007 和 Microsoft Office Communicator 2007 R2 中，可使用「群組原則」協助決定使用者可以用 Communicator 及其他用戶端做些什麼；例如，「群組原則」設定決定使用者是否可以儲存其立即訊息交談的記錄、來自 Microsoft Outlook 的資訊是否整合到他們的目前狀態資訊，以及使用者是否可以在立即訊息中加入表情或格式化文字。

儘管「群組原則」如此有用，它在技術上仍有限制，尤其是在套用到 Lync Server 時。首先，「群組原則」的設計是根據個別網域或個別 OU 而套用原則；這使得它很難將原則套用到更精確選取的使用者群組 (例如，在特定部門工作的所有使用者，或是所有具特定工作職稱的使用者)。另一方面，「群組原則」只會套用到登入網域的使用者，以及使用電腦登入的使用者；「群組原則」不會套用到透過網際網路存取 Lync Server 的使用者，或使用行動電話存取系統的使用者。這就表示，同一名使用者隨著登入裝置以及登入位置的不同，就會有不同的使用經驗。

為了解決這些不一致的問題，Lync Server 使用用戶端管理原則而不是「群組原則」。用戶端原則會在使用者每一次存取系統時套用，不管使用者從何處登入以及使用何種裝置登入。此外，用戶端原則 (如同其他 Lync Server 原則) 很容易便可套用到選取的使用者群組。您甚至可以建立指派給單一使用者的自訂原則。

用戶端原則可以在全域、網站和個別使用者範圍設定。稍後可以使用 **Remove-CsClientPolicy** Cmdlet，刪除在網站範圍或個別使用者範圍內設定的原則。您也可以針對全域原則執行 **Remove-CsClientPolicy** Cmdlet。在該情況下，將不會移除全域原則，因為全域原則無法刪除。不過，全域原則中的所有屬性將會重設為其預設值。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsClientPolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsClientPolicy"}

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
<td><p>要移除之用戶端原則的唯一識別碼。若要「移除」全域原則，請使用下列語法：-Identity global。(請注意，無法實際移除全域原則。而是將該原則中的所有屬性重設為其預設值)。若要移除網站原則，請使用類似下列的語法：-Identity &quot;site:Redmond&quot;。若要移除個別使用者原則，請使用類似下列的語法：-Identity &quot;SalesDepartmentPolicy&quot;。在指定原則 Identity 時不能使用萬用字元。</p></td>
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
<td><p>如果此參數已經存在，即使原則目前已指派給至少一個使用者，也將會遭到自動移除。若未指定此參數，則 <strong>Remove-CsClientPolicy</strong> Cmdlet 就不會自動移除已指派給至少一個使用者的個別使用者原則。但是會顯示一個確認提示，詢問您是否確定要移除該原則。您必須回答是 (按下 Y 鍵)，命令才會繼續並移除該原則。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Client.ClientPolicy 物件。**Remove-CsClientPolicy** Cmdlet 接受管線傳送的用戶端原則物件執行個體。

## 傳回類型

**Remove-CsClientPolicy** Cmdlet 不會傳回值。而是 Cmdlet 會刪除 Microsoft.Rtc.Management.WritableConfig.Policy.Client.ClientPolicy 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsClientPolicy](get-csclientpolicy.md)  
[Grant-CsClientPolicy](grant-csclientpolicy.md)  
[New-CsClientPolicy](new-csclientpolicy.md)  
[Set-CsClientPolicy](set-csclientpolicy.md)

