---
title: Set-CsSite
TOCTitle: Set-CsSite
ms:assetid: f4165fdb-5828-4e81-b489-7e263b27e36b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413023(v=OCS.15)
ms:contentKeyID: 49292801
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsSite

 

_**上次修改主題的時間：** 2015-03-09_

修改您任一 Lync Server 網站的屬性。網站代表 Lync Server 集區的集合，通常會根據地理區域設計。 Lync Server 包括兩種網站類型：資料中心網站和遠端網站 (分支網站)。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsSite [-Identity <XdsGlobalRelativeIdentity>] [-Confirm [<SwitchParameter>]] [-DefaultPersistentChatPool <String>] [-Description <String>] [-DisplayName <String>] [-FederationRoute <String>] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]] [-XmppFederationRoute <String>]

## 範例

## 範例 1

範例 1 所示的命令會修改 Redmond 網站的 Description 屬性 (-Identity Redmond)。

    Set-CsSite -Identity Redmond -Description "Full-time employees in Redmond, WA."

## 範例 2

範例 2 會將 Redmond 網站的顯示名稱變更為 "US Headquarters"。

    Set-CsSite -Identity Redmond -DisplayName "US Headquarters"

## 範例 3

範例 3 所示的命令會找到所有不含 Description 的網站，然後為每個網站指派一般描述 "Litwareinc.com" 。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsSite** Cmdlet，以傳回所有 Lync Server 網站的集合。然後再將傳回的集合以管線傳送到 **Where-Object** Cmdlet，這會只挑出 Description 屬性等於 (-eq) Null 值 ($Null) 的網站。接著將這些網站以管線傳送到 **ForEach-Object** Cmdlet，以取得集合中的每個項目，然後使用 **Set-CsSite** Cmdlet 修改 Description 屬性值。

    Get-CsSite | Where-Object {$_.Description -eq $Null} | ForEach-Object {Set-CsSite $_.Identity -Description "Litwareinc.com"}

## 詳細描述

Lync Server 2010 引進 Lync Server 拓撲的新概念：網站。網站 (請勿與 Active Directory 網站或 Microsoft Exchange Server 網站混淆) 是指通常根據地理區域和網路頻寬來組織的 Lync Server 集區和伺服器的集合。例如，如果您在 Redmond 的所有電腦均位於具備高速、低延遲連線的相同區域網路上，則可能會指定包含這些電腦的 Redmond 網站。如果您在 Dublin 的電腦均位於他們自己的區域網路上，並共用高速、低延遲的連線，則可能也會建立個別的 Dublin 網站。網站也會在 Lync Server 管理中扮演一個關鍵角色：許多原則和設定都可設定於網站範圍上，以方便進行像是將一組撥號對應表套用至位於 Redmond 的使用者並將另一組撥號對應表套用至位於 Dublin 之使用者的作業。

網站可以使用 拓撲產生器 來建立，而任何對於網站基礎架構的變更 (例如，新增集區) 也必須使用拓撲產生器進行。但您可以使用 **Set-CsSite** Cmdlet 變更組織中任何網站的顯示名稱、描述和同盟路由。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsSite** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsSite"}

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
<td><p><em>DefaultPersistentChatPool</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>網站之預設常設聊天室集區的完整網域名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>讓系統管理員可以為網站物件新增額外資訊。例如，Description 可能包括網站的連絡人資訊。</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>網站的易記名稱。例如：-DisplayName &quot;North America and South America&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>FederationRoute</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>Edge Server 的服務位置，可用來提供內部網路與網際網路之間的橋接器。例如：-FederationRoute &quot;EdgeServer:atl-edge-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏當執行 Cmdlet 時可能發生的任何確認提示或非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要修改的網站名稱；例如：-Identity &quot;Redmond&quot;。在指定 Identity 時，請勿使用 &quot;site:Redmond&quot; 的格式。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
<tr class="odd">
<td><p><em>XmppFederationRoute</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>用於 XMPP (Extensible Messaging and Presence Protocol) 同盟之 Edge Server 的服務識別。例如：</p>
<p>-XmppFederationRoute EdgeServer:atl-xmpp-001.litwareinc.com</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Set-CsSite** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Set-CsSite** Cmdlet 不會傳回任何物件或值，而會修改 Microsoft.Rtc.Management.Deploy.Internal.Site+CentralSite 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsSite](get-cssite.md)

