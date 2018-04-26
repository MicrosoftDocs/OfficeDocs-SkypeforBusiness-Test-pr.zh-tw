---
title: Set-CsXmppAllowedPartner
TOCTitle: Set-CsXmppAllowedPartner
ms:assetid: 12586746-fbea-44b1-b656-a98028c90552
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204686(v=OCS.15)
ms:contentKeyID: 49290148
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsXmppAllowedPartner

 

_**上次修改主題的時間：** 2015-03-09_

修改現有允許 XMPP 的協力廠商。Extensible Messaging and Presence Protocol (XMPP) 是開放標準的通訊協定，可使用 XML 交換訊息。允許的協力廠商是指 IM 與網站空間提供者，其使用者有權與您的 Lync Server 2013 使用者交換立即訊息與目前狀態資訊。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Set-CsXmppAllowedPartner [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsXmppAllowedPartner [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AdditionalDomains <PSListModifier>] [-Confirm [<SwitchParameter>]] [-ConnectionLimit <UInt32>] [-Description <String>] [-EnableKeepAlive <$true | $false>] [-Force <SwitchParameter>] [-PartnerType <Federated | PublicVerified | PublicUnverified>] [-ProxyFqdn <String>] [-SaslNegotiation <Required | Optional | NotSupported>] [-SupportDialbackNegotiation <$true | $false>] [-TlsNegotiation <Required | Optional | NotSupported>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會停用允許 XMPP 之協力廠商 contoso.com 的回撥交涉。作法是加入 SupportDialbackNegotiation 參數，並將參數值設為 False ($False)。

    Set-CsXmppAllowedPartner -Identity "contoso.com" -SupportDialbackNegotiation $False

## 範例 2

上述範例會為組織中所有允許 XMPP 的協力廠商啟用簡單驗證及安全性層級交涉 (必要)。為了執行此工作，命令會先使用 **Get-CsXmppAllowedPartner** Cmdlet，以傳回所有允許 XMPP 之協力廠商的集合。然後，此集合會管線傳送到 **Set-CsXmppAllowedPartner** Cmdlet，以將集合中每個協力廠商的 SaslNegotiation 屬性值設為 Required。

    Get-CsXmppAllowedPartner | Set-CsXmppAllowedPartner -SaslNegotiation "Required"

## 範例 3

範例 3 會將新的子網域 na.contoso.com 加入允許 XMPP 的協力廠商 contoso.com。為達此目的，會在語法 @{Add="na.contoso.com"} 中加入 AdditionalDomains 參數。該語法會將 na.contoso.com 加入目前在 AdditionalDomains 屬性中找到的其他網域。

    Set-CsXmppAllowedPartner -Identity "contoso.com" -AdditionalDomains @{Add="na.contoso.com"}

## 範例 4

範例 4 會從指派給允許 XMPP 之協力廠商 contoso.com 的其他網域集合中，移除 europe.contoso.com 網域。為移除此網域，會在參數值 @{Remove="europe.contoso.com"} 中加入 AdditionalDomains 參數。該語法只會從 AdditionalDomains 屬性中移除 Europe.contoso.com，而不會影響可能也儲存在 AdditionalDomains 中的其他網域。

    Set-CsXmppAllowedPartner -Identity "contoso.com" -AdditionalDomains @{Remove="europe.contoso.com"}

## 範例 5

範例 5 所示的命令會移除允許 XMPP 之協力廠商 contoso.com 的子網域支援。作法是加入 AdditionalDomains 參數及 $Null 參數值；這會刪除 AdditionalDomains 屬性中目前所含的所有網域。

    Set-CsXmppAllowedPartner -Identity "contoso.com" -AdditionalDomains $Null

## 詳細描述

Extensible Messaging and Presence Protocol (XMPP) 是標準的通訊協定 (XML 格式)，可用於在網際網路上傳送訊息。XMPP 原名 Jabber，是許多網際網路訊息與通訊應用程式 (包括 Google Talk 與 Facebook Chat) 所支援的通訊協定。

您的使用者要能和 XMPP 網路上的使用者交換立即訊息與目前狀態資訊，該網路必須設定為允許 XMPP 的協力廠商 (除此之外也必須為使用者指派允許 XMPP 存取的外部存取原則)。從設計的角度看，使用者可以和所有列名在允許的協力廠商清單中之 XMPP 網路上的使用者通訊。若不想讓使用者與指定網路上的使用者通訊，必須從允許的協力廠商清單中刪除該網路。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsXmppAllowedPartner"}

**Lync Server 控制台：**若要使用 Lync Server 控制台為現有允許 XMPP 的協力廠商編輯屬性值，請依序按一下 \[外部使用者存取\]、\[XMPP 同盟協力廠商\]，然後按兩下所要修改的協力廠商。

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
<td><p><em>AdditionalDomains</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>屬於允許之協力廠商的其他 XMPP 網域。</p></td>
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
<td><p>指出 XMPP 協力廠商是否應定期傳送 &quot;keep alive&quot; 封包，以檢查連線是否仍然有效。預設值為 True。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要修改之允許 XMPP 的協力廠商的完整網域名稱 (FQDN) (例如 fabrikam.com)。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>允許您將物件參照傳遞給 Cmdlet，而不設定個別參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>PartnerType</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.XmppFederation.PartnerType</p></td>
<td><p>指定 Lync Server 2013與 XMPP 協力廠商之間的關係。允許的值為：</p>
<p>* Federated (XMPP 協力廠商屬於同盟網域)</p>
<p>* PublicVerified</p>
<p>* PublicUnverified</p>
<p>預設值為 PublicUnverified。</p></td>
</tr>
<tr class="even">
<td><p><em>ProxyFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>XMPP 協力廠商所使用之 Proxy 伺服器的完整網域名稱。</p></td>
</tr>
<tr class="odd">
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
<tr class="even">
<td><p><em>SupportDialbackNegotiation</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指定是否要支援回撥交涉。若是使用回撥交涉，當 Server A 連絡 Server B 時，並不會立即建立通訊。反之，Server B 會先嘗試連絡 Server A 宣稱所屬之網域的授權 DNS 伺服器，以驗證 Server A 的身分識別。</p>
<p>請注意，回撥交涉不如 SASL 或 TLS 安全。一般只有在無法使用憑證來驗證伺服器身分識別時，才會用此方法。</p>
<p>預設值為 True。</p></td>
</tr>
<tr class="odd">
<td><p><em>TlsNegotiation</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.XmppFederation.TlsNegotiation</p></td>
<td><p>指定是否要支援傳輸層安全性通訊協定供伺服器對伺服器的資料串流加密之用。</p>
<p>允許的值為：</p>
<p>* Required (必須支援 TLS 交涉)</p>
<p>* Optional (如有 TLS 即使用)</p>
<p>* NotSupported (不支援 TLS 交涉)</p>
<p>預設值為 Required。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>描述執行命令後的結果，但無須實際執行命令。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

**Set-CsXmppAllowedPartner** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Settings.XmppFederation.XmppAllowedPartner\#Decorated 物件執行個體。

## 傳回類型

無。反之，**Set-CsXmppAllowedPartner** Cmdlet 會修改現有 Microsoft.Rtc.Management.WritableConfig.Settings.XmppFederation.XmppAllowedPartner\#Decorated 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsXmppAllowedPartner](get-csxmppallowedpartner.md)  
[New-CsXmppAllowedPartner](new-csxmppallowedpartner.md)  
[Remove-CsXmppAllowedPartner](remove-csxmppallowedpartner.md)

