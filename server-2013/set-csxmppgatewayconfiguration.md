---
title: Set-CsXmppGatewayConfiguration
TOCTitle: Set-CsXmppGatewayConfiguration
ms:assetid: 2b90d563-a3fe-45bd-81da-210a7459411b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204769(v=OCS.15)
ms:contentKeyID: 49290428
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsXmppGatewayConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

修改組織所使用的 XMPP 閘道組態設定。Extensible Messaging and Presence Protocol (XMPP) 是使用 XML 格式交換訊息的開放標準通訊協定。XMPP 閘道可讓 Lync Server 2013 使用者與使用 XMPP 之 IM 和目前狀態提供者的使用者交換立即訊息和目前狀態資訊。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Set-CsXmppGatewayConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsXmppGatewayConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-ConnectionLimit <UInt32>] [-DialbackPassphrase <String>] [-EnableLoggingAllMessageBodies <$true | $false>] [-Force <SwitchParameter>] [-KeepAliveInterval <UInt32>] [-PartnerConnectionLimit <UInt32>] [-StreamEstablishmentTimeout <UInt32>] [-StreamInactivityTimeout <UInt32>] [-SubscriptionRefreshInterval <UInt32>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會修改全域 XMPP 閘道設定集合的 ConnectionLimit 屬性。

    Set-CsXmppGatewayConfiguration -Identity "global" -ConnectionLimit 1200

## 詳細描述

Extensible Messaging and Presence Protocol (XMPP) 是標準的通訊協定 (XML 格式)，可用於在網際網路上傳送訊息。XMPP 原名 Jabber，是許多網際網路訊息與通訊應用程式 (包括 Google Talk 與 Facebook Chat) 所支援的通訊協定。

讓 Lync 2013 可與 XMPP 網路上之使用者通訊的 XMPP 閘道，最初是以 Microsoft Lync Server 2010 的附加元件形式發行，Lync Server 2013已將此功能內建到軟體之中。換言之，只要符合下列條件，您的使用者即可與 XMPP 使用者通訊：

  -   
    設定 XMPP 閘道設定。

  -   
    設定其他 XMPP 網路 (例如 Google Talk) 做用允許的 XMPP 協力廠商。

請注意，Lync Server 2013只提供一組全域 XMPP 組態設定集。您無法只為指定的網站或登錄器集區啟用或停用 XMPP。事實上您根本無法啟用或停用 XMPP，因此一律會啟用 XMPP。若您不想讓使用者與 XMPP 網路通訊，必須移除所有允許的 XMPP 協力廠商。只有設定為允許之協力廠商的 XMPP 網路，使用者才可與之通訊。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsXmppGatewayConfiguration"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Set-CsXmppGatewayConfiguration** Cmdlet 所執行的功能。

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
<td><p>執行命令前先要求您確認。</p></td>
</tr>
<tr class="even">
<td><p><em>ConnectionLimit</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>允許用於所有 XMPP 協力廠商的同時連線總數。預設值為 1000。</p></td>
</tr>
<tr class="odd">
<td><p><em>DialbackPassphrase</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>透過 TCP 回撥連線來連接至 XMPP 協力廠商時，所使用的密碼。藉由 TCP 回撥，協力廠商可以連絡 XMPP 閘道，然後掛斷電話。XMPP 閘道會回撥給協力廠商，然後就可以開始通訊工作階段。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableLoggingAllMessageBodies</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數設為 True 時，Lync Server 2013會記錄所有立即訊息的實際內容。基於隱私權，通常會刪除訊息內容，只會在記錄檔中包含通訊端點的資訊。</p>
<p>預設值為 False。</p></td>
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
<td><p>要修改之 XMPP 閘道組態設定的唯一識別碼。因為您只會有這些設定的單一全域執行個體，所以不需要在呼叫 <strong>Set-CsXmppGatewayConfiguration</strong> Cmdlet 時指定 Identity。但是，您可以視需要使用下列語法來參照全域設定：</p>
<p>-Identity global</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>允許您將物件參照傳遞給 Cmdlet，而非設定個別參數值。</p></td>
</tr>
<tr class="even">
<td><p><em>KeepAliveInterval</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>最多經過多少時間 (以秒為單位) 後，協力廠商必須傳送 &quot;keep alive&quot; 訊息 (Keep Alive 訊息只是驗證連線仍作用中)。如果過了時間間隔，還沒收到 Keep Alive 訊息，將關閉連線。預設值為 300 秒。</p></td>
</tr>
<tr class="odd">
<td><p><em>PartnerConnectionLimit</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>允許用於單一 XMPP 協力廠商的同時連線總數。預設值為 20。</p></td>
</tr>
<tr class="even">
<td><p><em>StreamEstablishmentTimeout</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>配置讓 XMPP 協力廠商建立 XMPP 資料流的時間上限 (以秒為單位)。如果過了此逾時時段，連線會自動終止。預設值為 60 秒。</p></td>
</tr>
<tr class="odd">
<td><p><em>StreamInactivityTimeout</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>XMPP 資料流在停止作用多少時間後 (以秒為單位)，連線會自動終止。預設值為 600 秒 (10 分鐘)。</p></td>
</tr>
<tr class="even">
<td><p><em>SubscriptionRefreshInterval</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>最多經過多少時間 (以秒為單位) 後，協力廠商必須重新整理其目前狀態訂閱。預設值為 28800 秒 (8 小時)。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>描述執行命令後的結果，但無須實際執行命令。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

**Set-CsXmppGatewayConfiguration** Cmdlet 接受 Microsoft.Rtc.Management.WritableConfig.Settings.XmppFederation.XmppGatewaySettings 物件的管線傳送執行個體。

## 傳回類型

無。反之，**Set-CsXmppGatewayConfiguration** Cmdlet 會修改現有的 Microsoft.Rtc.Management.WritableConfig.Settings.XmppFederation.XmppGatewaySettings 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsXmppGatewayConfiguration](get-csxmppgatewayconfiguration.md)

