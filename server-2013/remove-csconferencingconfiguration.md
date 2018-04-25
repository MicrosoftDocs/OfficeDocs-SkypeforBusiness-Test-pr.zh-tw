---
title: Remove-CsConferencingConfiguration
TOCTitle: Remove-CsConferencingConfiguration
ms:assetid: a3dff4b0-100b-46fa-9078-d3b0d4914d87
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412767(v=OCS.15)
ms:contentKeyID: 49291887
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsConferencingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除指定的會議組態設定集合。會議設定可指定會議內容與講義的大小上限、內容寬限期，以及支援之用戶端內部與外部下載的 URL 等事項。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsConferencingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會刪除已套用至 Redmond 網站的會議組態設定。刪除這類網站設定時，網站中的使用者會自動繼承全域會議組態設定中的設定。

    Remove-CsConferencingConfiguration -Identity site:Redmond

## 範例 2

範例 2 中的命令會刪除所有已套用至網站範圍的會議組態設定。為達成此目的，命令會先呼叫 **Get-CsConferencingConfiguration** Cmdlet 搭配 Filter 參數；篩選值 "site:" 可確保只會傳回 Identity 開頭為字元 "site:" 的設定。然後再將此篩選後的集合管線傳送到 **Remove-CsConferencingConfiguration** Cmdlet，以刪除集合中的每一個項目。

    Get-CsConferencingConfiguration -Filter site:* | Remove-CsConferencingConfiguration

## 範例 3

範例 3 會刪除所有其組織未設為 Litwareinc 的會議組態設定。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsConferencingConfiguration** Cmdlet，以傳回組織所使用之所有會議組態設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 Organization 屬性不等於 Litwareinc 的設定。最後將篩選後的集合管線傳送到 **Remove-CsConferencingConfiguration** Cmdlet，以刪除集合中的所有設定。

    Get-CsConferencingConfiguration | Where-Object {$_.Organization -ne "Litwareinc"} | Remove-CsConferencingConfiguration

## 詳細描述

對於會議而言，管理與系統管理會分別以兩組 Cmdlet 進行。如果您想要管理使用者能做與不能做的事情 (例如，使用者是否可以邀請匿名參與者加入會議、使用者是否可以在會議內進行應用程式共用、使用者是否可以在會議內傳輸檔案)，則需使用 **CsConferencingPolicy** Cmdlet。

除了使用者活動之外，系統管理員還需要管理 Web 會議服務。例如，系統管理員需要能夠執行一些動作，例如指定配置給單一會議的內容儲存量上限，以及指定自動刪除該會議內容之前的寬限期。他們也需要能夠指定諸如應用程式共用及檔案傳輸這類活動使用的連接埠。

後面的活動是使用 **CsConferencingConfiguration** Cmdlet 來管理的。這些 Cmdlet 可讓您管理實際伺服器本身。**CsConferencingConfiguration** Cmdlet (可以套用至全域、網站及服務範圍) 雖然不能用來指定使用者是否可在會議期間共用應用程式，但是可以在允許應用程式共用時，用來指出該活動應該使用哪些連接埠。同樣地，Cmdlet 也可讓您指定一些事項，例如儲存限制和期限，以及可供使用者用來取得會議說明及資源的內部與外部 URL 指標。

**Remove-CsConferencingConfiguration** Cmdlet 提供一種方法，可讓您刪除任何為了要在您組織中使用而建立的自訂會議組態設定集合。當您刪除設定集合時，任何先前受這些設定影響的伺服器，都會自動變成受到階層中 (服務 – 網站 – 範圍) 下一個集合的管轄。如果刪除的設定是在服務範圍套用，則伺服器將變成由網站設定管理。如果網站範圍中沒有任何設定，則伺服器將變成由全域設定管理。同樣地，如果您刪除網站範圍的設定，則先前受到這些網站設定管理的伺服器，將變成由全域設定管理。

請注意，您也可以對全域設定執行 **Remove-CsConferencingConfiguration** Cmdlet。但在此情況下，不會移除全域設定；因為 Lync Server 不容許您移除全域設定。而是會將全域集合內的所有屬性都重設為預設值。例如，如果您先前已將內容儲存值上限變更為 200 MB，則此屬性將還原為預設值 100 MB。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsConferencingConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsConferencingConfiguration"}

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
<td><p>要移除之會議組態設定集合的唯一識別碼。若要移除在此網站範圍設定的設定，請使用類似下列的語法：-Identity &quot;site:Redmond&quot;。若要移除在服務範圍設定的設定，請使用下列語法：-Identity &quot;service:ConferencingServer:atl-cs-001.litwareinc.com&quot;。</p>
<p>也可以對全域設定執行 <strong>Remove-CsConferencingConfiguration</strong> Cmdlet。但在此情況下，不會移除這些設定，而只是將所有屬性都重設為預設值。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConfSettings 物件。**Remove-CsConferencingConfiguration** Cmdlet 接受會議組態物件管線傳送的執行個體。

## 傳回類型

無。反之，**Remove-CsConferencingConfiguration** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConfSettings 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsConferencingConfiguration](get-csconferencingconfiguration.md)  
[New-CsConferencingConfiguration](new-csconferencingconfiguration.md)  
[Set-CsConferencingConfiguration](set-csconferencingconfiguration.md)

