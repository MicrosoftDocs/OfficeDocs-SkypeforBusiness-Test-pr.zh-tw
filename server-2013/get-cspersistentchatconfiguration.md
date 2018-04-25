---
title: Get-CsPersistentChatConfiguration
TOCTitle: Get-CsPersistentChatConfiguration
ms:assetid: a15ce45f-00cc-49af-9ef4-3991d891d37e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205140(v=OCS.15)
ms:contentKeyID: 49291847
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPersistentChatConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織目前所使用之常設聊天室組態設定的資訊。常設聊天室組態設定可用於管理常設聊天室服務。例如，這些設定可讓您指定可加入聊天室的使用者人數上限。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsPersistentChatConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsPersistentChatConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回組織使用之所有常設聊天室組態設定的資訊。

    Get-CsPersistentChatConfiguration

## 範例 2

範例 2 會傳回指定之常設聊天室組態設定 (套用至 Redmond 網站之設定) 集合的資訊。

    Get-CsPersistentChatConfiguration -Identity "site:Redmond"

## 範例 3

範例 3 會傳回套用至網站範圍之所有常設聊天室組態設定的資訊。作法是加入 Filter 參數和篩選值 "service:\*"。

    Get-CsPersistentChatConfiguration -Filter "service:*"

## 範例 4

範例 4 會傳回預設聊天記錄值設定大於 30 之所有常設聊天室組態設定的資訊。為了執行此工作，命令會先使用 **Get-CsPersistentChatConfiguration** Cmdlet 傳回所有常設聊天室組態設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 DefaultChatHistory 屬性大於 (-gt) 30 的設定。

    Get-CsPersistentChatConfiguration | Where-Object {$_.DefaultChatHistory -gt 30}

## 範例 5

範例 5 顯示如何傳回尚未定義聊天室管理 URL 之所有常設聊天室組態設定的資訊。為達成此目的，命令會先使用 **Get-CsPersistentChatConfiguration** Cmdlet 傳回所有常設聊天室組態設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會選取任何 RoomManagementUrl 屬性等於 Null 值 ($Null) 的設定。

    Get-CsPersistentChatConfiguration | Where-Object {$_.RoomManagementUrl -eq $Null}

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

常設聊天室服務有一部分是由常設聊天室組態設定所控制。這些設定可以指定當您登入聊天室時，所能立即見到在您登入前所張貼的聊天訊息數 (聊天歷程)，或是可以上傳到服務 (或從服務下載) 的檔案大小等等。這些設定可以在全域、網站或服範圍設定 (亦即您可以將自訂的設定集合指派到個別的常設聊天室集區)。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPersistentChatConfiguration"}

**Lync Server 控制台：**若要在 Lync Server 控制台 中檢視常設聊天室組態設定，請按一下 **常設聊天室**，然後按一下 **常設聊天室設定**。

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
<td><p>可讓您使用萬用字元指定要傳回的一或多個常設聊天室組態設定集合。例如，下列語法會傳回在服務範圍設定的所有設定：</p>
<p>-Filter &quot;service:*&quot;</p>
<p>同一個命令中不可同時使用 Filter 與 Identity 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要傳回之常設聊天室組態設定的唯一識別碼。若要傳回全域集合，請使用下列語法：</p>
<p>-Identity &quot;global&quot;</p>
<p>若要傳回在網站範圍設定的設定集合，請使用類似下列的語法：</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>若要傳回在服務範圍設定的集合，請使用類似下列的語法：</p>
<p>-Identity &quot;service:PersistentChatServer:atl-gc-001.litwareinc.com&quot;</p>
<p>請注意，Identity 參數不可使用萬用字元。</p>
<p>命令中若未加入 Identity 參數和 Filter 參數， <strong>Get-CsPersistentChatConfiguration</strong> Cmdlet 會傳回組織所使用之所有常設聊天室組態設定的相關資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取常設聊天室組態資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Get-CsPersistentChatConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsPersistentChatConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PersistentChatConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsPersistentChatConfiguration](new-cspersistentchatconfiguration.md)  
[Remove-CsPersistentChatConfiguration](remove-cspersistentchatconfiguration.md)  
[Set-CsPersistentChatConfiguration](set-cspersistentchatconfiguration.md)

