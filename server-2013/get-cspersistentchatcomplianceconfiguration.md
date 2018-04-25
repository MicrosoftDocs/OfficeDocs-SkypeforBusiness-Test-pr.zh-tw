---
title: Get-CsPersistentChatComplianceConfiguration
TOCTitle: Get-CsPersistentChatComplianceConfiguration
ms:assetid: 01fe3824-32fb-4d75-b80a-8a7dcc109911
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204625(v=OCS.15)
ms:contentKeyID: 49289900
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPersistentChatComplianceConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織中目前所使用之常設聊天室規範組態設定的資訊。常設聊天室規範可讓系統管理員維護常設聊天室項目及活動的封存，包括：新訊息；新事件 (例如，使用者進入或退出聊天室)；檔案上傳和下載；以及所有對聊天記錄的搜尋。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsPersistentChatComplianceConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsPersistentChatComplianceConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回組織中目前所使用的所有常設聊天室規範組態設定資訊。

    Get-CsPersistentChatComplianceConfiguration

## 範例 2

範例 2 會傳回套用到 Redmond 網站之常設聊天室規範組態設定的資訊。

    Get-CsPersistentChatComplianceConfiguration -Identity "site:Redmond"

## 範例 3

範例 3 會傳回套用至服務範圍之所有常設聊天室規範組態設定的資訊。作法是加入 Filter 參數搭配篩選值 "service:\*"。

    Get-CsPersistentChatComplianceConfiguration -Filter "service:*"

## 範例 4

範例 4 會傳回 OneChatRoomPerOutputFile 屬性等於 True 之所有常設聊天室規範組態設定的資訊。為達成此目的，此命令會先使用 **Get-CsPersistentChatComplianceConfiguration** 傳回包含所有常設聊天室規範組態設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 OneChatRoomPerOutputFile 屬性等於 ($True) 的設定。

    Get-CsPersistentChatComplianceConfiguration | Where-Object {$_.OneChatRoomPerOutputFile -eq $True}

## 範例 5

範例 5 只會傳回 CustomConfiguration 屬性設為 Null 值之常設聊天室規範組態設定。為了執行此工作，命令會先使用 **Get-CsPersistentChatComplianceConfiguration** Cmdlet 傳回目前使用之所有常設聊天室規範組態設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這只會選取 CustomConfiguration 等於 Null 值 ($Null) 的設定。

    Get-CsPersistentChatComplianceConfiguration | Where-Object {$_.CustomConfiguration -ne $Null}

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

許多組織 (包括醫療組織以及金融業相關組織) 都必須保留所有其電子通訊的封存，其中包括使用常設聊天室服務所進行的交談。Lync Server 可讓您個別建立規範資料庫來保存常設聊天室中所有資料的封存。常設聊天室規範可從網站範圍或服務範圍啟用或停用 (亦即可以針對特定的常設聊天室集區啟用或停用規範)。此外， Windows PowerShell 命令列介面僅可用於管理常設聊天室規範； Lync Server 2013 控制台不提供任何有關於常設聊天室規範的管理功能。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPersistentChatComplianceConfiguration"}

**Lync Server 控制台：** **Get-CsPersistentChatComplianceConfiguration** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p>可讓您在指定要傳回之常設聊天室規範設定集合時使用萬用字元。例如，下列語法會傳回在服務範圍所設定的所有設定原則：</p>
<p>-Filter &quot;service:*&quot;</p>
<p>同一個命令中不可同時使用 Filter 與 Identity 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要傳回之常設聊天室規範設定的唯一識別碼。若要傳回全域集合，請使用下列語法：</p>
<p>-Identity &quot;global&quot;</p>
<p>若要傳回在網站範圍設定的設定集合，請使用類似下列的語法：</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>若要傳回在服務範圍設定的集合，請使用類似下列的語法：</p>
<p>-Identity &quot;service:PersistentChatServer:atl-gc-001.litwareinc.com&quot;</p>
<p>請注意，Identity 參數不可使用萬用字元。</p>
<p>如果命令未使用 Identity 參數和 Filter 參數， <strong>Get-CsPersistentChatComplianceConfiguration</strong> Cmdlet 將會傳回組織中所使用之所有常設聊天室規範設定的資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取常設聊天室規範資料，而不從中央管理存放區擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Get-CsPersistentChatComplianceConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsPersistentChatComplianceConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PersistentChatComplianceConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsPersistentChatComplianceConfiguration](new-cspersistentchatcomplianceconfiguration.md)  
[Remove-CsPersistentChatComplianceConfiguration](remove-cspersistentchatcomplianceconfiguration.md)  
[Set-CsPersistentChatComplianceConfiguration](set-cspersistentchatcomplianceconfiguration.md)

