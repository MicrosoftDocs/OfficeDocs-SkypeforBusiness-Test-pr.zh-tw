---
title: Remove-CsXmppAllowedPartner
TOCTitle: Remove-CsXmppAllowedPartner
ms:assetid: 858a07a3-891e-4678-b989-6339b0978427
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205055(v=OCS.15)
ms:contentKeyID: 49291543
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsXmppAllowedPartner

 

_**上次修改主題的時間：** 2015-03-09_

移除現有允許 XMPP 的協力廠商。Extensible Messaging and Presence Protocol (XMPP) 是開放標準的通訊協定，可使用 XML 交換訊息。允許的協力廠商是指 IM 與網站空間提供者，其使用者有權與您的 Lync Server 2013使用者交換立即訊息與目前狀態資訊。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Remove-CsXmppAllowedPartner -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會刪除 Identity 為 "contoso.com" 之 XMPP 允許的協力廠商。

    Remove-CsXmppAllowedPartner -Identity "contoso.com"

## 範例 2

範例 2 所示的命令會刪除所有 XMPP 允許的協力廠商。為了執行此工作，命令會先呼叫 **Get-CsXmppAllowedPartner** Cmdlet，以傳回組織目前所使用之所有 XMPP 允許的協力廠商集合。然後，此集合會管線傳送到 **Remove-CsXmppAllowedPartner** Cmdlet，以移除集合中的每個協力廠商。

    Get-CsXmppAllowedPartner | Remove-CsXmppAllowedPartner

## 範例 3

範例 3 會刪除協力廠商類型為 PublicUnverified 之所有 XMPP 允許的協力廠商。為達成此目的，命令會先使用 **Get-CsXmppAllowedPartner** Cmdlet 傳回所有允許的協力廠商集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 PartnerType 屬性等於 "PublicUnverified" 的協力廠商。接著將符合該準則的協力廠商管線傳送到 **Remove-CsXmppAllowedPartner** Cmdlet 加以刪除。

    Get-CsXmppAllowedPartner | Where-Object {$_.PartnerType -eq "PublicUnverified"} | Remove-CsXmppAllowedPartner

## 詳細描述

Extensible Messaging and Presence Protocol (XMPP) 是標準的通訊協定 (XML 格式)，可用於在網際網路上傳送訊息。XMPP 原名 Jabber，是許多網際網路訊息與通訊應用程式 (包括 Google Talk 與 Facebook Chat) 所支援的通訊協定。

您的使用者要能和 XMPP 網路上的使用者交換立即訊息與目前狀態資訊，該網路必須設定為允許 XMPP 的協力廠商 (除此之外也必須為使用者指派允許 XMPP 存取的外部存取原則)。從設計的角度看，使用者可以和所有列名在允許的協力廠商清單中之 XMPP 網路上的使用者通訊。若不想讓使用者與指定網路上的使用者通訊，必須從允許的協力廠商清單中刪除該網路。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsXmppAllowedPartner"}

**Lync Server 控制台：**若要使用 Lync Server 控制台來移除 XMPP 允許的協力廠商，請按一下 \[外部使用者存取\]，然後再按一下 \[XMPP 同盟協力廠商\]。選取所要移除的協力廠商，按一下 \[編輯\]，然後按一下 \[刪除\]。

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
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>所要刪除之 XMPP 允許的協力廠商完整網域名稱 (FQDN)。例如：</p>
<p>-Identity &quot;fabrikam.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的任何非嚴重錯誤訊息。</p></td>
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

**Remove-CsXmppAllowedPartner** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Settings.XmppFederation.XmppAllowedPartner\#Decorated 物件執行個體。

## 傳回類型

無。反之，**Remove-CsXmppAllowedPartner** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.WritableConfig.Settings.XmppFederation.XmppAllowedPartner\#Decorated 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsXmppAllowedPartner](get-csxmppallowedpartner.md)  
[New-CsXmppAllowedPartner](new-csxmppallowedpartner.md)  
[Set-CsXmppAllowedPartner](set-csxmppallowedpartner.md)

