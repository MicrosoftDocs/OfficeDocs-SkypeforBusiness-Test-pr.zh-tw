---
title: Get-CsXmppAllowedPartner
TOCTitle: Get-CsXmppAllowedPartner
ms:assetid: 6d031b38-325a-4196-998f-c473390f2055
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204981(v=OCS.15)
ms:contentKeyID: 49291250
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsXmppAllowedPartner

 

_**上次修改主題的時間：** 2015-03-09_

傳回獲授權可與您的組織通訊之 XMPP 協力廠商的資訊。Extensible Messaging and Presence Protocol (XMPP) 是使用 XML 格式交換訊息的開放標準通訊協定。允許的協力廠商是指獲授權可與 Lync Server 2013使用者交換立即訊息和目前狀態資訊的 IM 和目前狀態提供者。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsXmppAllowedPartner [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsXmppAllowedPartner [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回設定供組織使用之所有 XMPP 允許之協力廠商的資訊。

    Get-CsXmppAllowedPartner

## 範例 2

範例 2 會傳回單一 XMPP 允許之協力廠商 (Identity 為 xmpp.contoso.com 的協力廠商) 的資訊。

    Get-CsXmppAllowedPartner -Identity "xmpp.contoso.com"

## 範例 3

範例 3 會針對 Identity 以 ".org" 字串值結尾 (例如，xmpp.contoso.org and xmpp.fabrikam.org) 之所有 XMPP 允許的協力廠商傳回資訊。

    Get-CsXmppAllowedPartner - Filter "*.org"

## 範例 4

範例 4 所示的命令會針對需要簡單驗證及安全性層級交涉之所有 XMPP 允許的協力廠商傳回相關資訊。為達成此目的，命令會先使用 **Get-CsXmppAllowedPartner** Cmdlet，以傳回所有 XMPP 允許之協力廠商的資訊。傳回的協力廠商接著會管線傳送到 **Where-Object** Cmdlet，這會只選取 SaslNegotiation 屬性等於 Required 的協力廠商。

    Get-CsXmppAllowedPartner | Where-Object {$_.SaslNegotiation -eq "Required"}

## 詳細描述

Extensible Messaging and Presence Protocol (XMPP) 是標準的通訊協定 (XML 格式)，可用於在網際網路上傳送訊息。XMPP 原名 Jabber，是許多網際網路訊息與通訊應用程式 (包括 Google Talk 與 Facebook Chat) 所支援的通訊協定。

您的使用者要能和 XMPP 網路上的使用者交換立即訊息與目前狀態資訊，該網路必須設定為允許 XMPP 的協力廠商 (除此之外也必須為使用者指派允許 XMPP 存取的外部存取原則)。從設計的角度看，使用者可以和所有列名在允許的協力廠商清單中之 XMPP 網路上的使用者通訊。若不想讓使用者與指定網路上的使用者通訊，必須從允許的協力廠商清單中刪除該網路。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsXmppAllowedPartner"}

**Lync Server 控制台：**若要在 Lync Server 控制台中檢視 XMPP 允許之協力廠商的資訊，請按一下 \[外部使用者存取\]，然後再按一下 \[XMPP 同盟協力廠商\]。

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
<td><p>可讓您在指定所要傳回 XMPP 允許之協力廠商的 Identity 時使用萬用字元。例如，篩選值 &quot;*.org&quot; 可傳回 Identity 結尾為字串值 &quot;.org&quot; 之所有 XMPP 允許的協力廠商集合。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要傳回 XMPP 允許之協力廠商的完整網域名稱 (FQDN) (例如 fabrikam.com)。若未指定此參數，也未指定 Filter 參數，將會傳回設定供組織使用的所有 XMPP 協力廠商。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取 XMPP 允許的協力廠商，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsXmppAllowedPartner** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsXmppAllowedPartner** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.XmppFederation.XmppAllowedPartner\#Decorated 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsXmppAllowedPartner](new-csxmppallowedpartner.md)  
[Remove-CsXmppAllowedPartner](remove-csxmppallowedpartner.md)  
[Set-CsXmppAllowedPartner](set-csxmppallowedpartner.md)

