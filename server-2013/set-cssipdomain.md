---
title: Set-CsSipDomain
TOCTitle: Set-CsSipDomain
ms:assetid: c19aaa3f-04d3-467e-b9d5-d574674eb4a4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412949(v=OCS.15)
ms:contentKeyID: 49292206
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsSipDomain

 

_**上次修改主題的時間：** 2015-03-09_

可讓您修改組織中之 SIP 網域的屬性值。SIP 網域是有權傳送及接收 SIP 流量的網域，會在指派 SIP 位址給使用者時使用。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsSipDomain [-Identity <XdsGlobalRelativeIdentity>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-IsDefault <$true | $false>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

顯例 1 所示的命令會使 SIP 網域 fabrikam.com 成為預設 SIP 網域；這可以透過使用 IsDefault 參數和參數值 $True 完成。執行此命令時，Fabrikam.com 會成為預設網域，而先前當做預設值的網域將會「降級」。那是因為您只能有一個預設網域。

    Set-CsSipDomain -Identity fabrikam.com -IsDefault $True

## 詳細描述

為了設定 SIP 位址給您的使用者 (進而讓他們能夠使用 Lync 2013 之類的 SIP 相關軟體)，您需要兩項資訊：使用者 ID (例如 Ken.Myer) 和 SIP 網域 (例如 litwareinc.com)。用來建構 SIP 位址的 SIP 網域必須是您 Active Directory 樹系內有權傳送及接收流量的網域。例如，假設您有名為 litwareinc.com、fabrikam.com 和 contoso.com 的網域，但是只有 litwareinc.com 已識別為 SIP 網域。在此情況下，您無法使用 sip:Ken.Myer@fabrikam.com 或 sip:Ken.Myer@contoso.com 這類的 SIP 位址，除非將 fabrikam.com 和 contoso.com 設為有效的 SIP 網域。這就是執行 **New-CsSipDomain** Cmdlet 的作用之一。

您一律需有一個已設定為預設網域的 SIP 網域。**Set-CsSipDomain** Cmdlet 可讓您變更預設的 SIP 網域。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsSipDomain** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsSipDomain"}

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
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>已設定為預設網域之 SIP 網域的完整網域名稱 (FQDN)。例如：-Identity fabrikam.com。</p></td>
</tr>
<tr class="even">
<td><p><em>IsDefault</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>表示該網域是否是預設 SIP 網域，也就是每次未明確指定網域名稱時，Lync Server 所使用的網域。如果設為 True，則新網域會成為新的預設網域。您無法將此值設定為 False，因為這樣會讓您沒有預設的 SIP 網域。</p>
<p>如果您變更預設 SIP 網域，則需要重新啟動 RTCCAA 和 RTCCAS 服務。</p></td>
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

無。**Set-CsSipDomain** Cmdlet 不接受管線傳送的資料。

## 傳回類型

**Set-CsSipDomain** Cmdlet 不會傳回任何物件或值，而會修改現有的 Microsoft.Rtc.Management.Xds.SipDomain 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsSipDomain](get-cssipdomain.md)  
[New-CsSipDomain](new-cssipdomain.md)  
[Remove-CsSipDomain](remove-cssipdomain.md)

