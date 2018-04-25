---
title: Remove-CsSipDomain
TOCTitle: Remove-CsSipDomain
ms:assetid: cccd344f-7744-46c5-b1e1-ca4e8a29772c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398865(v=OCS.15)
ms:contentKeyID: 49292338
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsSipDomain

 

_**上次修改主題的時間：** 2015-03-09_

移除先前設定供組織使用的 SIP 網域。SIP 網域是有權收送 SIP 流量的網域，會在指派 SIP 位址給使用者時使用。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsSipDomain -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 可自支援的網域名稱清單中移除 Identity 為 fabrikam.com 的 SIP 網域。請注意，如果 fabrikam.com 是組織中目前正在使用的唯一一個 SIP 網域，此命令將會失敗。失敗原因在於您的拓撲至少必須包含一個 SIP 網域。

    Remove-CsSipDomain -Identity fabrikam.com

## 範例 2

範例 2 所示的命令會刪除組織中除預設網域之外的所有 SIP 網域。為達成此目的，命令會先呼叫 **Get-CsSipDomain** Cmdlet，以傳回所有 SIP 網域的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 IsDefault 屬性不等於 True 的網域。整體效果：篩選掉預設網域，並將剩餘的網域傳送到 **Remove-CsSipDomain** Cmdlet 加以刪除。

    Get-CsSipDomain | Where-Object {$_.IsDefault -ne $True} | Remove-CsSipDomain

## 詳細描述

為了設定 SIP 位址給您的使用者 (進而讓他們能夠使用 Lync 2013 之類的 SIP 相關軟體)，您需要兩項資訊：使用者 ID (例如 Ken.Myer) 和 SIP 網域 (例如 litwareinc.com)。用來建構 SIP 位址的 SIP 網域必須是您 Active Directory 樹系內有權傳送及接收流量的網域。例如，假設您有名為 litwareinc.com、fabrikam.com 和 contoso.com 的網域，但是只有 litwareinc.com 已識別為 SIP 網域。在此情況下，您無法使用 sip:Ken.Myer@fabrikam.com 或 sip:Ken.Myer@contoso.com 這類的 SIP 位址，除非將 fabrikam.com 和 contoso.com 設為有效的 SIP 網域。這就是執行 **New-CsSipDomain** Cmdlet 的作用之一。

對於已經授權的 SIP 網域，您可以使用 **Remove-CsSipDomain** Cmdlet取消其授權。此 Cmdlet 可從核准的 SIP 網域清單中移除指定的網域。請注意，您無法移除預設網域。如果要移除預設網域，必須先將其他 SIP 網域設定為預設網域。如果您只有一個 SIP 網域，該網域會自動將設定為預設網域，而且無法加以移除。

此外，您無法移除任何擁有一或多個已指派給它之 SIP 位址的 SIP 網域。例如，如果 Ken Myer 的 SIP 位址為 "sip:kenmyer@contoso.com"，則您無法將 Contoso.com 當成 SIP 網域來移除。若要移除目前正在使用的 SIP 網域，必須先將新的 SIP 位址指派給 SIP 位址中含有該網域的所有使用者。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsSipDomain** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsSipDomain"}

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
<td><p>要移除之 SIP 網域的完整網域名稱 (FQDN)：例如：-Identity fabrikam.com。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
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

Microsoft.Rtc.Management.Xds.SipDomain 物件。**Remove-CsSipDomain** Cmdlet 接受 SIP 網域物件管線傳送的執行個體。

## 傳回類型

無。反之，**Remove-CsSipDomain** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.Xds.SipDomain 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsSipDomain](get-cssipdomain.md)  
[New-CsSipDomain](new-cssipdomain.md)  
[Set-CsSipDomain](set-cssipdomain.md)

