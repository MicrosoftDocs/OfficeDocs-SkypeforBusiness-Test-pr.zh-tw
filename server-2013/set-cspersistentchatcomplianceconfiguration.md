---
title: Set-CsPersistentChatComplianceConfiguration
TOCTitle: Set-CsPersistentChatComplianceConfiguration
ms:assetid: 615625f8-574a-4832-8d3f-26721cd124d8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204949(v=OCS.15)
ms:contentKeyID: 49291087
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPersistentChatComplianceConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改現有的常設聊天室規範組態設定集合。常設聊天室規範可讓系統管理員維護常設聊天室項目及活動的封存，包括：新訊息、新事件 (例如，使用者進入或退出聊天室)、檔案上傳與下載，以及對聊天記錄執行的搜尋。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Set-CsPersistentChatComplianceConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsPersistentChatComplianceConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AdapterName <String>] [-AdapterOutputDirectory <String>] [-AdapterType <String>] [-AddChatRoomDetails <$true | $false>] [-AddUserDetails <$true | $false>] [-Confirm [<SwitchParameter>]] [-CreateFileAttachmentsManifest <$true | $false>] [-CustomConfiguration <String>] [-Force <SwitchParameter>] [-OneChatRoomPerOutputFile <$true | $false>] [-RunInterval <TimeSpan>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會將常設聊天室規範組態設定全域集合的 RunInterval 屬性設為 00 小時 : 10 分鐘 : 00 秒。

    Set-CsPersistentChatComplianceConfiguration -Identity "global" -RunInterval "00:10:00"

## 範例 2

在範例 2 中，會將組織目前使用之所有常設聊天室規範組態設定的 RunInterval 屬性設為 10 分鐘。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsPersistentChatComplianceConfiguration** Cmdlet，以傳回所有規範設定的集合。然後，此集合會管線傳送到 **Set-CsPersistentChatComplianceConfiguration** Cmdlet，以將集合中每個項目的 RunInterval 屬性值變更為 10 分鐘。

    Get-CsPersistentChatComplianceConfiguration | Set-CsPersistentChatComplianceConfiguration  -RunInterval "00:10:00"

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

許多組織 (包括醫療組織與金融組織) 都必須維護電子通訊的封存，其中包括使用常設聊天室服務所進行的交談。Lync Server 可讓您個別建立規範資料庫來保存常設聊天室中所有詳細資料的封存。常設聊天室規範可從網站範圍或服務範圍啟用或停用 (亦即可以針對特定的常設聊天室集區啟用或停用規範)。除此之外，只有 Windows PowerShell 命令列介面才可用於管理常設聊天室規範。 Lync Server 2013 控制台不提供任何有關於常設聊天室規範的管理功能。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPersistentChatComplianceConfiguration"}

**Lync Server 控制台：** **Set-CsPersistentChatComplianceConfiguration** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p><em>AdapterName</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>常設聊天室配接器的名稱。配接器是協力廠商產品，可將規範資料庫中的資料轉換成特定格式。</p></td>
</tr>
<tr class="even">
<td><p><em>AdapterOutputDirectory</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>配接器資料儲存所在之資料夾的完整路徑。您必須針對每個配接器使用不同的資料夾。</p></td>
</tr>
<tr class="odd">
<td><p><em>AdapterType</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>指定實作 Microsoft.Rtc.Internal.Chat.Server.Compliance.IComplianceAdapter 介面之 .Net 受管理類型的完整格式名稱。此配接器是由協力廠商提供，或可設為內部 XML 配接器 &quot;Microsoft.Rtc.Internal.Chat.Server.Compliance.XmlAdapter,compliance&quot; 。</p>
<p>若未指定配接器類型，常設聊天室將不會儲存規範資料。</p></td>
</tr>
<tr class="even">
<td><p><em>AddChatRoomDetails</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>設為 True 時，會為配接器提供關於每個聊天室的其他詳細資訊。這樣可能會大幅增加規範資料的大小。</p>
<p>預設值為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>AddUserDetails</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>設為 True 時，會為配接器提供關於每個聊天室使用者的其他詳細資訊。這樣可能會大幅增加規範資料的大小。</p>
<p>預設值為 False。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>CreateFileAttachmentsManifest</em></p></td>
<td><p>選用</p></td>
<td><p>Boolean</p></td>
<td><p>設為 True 時，會建立其他輸出檔案以追蹤聊天室內的檔案傳輸。這些檔案的副檔名為 .ATTACH，並置於 AdapterOutputDirectory 所指定的位置。</p></td>
</tr>
<tr class="even">
<td><p><em>CustomConfiguration</em></p></td>
<td><p>選用</p></td>
<td><p>String</p></td>
<td><p>XSLT 轉換指令碼，可讓常設聊天室以您設計的自訂格式來儲存規範資料。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>XdsIdentity</p></td>
<td><p>要修改之常設聊天室規範設定的唯一識別碼。若要修改全域集合，請使用下列語法：</p>
<p>-Identity &quot;global&quot;</p>
<p>若要修改在網站範圍設定的設定集合，請使用類似下列的語法：</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>若要修改在服務範圍設定的集合，請使用如下語法：</p>
<p>-Identity &quot;service:PersistentChatServer:atl-gc-001.litwareinc.com&quot;</p>
<p>如果未包含此參數，則 <strong>Set-CsPersistentChatComplianceConfiguration</strong> Cmdlet 將會修改全域集合。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>PSObject</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
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
<td><p>伺服器在產生下一個輸出檔案之前所等候的時間。您必須以下列格式指定 RunInterval：天數.小時數:分鐘數:秒數。例如，若要將 RunInterval 指定為 15 分鐘 (預設值)，請使用下列語法：</p>
<p>-RunInterval 00:15:00</p>
<p>RunInterval 可以設為 1 分鐘 (00:01.00) 到 30 天 (30.00:00:00) 的任何值。</p></td>
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

**Set-CsPersistentChatComplianceConfiguration** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PersistentChatComplianceConfiguration 物件執行個體。

## 傳回類型

無。反之， **Set-CsPersistentChatComplianceConfiguration** Cmdlet 會修改現有的 Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PersistentChatComplianceConfiguration 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsPersistentChatComplianceConfiguration](get-cspersistentchatcomplianceconfiguration.md)  
[New-CsPersistentChatComplianceConfiguration](new-cspersistentchatcomplianceconfiguration.md)  
[Remove-CsPersistentChatComplianceConfiguration](remove-cspersistentchatcomplianceconfiguration.md)

