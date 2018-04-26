---
title: New-CsPersistentChatEndpoint
TOCTitle: New-CsPersistentChatEndpoint
ms:assetid: 3a3a7acc-3239-4140-8005-ef72ab2f61e1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204811(v=OCS.15)
ms:contentKeyID: 49290632
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPersistentChatEndpoint

 

_**上次修改主題的時間：** 2015-03-09_

建立新的常設聊天室端點。常設聊天室端點是 Active Directory 連絡人物件，是 Lync Server 2013之常設聊天室集區的易記 URL。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    New-CsPersistentChatEndpoint -PersistentChatPoolFqdn <Fqdn> -SipAddress <String> [-Confirm [<SwitchParameter>]] [-DisplayName <String>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會為集區 atl-pcpool-001.litwareinc.com 建立新的常設聊天室端點。該端點的 SIP 位址為 "sip:pce@litwareinc.com"，顯示名稱為 "Persistent Chat Endpoint 1"。

    New-CsPersistentChatEndpoint -SipAddress "sip:pce@litwareinc.com" -PersistentChatPoolFqdn "atl-pcpool-001.litwareinc.com" -DisplayName "Persistent Chat Endpoint 1"

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

但您若是有使用者執行舊版的用戶端 (例如 Microsoft Lync 2010)，這些使用者在將其舊版用戶端指向集區時，可能會發現預設的常設聊天室 URI 十分不好使用。 有鑑於此，系統管理員可以使用 **New-CsPersistentChatEndpoint** Cmdlet 為集區另外建立一個連絡人物件，提供易記易用的 URI。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsPersistentChatEndpoint"}

**Lync Server 控制台：** **New-CsPersistentChatEndpoint** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p><em>PersistentChatPoolFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>新端點要與常設聊天室集區相關聯的完整網域名稱。例如：</p>
<p>-PersistentChatPoolFqdn &quot;atl-pc-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>SipAddress</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>可讓端點與 SIP 裝置 (例如 Lync 2013) 通訊的唯一識別碼。SIP 位址必須使用 sip: 首碼，以及有效的 SIP 網域，例如：</p>
<p>-SipAddress &quot;sip:pcEndpoint1@litwareinc.com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayName</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>新連絡人物件的 Active Directory 顯示名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>可讓您透過管線傳遞代表新常設聊天室端點的連絡人物件。根據預設， <strong>New-CsPersistentChatEndpoint</strong> Cmdlet 不會透過管線傳遞物件。</p></td>
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

無。 **New-CsPersistentChatEndpoint** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsPersistentChatEndpoint** Cmdlet 會建立 Microsoft.Rtc.Management.ADConnect.Schema.OCSPersistentChatContact 類別的新執行個體。

## 請參閱

#### 其他資源

[Get-CsPersistentChatEndpoint](get-cspersistentchatendpoint.md)  
[Remove-CsPersistentChatEndpoint](remove-cspersistentchatendpoint.md)

