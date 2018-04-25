---
title: Remove-CsPersistentChatConfiguration
TOCTitle: Remove-CsPersistentChatConfiguration
ms:assetid: 5b71b66b-9b9b-4833-94b8-528260cd7589
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204927(v=OCS.15)
ms:contentKeyID: 49291032
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPersistentChatConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除現有的常設聊天室組態設定集合。常設聊天室組態設定可用於管理常設聊天室服務。例如，這些設定可讓您指定可加入聊天室的使用者人數上限。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Remove-CsPersistentChatConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會刪除 Redmond 網站的常設聊天室組態設定。

    Remove-CsPersistentChatConfiguration -Identity "site:Redmond"

## 範例 2

範例 2 會移除套用至網站範圍的所有常設聊天室組態設定。為達成此目的，命令會先使用 **Get-CsPersistentChatConfiguration** Cmdlet 並搭配 –Filter 參數；篩選值 "site:\*" 可將傳回的資料限制在網站範圍所套用的設定。然後再將這些設定管線傳送到 **Remove-CsPersistentChatConfiguration** Cmdlet，以刪除套用至網站範圍的所有設定。

    Get-CsPersistentChatConfiguration -Filter "site:*" | Remove-CsPersistentChatConfiguration

## 範例 3

範例 3 會刪除預設聊天記錄大於 30 的所有常設聊天室組態設定。為了執行此工作，命令會先使用 **Get-CsPersistentChatConfiguration** Cmdlet 傳回所有常設聊天室組態設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 DefaultChatHistory 屬性大於 (-gt) 30 的設定。接著將篩選後的集合管線傳送到 **Remove-CsPersistentChatConfiguration** Cmdlet，以刪除篩選後之集合中的每個項目。

    Get-CsPersistentChatConfiguration | Where-Object {$_.DefaultChatHistory -gt 30} | Remove-CsPersistentChatConfiguration

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

常設聊天室服務有一部分是由常設聊天室組態設定所控制。這些設定可以指定當您登入聊天室時，所能立即見到在您登入前所張貼的聊天訊息數 (聊天歷程)，或是可以上傳到服務 (或從服務下載) 的檔案大小等等。這些設定可以在全域、網站或服範圍設定 (亦即您可以將自訂的設定集合指派到個別的常設聊天室集區)。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPersistentChatConfiguration"}

**Lync Server 控制台：**若要使用 Lync Server 控制台 移除常設聊天室組態設定的集合，請按一下 **\[常設聊天室\]**，然後再按一下 **\[常設聊天室組態\]**。選取所要移除的集合，再按一下 **\[編輯\]**，然後按一下 **\[刪除\]**。

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
<td><p>要移除之常設聊天室組態設定的唯一識別碼。若要移除在網站範圍設定的設定集合，請使用類似下列的語法：</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>若要移除在服務範圍設定的集合，請使用下列語法：</p>
<p>-Identity &quot;service:PersistentChatServer:atl-gc-001.litwareinc.com&quot;</p>
<p>請注意，Identity 參數不可使用萬用字元。</p>
<p>您也可以對全域設定集合執行 <strong>Remove-CsPersistentChatConfiguration</strong> Cmdlet。不過，在該情況下，將不會移除全域集合，而是將該集合中的所有屬性重設為其預設值。</p></td>
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

**Remove-CsPersistentChatConfiguration** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PersistentChatConfiguration 物件執行個體。

## 傳回類型

無。反之， **Remove-CsPersistentChatConfiguration** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PersistentChatConfiguration 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsPersistentChatConfiguration](get-cspersistentchatconfiguration.md)  
[New-CsPersistentChatConfiguration](new-cspersistentchatconfiguration.md)  
[Set-CsPersistentChatConfiguration](set-cspersistentchatconfiguration.md)

