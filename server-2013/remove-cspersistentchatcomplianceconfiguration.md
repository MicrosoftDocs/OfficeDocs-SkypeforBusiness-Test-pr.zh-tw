---
title: Remove-CsPersistentChatComplianceConfiguration
TOCTitle: Remove-CsPersistentChatComplianceConfiguration
ms:assetid: 2d54eabf-fbb5-435b-9a71-d6b03beb09a5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204767(v=OCS.15)
ms:contentKeyID: 49290448
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPersistentChatComplianceConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除現有的常設聊天室規範組態設定集合。常設聊天室規範可讓系統管理員維護常設聊天室項目及活動的封存，包括：新訊息、新事件 (例如，使用者進入或退出聊天室)、檔案上傳與下載，以及對聊天記錄執行的搜尋。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Remove-CsPersistentChatComplianceConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會移除套用至 Redmond 網站的常設聊天室規範組態設定。

    Remove-CsPersistentChatComplianceConfiguration -Identity "site:Redmond"

## 範例 2

在範例 2 中，會移除套用至網站範圍的所有常設聊天室規範組態設定。為達成此目的，命令會先使用 **Get-CsPersistentChatComplianceConfiguration** Cmdlet 和 Filter 參數擷取指派給網站範圍的所有設定 (作法是使用篩選值 "site:\*")。擷取網站範圍的設定之後，會將這些設定管線傳送到 **Remove-CsPersistentChatComplianceConfiguration** Cmdlet 加以移除。

    Get-CsPersistentChatComplianceConfiguration -Filter "site:*" | Remove-CsPersistentChatComplianceConfiguration

## 範例 3

範例 3 顯示如何移除 AddUserDetails 和 AddChatRoomDetails 屬性都設為 True 的所有常設聊天室規範組態設定。為了執行此工作，命令會先使用 **Get-CsPersistentChatComplianceConfiguration** Cmdlet 傳回所有常設聊天室規範組態設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 AddUserDetails 屬性和 AddChatRoomDetails 屬性等於 True ($True) 的設定。接著將篩選後的集合管線傳送到 **Remove-CsPersistentChatComplianceConfiguration** Cmdlet，以繼續刪除該經過篩選集合中每一個項目。

    Get-CsPersistentChatComplianceConfiguration | Where-Object {$_.AddUserDetals -eq $True -and $_.AddChatRoomDetails -eq $True} | Remove-CsPersistentChatComplianceConfiguration

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

許多組織 (包括醫療組織與金融組織) 都必須維護其所有電子通訊的封存，其中包括使用常設聊天室服務所進行的交談。Lync Server 2013 可讓您個別建立規範資料庫來保存常設聊天室中所有詳細資料的封存。常設聊天室規範可從網站範圍或服務範圍啟用或停用 (亦即可以針對特定的常設聊天室集區啟用或停用規範)。除此之外，只能使用 Windows PowerShell 命令列介面來管理常設聊天室規範。Lync Server 2013 控制台不提供任何可用來管理常設聊天室規範的功能。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPersistentChatComplianceConfiguration"}

**Lync Server 控制台：** **Remove-CsPersistentChatComplianceConfiguration** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p>要移除之常設聊天室規範設定的唯一識別碼。若要移除在網站範圍設定的設定集合，請使用類似下列的語法：</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>若要移除在服務範圍設定的集合，請使用下列語法：</p>
<p>-Identity &quot;service:PersistentChatServer:atl-gc-001.litwareinc.com&quot;</p>
<p>請注意，Identity 參數不可使用萬用字元。</p>
<p>您也可以對全域設定集合執行 <strong>Remove-CsPersistentChatComplianceConfiguration</strong> Cmdlet。不過，在該情況下，將不會移除全域集合，而是將該集合中的所有屬性重設為其預設值。</p></td>
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

**Remove-CsPersistentChatComplianceConfiguration** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PersistentChatComplianceConfiguration 物件執行個體。

## 傳回類型

無。反之，**Remove-CsPersistentChatComplianceConfiguration** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PersistentChatComplianceConfiguration 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsPersistentChatComplianceConfiguration](get-cspersistentchatcomplianceconfiguration.md)  
[New-CsPersistentChatComplianceConfiguration](new-cspersistentchatcomplianceconfiguration.md)  
[Set-CsPersistentChatComplianceConfiguration](set-cspersistentchatcomplianceconfiguration.md)

