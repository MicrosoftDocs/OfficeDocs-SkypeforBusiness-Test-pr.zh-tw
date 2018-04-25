---
title: Get-CsXmppGatewayConfiguration
TOCTitle: Get-CsXmppGatewayConfiguration
ms:assetid: 4c9ee876-de89-420c-bda9-9901cef47799
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204869(v=OCS.15)
ms:contentKeyID: 49290848
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsXmppGatewayConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織所使用之 XMPP 閘道組態設定的資訊。Extensible Messaging and Presence Protocol (XMPP) 是使用 XML 格式交換訊息的開放標準通訊協定。XMPP 閘道可讓 Lync Server 2013 使用者與使用 XMPP 之 IM 和目前狀態提供者的使用者交換立即訊息和目前狀態資訊。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsXmppGatewayConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsXmppGatewayConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 會傳回組織目前所使用之 XMPP 閘道設定的資訊。因為 Lync Server 2013只允許單一、全域的閘道設定集合，所以無須加入 Identity 參數取回全域設定的資訊。

    Get-CsXmppGatewayConfiguration

## 詳細描述

Extensible Messaging and Presence Protocol (XMPP) 是標準的通訊協定 (XML 格式)，可用於在網際網路上傳送訊息。XMPP 原名 Jabber，是許多網際網路訊息與通訊應用程式 (包括 Google Talk 與 Facebook Chat) 所支援的通訊協定。

讓 Lync 2013 可與 XMPP 網路上之使用者通訊的 XMPP 閘道，最初是以 Microsoft Lync Server 2010 的附加元件形式發行，Lync Server 2013已將此功能內建到軟體之中。換言之，只要符合下列條件，您的使用者即可與 XMPP 使用者通訊：

  -   
    設定 XMPP 閘道設定。

  -   
    設定其他 XMPP 網路 (例如 Google Talk) 做用允許的 XMPP 協力廠商。

請注意，Lync Server 2013只提供一組全域 XMPP 組態設定集。您無法只為指定的網站或登錄器集區啟用或停用 XMPP。事實上您根本無法啟用或停用 XMPP，因此一律會啟用 XMPP。若您不想讓使用者與 XMPP 網路通訊，必須移除所有允許的 XMPP 協力廠商。只有設定為允許之協力廠商的 XMPP 網路，使用者才可與之通訊。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsXmppGatewayConfiguration"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Get-CsXmppGatewayConfiguration** Cmdlet 所執行的功能。

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
<td><p>System.String</p></td>
<td><p>可讓您在參照 XMPP 閘道組態設定集合時，使用萬用字元值。因為您只能有這些設定的單一、全域執行個體，所以沒有理由使用 Filter 參數。不過，如果您想要，可以使用下列語法來參照全域設定：</p>
<p>-Filter &quot;g*&quot;</p>
<p>該語法會傳回 Identity 以字母 &quot;g&quot; 為開頭的所有 XMPP 閘道組態設定。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>XMPP 閘道組態設定的唯一識別碼。因為您只能有這些設定的單一、全域執行個體，所以在呼叫 <strong>Get-CsXmppGatewayConfiguration</strong> Cmdlet 時，不需要指定 Identity。但是，您可以視需要使用下列語法來參照全域設定：</p>
<p>-Identity global</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取 XMPP 閘道資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsXmppGatewayConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsXmppGatewayConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.XmppFederation.XmppGatewaySettings 物件的執行個體。

## 請參閱

#### 其他資源

[Set-CsXmppGatewayConfiguration](set-csxmppgatewayconfiguration.md)

