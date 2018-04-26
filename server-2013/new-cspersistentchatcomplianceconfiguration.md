---
title: New-CsPersistentChatComplianceConfiguration
TOCTitle: New-CsPersistentChatComplianceConfiguration
ms:assetid: a61b76a9-0e2b-4f64-b2fa-cddadc15451c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205163(v=OCS.15)
ms:contentKeyID: 49291905
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPersistentChatComplianceConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

在網站範圍或服務範圍建立新的常設聊天室規範組態設定集合。常設聊天室規範可讓系統管理員維護常設聊天室項目及活動的封存，包括：新訊息、新事件 (例如，使用者進入或退出聊天室)、檔案上傳與下載，以及對聊天記錄執行的搜尋。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    New-CsPersistentChatComplianceConfiguration -Identity <XdsIdentity> [-AdapterName <String>] [-AdapterOutputDirectory <String>] [-AdapterType <String>] [-AddChatRoomDetails <$true | $false>] [-AddUserDetails <$true | $false>] [-Confirm [<SwitchParameter>]] [-CreateFileAttachmentsManifest <$true | $false>] [-CustomConfiguration <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-OneChatRoomPerOutputFile <$true | $false>] [-RunInterval <TimeSpan>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會建立 Redmond 網站之常設聊天室規範組態設定的新集合。在此範例中，AddUserDetails 和 AddChatRoomDetails 屬性都會設為 True ($True)。

    New-CsPersistentChatComplianceConfiguration -Identity "site:Redmond" -AddUserDetails $True -AddChatRoomDetails $True

## 範例 2

範例 2 也會示範如何建立 Redmond 網站之常設聊天室規範組態設定的新集合。在此範例中，RunInterval 屬性設為 30 分鐘，也就是 00 小時：30 分鐘：00 秒。

    New-CsPersistentChatComplianceConfiguration -Identity "site:Redmond" -RunInterval "00:30:00"

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

許多組織 (包括醫療組織與金融組織) 都必須維護其所有電子通訊的封存，其中包括使用常設聊天室服務所進行的交談。 Lync Server 2013 可讓您個別建立規範資料庫來保存常設聊天室中所有詳細資料的封存。常設聊天室規範可從網站範圍或服務範圍啟用或停用 (亦即可以針對特定的常設聊天室集區啟用或停用規範)。除此之外，只能使用 Windows PowerShell 命令列介面來管理常設聊天室規範。 Lync Server 2013 控制台不提供任何可用來管理常設聊天室規範的功能。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsPersistentChatComplianceConfiguration"}

Lync Server 控制台：**New-CsPersistentChatComplianceConfiguration** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p>XdsIdentity</p></td>
<td><p>所建立之新常設聊天室規範設定的唯一識別碼。可在網站範圍或服務範圍建立新規範設定 (僅限 Persistent Chat Server 服務)。若要在網站範圍建立新的設定，請使用類似下列的語法：</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>若要在服務範圍建立新的設定，請使用類似下列的語法：</p>
<p>-Identity &quot;service:PersistentChatServer:atl-gc-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>AdapterName</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>規範設定所使用的常設聊天室配接器名稱。配接器是第三方產品，可將規範資料庫中的資料轉換為特定格式。</p></td>
</tr>
<tr class="odd">
<td><p><em>AdapterOutputDirectory</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>配接器資料儲存所在之資料夾的完整路徑。您必須針對每個配接器使用不同的資料夾。</p></td>
</tr>
<tr class="even">
<td><p><em>AdapterType</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>指定實作 Microsoft.Rtc.Internal.Chat.Server.Compliance.IComplianceAdapter 介面之 .Net 受管理類型的完整格式名稱。此配接器是由協力廠商提供，或可設為內部 XML 配接器 &quot;Microsoft.Rtc.Internal.Chat.Server.Compliance.XmlAdapter,compliance&quot; 。</p>
<p>若未指定配接器類型，常設聊天室將不會儲存規範資料。</p></td>
</tr>
<tr class="odd">
<td><p><em>AddChatRoomDetails</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>設為 True 時，會為配接器提供關於每個聊天室的其他詳細資訊。這樣可能會大幅增加規範資料的大小。</p>
<p>預設值為 False。</p></td>
</tr>
<tr class="even">
<td><p><em>AddUserDetails</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>設為 True 時，會為配接器提供關於每個聊天室使用者的其他詳細資訊。這樣可能會大幅增加規範資料的大小。</p>
<p>預設值為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>CreateFileAttachmentsManifest</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>設為 True 時，會建立其他輸出檔案以追蹤聊天室內的檔案傳輸。這些檔案的副檔名為 .ATTACH，並置於 AdapterOutputDirectory 所指定的位置。</p></td>
</tr>
<tr class="odd">
<td><p><em>CustomConfiguration</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>XSLT 轉換指令碼，可讓常設聊天室以您設計的自訂格式來儲存規範資料。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="even">
<td><p><em>OneChatRoomPerOutputFile</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>設為 True 時，會針對每個聊天室建立不同的報告。預設值為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>RunInterval</em></p></td>
<td><p>選用</p></td>
<td><p>TimeSpan</p></td>
<td><p>伺服器在產生下一個輸出檔案之前所等候的時間。您必須以下列格式指定 RunInterval：天數.小時數:分鐘數:秒數。例如，若要將 RunInterval 指定為 30 分鐘 (預設值)，請使用下列語法：</p>
<p>-RunInterval 上午 12:30:00</p>
<p>您可以將 RunInterval 設為 1 分鐘 (00:01.00) 到 30 天 (30.00:00:00) (含) 之間的任何值。預設值為 15 分鐘 (00:15:00)。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **New-CsPersistentChatComplianceConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsPersistentChatComplianceConfiguration** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PersistentChatComplianceConfiguration 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsPersistentChatComplianceConfiguration](get-cspersistentchatcomplianceconfiguration.md)  
[Remove-CsPersistentChatComplianceConfiguration](remove-cspersistentchatcomplianceconfiguration.md)  
[Set-CsPersistentChatComplianceConfiguration](set-cspersistentchatcomplianceconfiguration.md)

