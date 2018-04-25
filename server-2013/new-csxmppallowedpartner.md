---
title: New-CsXmppAllowedPartner
TOCTitle: New-CsXmppAllowedPartner
ms:assetid: 02f8525a-d8ec-49d8-805b-e76c5449c553
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204631(v=OCS.15)
ms:contentKeyID: 49289917
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsXmppAllowedPartner

 

_**上次修改主題的時間：** 2015-03-09_

建立允許 XMPP 的新協力廠商。Extensible Messaging and Presence Protocol (XMPP) 是開放標準的通訊協定，可使用 XML 交換訊息。允許的協力廠商是指 IM 與網站空間提供者，其使用者有權與您的 Lync Server 2013使用者交換立即訊息與目前狀態資訊。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    New-CsXmppAllowedPartner -Domain <String> <COMMON PARAMETERS>

    New-CsXmppAllowedPartner -Identity <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AdditionalDomains <PSListModifier>] [-Confirm [<SwitchParameter>]] [-ConnectionLimit <UInt32>] [-Description <String>] [-EnableKeepAlive <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-PartnerType <Federated | PublicVerified | PublicUnverified>] [-ProxyFqdn <String>] [-SaslNegotiation <Required | Optional | NotSupported>] [-SupportDialbackNegotiation <$true | $false>] [-TlsNegotiation <Required | Optional | NotSupported>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會建立允許 XMPP 的新協力廠商 contoso.com。在此範例中，PartnerType 屬性設為 "PublicVerified"。

    New-CsXmppAllowedPartner -Identity "contoso.com" -PartnerType "PublicVerified"

## 範例 2

範例 2 會建立 Identity 為 fabrikam.com 並允許 XMPP 的新協力廠商。除了根網域 (fabrikam.com) 之外，也會包含 AdditionalDomains 屬性，以支援 research.fabrikam2.com 子網域。

    New-CsXmppAllowedPartner -Identity "fabrikam.com" -AdditionalDomains "research.fabrikam2.com"

## 詳細描述

Extensible Messaging and Presence Protocol (XMPP) 是標準的通訊協定 (XML 格式)，可用於在網際網路上傳送訊息。XMPP 原名 Jabber，是許多網際網路訊息與通訊應用程式 (包括 Google Talk 與 Facebook Chat) 所支援的通訊協定。

您的使用者要能和 XMPP 網路上的使用者交換立即訊息與目前狀態資訊，該網路必須設定為允許 XMPP 的協力廠商 (除此之外也必須為使用者指派允許 XMPP 存取的外部存取原則)。從設計的角度看，使用者可以和所有列名在允許的協力廠商清單中之 XMPP 網路上的使用者通訊。若不想讓使用者與指定網路上的使用者通訊，必須從允許的協力廠商清單中刪除該網路。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsXmppAllowedPartner"}

**Lync Server 控制台：**若要使用 Lync Server 控制台建立允許 XMPP 的新協力廠商，請依序按一下 \[外部使用者存取\]、\[XMPP 同盟協力廠商\] 及 \[新增\]。

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
<td><p><em>Domain</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>允許 XMPP 之協力廠商的主要網域，例如：</p>
<p>-Domain &quot;fabrikam.com&quot;</p>
<p>您可以使用 Domain 參數或 Identity 參數指定主要網域。但同一個命令中不可同時使用這兩個參數。</p>
<p>您可以使用 AdditionalDomains 參數指定其他網域。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>允許 XMPP 之協力廠商的主要網域，例如：</p>
<p>-Identity &quot;fabrikam.com&quot;</p>
<p>您可以使用 Identity 參數或 Domain 參數指定主要網域。但同一個命令中不可同時使用這兩個參數。</p>
<p>您可以使用 AdditionalDomains 參數指定其他網域。</p></td>
</tr>
<tr class="odd">
<td><p><em>AdditionalDomains</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>屬於允許之協力廠商的其他 XMPP 網域。若要指定多個網域，請使用逗號分隔網域名稱，例如：</p>
<p>-AdditionalDomains &quot;fabrikam2.com&quot;,&quot;fabrikam3.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>ConnectionLimit</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>指定允許特定協力廠商所能同時使用的連線數上限。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>讓系統管理員能夠提供其他文字說明允許 XMPP 的協力廠商。例如 Description 可以包括協力廠商的連絡人資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableKeepAlive</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出 XMPP 協力廠商是否應定期傳送 &quot;keep alive&quot; 封包，以檢查連線是否仍然有效。</p>
<p>預設值為 True。</p></td>
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
<td><p>建立物件參照，但不實際將物件認可為永久變更。若將此參數所呼叫的 Cmdlet 輸出指派給變數，將可變更物件參照的屬性，然後呼叫此 Cmdlet 的對應 Set- Cmdlet 認可這些變更。</p></td>
</tr>
<tr class="even">
<td><p><em>PartnerType</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.XmppFederation.PartnerType</p></td>
<td><p>指定 Lync Server 2013與 XMPP 協力廠商之間的關係。允許的值為：</p>
<p>* Federated (XMPP 協力廠商屬於同盟網域)</p>
<p>* PublicVerified</p>
<p>* PublicUnverified</p>
<p>預設值為 PublicUnverified。</p></td>
</tr>
<tr class="odd">
<td><p><em>ProxyFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>XMPP 協力廠商所使用之 Proxy 伺服器的完整網域名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>SaslNegotiation</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.XmppFederation.SaslNegotiation</p></td>
<td><p>指定要支援簡單驗證及安全性階層通訊協定來進行伺服器驗證。</p>
<p>允許的值為：</p>
<p>* Required (必須支援 SASL 交涉)</p>
<p>* Optional (如有 SASL 即使用)</p>
<p>* NotSupported (不支援 SASL 交涉)</p>
<p>預設值為 Required。</p></td>
</tr>
<tr class="odd">
<td><p><em>SupportDialbackNegotiation</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指定是否要支援回撥交涉。若是使用回撥交涉，當 Server A 連絡 Server B 時，並不會立即建立通訊。反之，Server B 會先嘗試連絡 Server A 宣稱所屬之網域的授權 DNS 伺服器，以驗證 Server A 的身分識別。</p>
<p>請注意，回撥交涉不如 SASL 或 TLS 安全。一般只有在無法使用憑證來驗證伺服器身分識別時，才會用此方法。</p>
<p>預設值為 True。</p></td>
</tr>
<tr class="even">
<td><p><em>TlsNegotiation</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.XmppFederation.TlsNegotiation</p></td>
<td><p>指定是否要支援傳輸層安全性通訊協定供伺服器對伺服器的資料串流加密之用。</p>
<p>允許的值為：</p>
<p>* Required (必須支援 TLS 交涉)</p>
<p>* Optional (如有 TLS 即使用)</p>
<p>* NotSupported (不支援 TLS 交涉，預設值為 Required)。</p>
<p></p></td>
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

無。**New-CsXmppAllowedPartner** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsXmppAllowedPartner** Cmdlet 會建立新的 Microsoft.Rtc.Management.WritableConfig.Settings.XmppFederation.XmppAllowedPartner\#Decorated 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsXmppAllowedPartner](get-csxmppallowedpartner.md)  
[Remove-CsXmppAllowedPartner](remove-csxmppallowedpartner.md)  
[Set-CsXmppAllowedPartner](set-csxmppallowedpartner.md)

