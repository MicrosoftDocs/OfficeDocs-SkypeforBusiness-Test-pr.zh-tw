---
title: New-CsPersistentChatConfiguration
TOCTitle: New-CsPersistentChatConfiguration
ms:assetid: df83eebe-c20c-4e22-a5d4-1546a7f06e25
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205330(v=OCS.15)
ms:contentKeyID: 49292564
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPersistentChatConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

在網站範圍或服務範圍建立新的常設聊天室組態設定集合。常設聊天室組態設定可用於管理常設聊天室服務。例如，這些設定可讓您指定可加入聊天室的使用者人數上限。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    New-CsPersistentChatConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-DefaultChatHistory <Int16>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-MaxFileSizeKB <UInt32>] [-ParticipantUpdateLimit <UInt32>] [-RoomManagementUrl <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會建立套用至 Redmond 網站的一組新常設聊天室組態設定。在此範例中，ParticipantUpdateLimit 屬性設為 100。

    New-CsPersistentChatConfiguration -Identity "site:Redmond" -ParticipantUpdateLimit 100

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

常設聊天室服務有一部分是由常設聊天室組態設定所控制。這些設定可以指定當您登入聊天室時，所能立即見到在您登入前所張貼的聊天訊息數 (聊天歷程)，或是可以上傳到服務 (或從服務下載) 的檔案大小等等。這些設定可以在全域、網站或服範圍設定 (亦即您可以將自訂的設定集合指派到個別的常設聊天室集區)。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsPersistentChatConfiguration"}

**Lync Server 控制台：**若要使用 Lync Server 控制台 建立新的常設聊天室組態設定集合，請依序按一下 **\[常設聊天室\]**、**\[常設聊天室組態\]** 及 **\[新增\]**，然後按一下 **\[網站集合\]** 或 **\[集區組態\]**。

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
<td><p>要建立之新常設聊天室組態設定的唯一識別碼。新組態設定可在網站範圍或服務範圍 (僅限 Persistent Chat Server 服務) 建立。若要在網站範圍建立新的設定，請使用類似下列的語法：</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>若要在服務範圍建立新的設定，請使用類似下列的語法：</p>
<p>-Identity &quot;service:PersistentChatServer:atl-gc-001.litwarein.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>DefaultChatHistory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int16</p></td>
<td><p>聊天室立即可用的預設聊天訊息數目。請注意，此值只表示立即可用的訊息數目，而不會限制可擷取的訊息總數。</p>
<p>DefaultChatHistory 可設為介於 1 和 500 (含) 之間的任何值。預設值為 30。</p></td>
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
<td><p><em>MaxFileSizeKB</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>Web 服務可上傳或下載的檔案大小上限 (KB)。預設值為 20000 KB。</p></td>
</tr>
<tr class="odd">
<td><p><em>ParticipantUpdateLimit</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>可參與聊天室的使用者數目上限，超過此上限即會停用作用中參與者清單更新。預設值為 75。</p></td>
</tr>
<tr class="even">
<td><p><em>RoomManagementUrl</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>系統管理員可用來管理個別聊天室的網頁 URL。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsPersistentChatConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsPersistentChatConfiguration** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PersistentChatConfiguration 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsPersistentChatConfiguration](get-cspersistentchatconfiguration.md)  
[Remove-CsPersistentChatConfiguration](remove-cspersistentchatconfiguration.md)  
[Set-CsPersistentChatConfiguration](set-cspersistentchatconfiguration.md)

