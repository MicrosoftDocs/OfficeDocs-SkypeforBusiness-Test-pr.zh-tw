---
title: New-CsSipDomain
TOCTitle: New-CsSipDomain
ms:assetid: 385f0f23-397b-4d8d-b9b7-ec942cda4a99
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425857(v=OCS.15)
ms:contentKeyID: 49290602
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsSipDomain

 

_**上次修改主題的時間：** 2015-03-09_

建立供組織使用的新 SIP 網域。SIP 網域是有權收送 SIP 流量的網域，會在指派 SIP 位址給使用者時使用。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsSipDomain -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-IsDefault <$true | $false>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會建立新的 SIP 網域，也就是 Identity 為 fabrikam.com 的網域。

    New-CsSipDomain -Identity fabrikam.com

## 範例 2

範例 2 會建立名稱為 fabrikam.com 的新 SIP 網域，並將此新網域設為預設 SIP 網域。將 fabrikam.com 設為預設網域後，此命令也會將先前做為預設 SIP 網域的網域「降級」。那是因為您只能有一個預設 SIP 網域。

    New-CsSipDomain -Identity fabrikam.com -IsDefault $True

## 詳細描述

為了設定 SIP 位址給您的使用者 (進而讓他們能夠使用 Lync 2013 之類的 SIP 相關軟體)，您需要兩項資訊：使用者 ID (例如 Ken.Myer) 和 SIP 網域 (例如 litwareinc.com)。用來建構 SIP 位址的 SIP 網域必須是您 Active Directory 樹系內有權傳送及接收流量的網域。例如，假設您有名為 litwareinc.com、fabrikam.com 和 contoso.com 的網域，但是只有 litwareinc.com 已識別為 SIP 網域。在此情況下，您無法使用 sip:Ken.Myer@fabrikam.com 或 sip:Ken.Myer@contoso.com 這類的 SIP 位址，除非將 fabrikam.com 和 contoso.com 設為有效的 SIP 網域。這就是執行 **New-CsSipDomain** Cmdlet 的作用之一。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsSipDomain** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsSipDomain"}

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
<td><p>新 SIP 網域的完整網域名稱 (FQDN)。例如：-Identity fabrikam.com。</p></td>
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
<td><p><em>IsDefault</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>表示該網域是否為預設 SIP 網域，也就是每次未明確指定網域名稱時，Lync Server 所使用的網域。若此參數設為 True，新網域也會成為新的預設網域。</p>
<p>IsDefault 的預設值為 False。如果您不想將新網域設為預設網域，只要省略此參數即可。</p>
<p>如果您變更預設 SIP 網域，則需重新啟動 RTCCAA 及 RTCCAS 服務。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsSipDomain** Cmdlet 不接受管線傳送的資料。

## 傳回類型

**New-CsSipDomain** Cmdlet 會建立 Microsoft.Rtc.Management.Xds.SipDomain 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsSipDomain](get-cssipdomain.md)  
[Remove-CsSipDomain](remove-cssipdomain.md)  
[Set-CsSipDomain](set-cssipdomain.md)

