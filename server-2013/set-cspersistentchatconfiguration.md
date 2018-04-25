---
title: Set-CsPersistentChatConfiguration
TOCTitle: Set-CsPersistentChatConfiguration
ms:assetid: 97d23d2e-878c-4573-bfce-0ddddc5a190e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205122(v=OCS.15)
ms:contentKeyID: 49291737
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPersistentChatConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的常設聊天室組態設定集合。常設聊天室組態設定可用於管理常設聊天室服務。例如，這些設定可讓您指定可加入聊天室的使用者人數上限。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Set-CsPersistentChatConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsPersistentChatConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-DefaultChatHistory <Int16>] [-Force <SwitchParameter>] [-MaxFileSizeKB <UInt32>] [-ParticipantUpdateLimit <UInt32>] [-RoomManagementUrl <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將全域常設聊天室組態設定的 DefaultChatHistory 屬性設為 100。

    Set-CsPersistentChatConfiguration -Identity "global" -DefaultChatHistory 100

## 範例 2

範例 2 會將所有常設聊天室組態設定的 DefaultChatHistory 屬性設為 100。為了執行此工作，命令會先使用 **Get-CsPersistentChatConfiguration** Cmdlet，以傳回組織中所有常設聊天室組態設定的集合。然後，此集合會管線傳送到 **Set-CsPersistentChatConfiguration** Cmdlet，以修改集合中所有項目的 DefaultChatHistory 屬性。

    Get-CsPersistentChatConfiguration | Set-CsPersistentChatConfiguration -DefaultChatHistory 100

## 範例 3

範例 3 顯示如何針對套用至網站範圍的所有常設聊天室組態設定，修改 DefaultChatHistory 屬性。為達成此目的，命令會先呼叫 **Get-CsPersistentChatConfiguration** Cmdlet 並搭配 Filter 參數；參數值 "site:\*" 可將傳回的資料限制在網站範圍設定的設定集合。然後再將這些設定管線傳送到 **Set-CsPersistentChatConfiguration** Cmdlet，以將每個設定集合的 DefaultChatHistory 屬性變更為 100。

    Get-CsPersistentChatConfiguration -Filter "site:*" | Set-CsPersistentChatConfiguration -DefaultChatHistory 100

## 範例 4

範例 4 會修改預設聊天記錄目前大於 100 之常設聊天室組態設定集合的 DefaultChatHistory 屬性。為了執行此工作，命令會先使用 **Get-CsPersistentChatConfiguration** Cmdlet，以傳回組織所使用之所有常設聊天室組態設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 DefaultChatHistory 屬性大於 (-gt) 100 的設定。接著將篩選後的集合管線傳送到 **Set-CsPersistentChatConfiguration** Cmdlet，以將篩選後集合中每個項目之 DefaultChatHistory 屬性的值設為 100。

    Get-CsPersistentChatConfiguration | Where-Object {$_.DefaultChatHistory -gt 100} | Set-CsPersistentChatConfiguration -DefaultChatHistory 100

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

常設聊天室服務有一部分是由常設聊天室組態設定所控制。這些設定可以指定當您登入聊天室時，所能立即見到在您登入前所張貼的聊天訊息數 (聊天歷程)，或是可以上傳到服務 (或從服務下載) 的檔案大小等等。這些設定可以在全域、網站或服範圍設定 (亦即您可以將自訂的設定集合指派到個別的常設聊天室集區)。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPersistentChatConfiguration"}

**Lync Server 控制台：**若要使用 Lync Server 控制台修改現有的常設聊天室組態設定的集合，請依序按一下 **\[常設聊天室\]** 及 **\[常設聊天室組態\]**，然後連按兩下所要修改的集合。

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
<td><p><em>DefaultChatHistory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int16</p></td>
<td><p>聊天室立即可用的預設聊天訊息數目。請注意，此值只表示立即可用的訊息數目，而不會限制可擷取的訊息總數。</p>
<p>DefaultChatHistory 可設為介於 1 和 500 (含) 之間的任何值。預設值為 30。</p></td>
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
<td><p>所要修改之常設聊天室組態設定的唯一識別碼。若要修改在網站範圍設定的設定集合，請使用類似下列的語法：</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>若要修改在服務範圍設定的集合，請使用如下語法：</p>
<p>-Identity &quot;service:PersistentChatServer:atl-gc-001.litwareinc.com&quot;</p>
<p>若要修改全域集合，請使用下列語法：</p>
<p>-Identity &quot;global&quot;</p>
<p>若未包含 Identity 參數， <strong>Set-CsPersistentChatConfiguration</strong> Cmdlet 將自動修改全域設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
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
<td><p>系統管理員可用來管理個別聊天室之網頁的 URL。</p></td>
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

**Set-CsPersistentChatConfiguration** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PersistentChatConfiguration 物件執行個體。

## 傳回類型

無。反之， **Set-CsPersistentChatConfiguration** Cmdlet 會修改現有的 Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PersistentChatConfiguration 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsPersistentChatConfiguration](get-cspersistentchatconfiguration.md)  
[New-CsPersistentChatConfiguration](new-cspersistentchatconfiguration.md)  
[Remove-CsPersistentChatConfiguration](remove-cspersistentchatconfiguration.md)

