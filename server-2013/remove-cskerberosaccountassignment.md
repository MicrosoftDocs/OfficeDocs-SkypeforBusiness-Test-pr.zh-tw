---
title: Remove-CsKerberosAccountAssignment
TOCTitle: Remove-CsKerberosAccountAssignment
ms:assetid: f878fed1-ee6d-4275-8f76-2bc134e465c2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413052(v=OCS.15)
ms:contentKeyID: 49292868
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsKerberosAccountAssignment

 

_**上次修改主題的時間：** 2015-03-09_

移除一個或多個 Kerberos 帳戶指派。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsKerberosAccountAssignment -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會移除 Redmond 網站的 Kerberos 帳戶指派，然後呼叫 **Enable-CsTopology** Cmdlet 完成停用 Kerberos Web 驗證。

    Remove-CsKerberosAccountAssignment -Identity "site:Redmond"
    Enable-CsTopology

## 範例 2

範例 2 會刪除目前所使用的所有 Kerberos 帳戶指派。為達成此目的，第一個命令會呼叫 **Get-CsKerberosAccountAssignment** Cmdlet (不含任何參數)，以傳回所有 Kerberos 帳戶指派的集合。然後，此集合會管線傳送到 **Remove-CsKerberosAccountAssignment** Cmdlet，以刪除集合中的每一個指派。完成後，範例中的第二個命令會呼叫 **Enable-CsTopology** Cmdlet 完成停用 Kerberos Web 驗證。

    Get-CsKerberosAccountAssignment | Remove-CsKerberosAccountAssignment
    Enable-CsTopology

## 詳細描述

在 Microsoft Office Communications Server 2007 和 Microsoft Office Communications Server 2007 R2 中，IIS 會以標準使用者帳戶執行。但這可能會帶來許多問題，其中包括密碼過期時，您會遺失 Web 服務這項很難診斷的問題。為避免過期密碼的問題，Lync Server 可讓您 (為實際上不存在的電腦) 建立電腦帳戶，並將其用為網站內執行 IIS 之所有電腦的驗證主體。因為這些帳戶使用 Kerberos 驗證通訊協定，所以帳戶稱為 Kerberos 帳戶，新驗證處理序別名 Kerberos Web 驗證。如此可讓您使用單一帳戶來管理所有 IIS 伺服器。

若要在這個新驗證主體下執行伺服器，首先必須使用 **New-CsKerberosAccount** Cmdlet 建立電腦帳戶 (再次強調，不依賴實際電腦)，然後將此帳戶指派給一個或多個網站。指派完成後，執行 **Enable-CsTopology** Cmdlet 來啟用關聯性；特別是在 Active Directory 網域服務 中建立所需的服務主體名稱 (SPN)。SPN 讓用戶端應用程式能夠找到特定的服務。

每一個 Lync Server 網站都可以建立關聯性，至多一個單一 Kerberos 帳戶(不過，每一個帳戶可以和多個網站建立關聯性)。您可以隨時使用 **Remove-CsKerberosAccountAssignment** Cmdlet 來移除網站和帳戶之間的關聯性。這個 Cmdlet 不刪除有問題的帳戶；它只是中斷網站和帳戶之間的關聯性，有效停用該網站內的 Kerberos Web 驗證。

請注意，執行 **Remove-CsKerberosAccountAssignment** Cmdlet，接著您必須執行 **Enable-CsTopology** Cmdlet。這樣會從 Active Directory 移除帳戶的服務主體名稱，而且完全停用 Kerberos Web 驗證。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsKerberosAccountAssignment** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsKerberosAccountAssignment"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要移除 Kerberos 帳戶指派之網站的唯一識別碼(這是該網站的 Identity，而不是 Kerberos 帳戶)。例如：-Identity &quot;site:Redmond&quot;。</p></td>
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
<td><p>若顯示，則抑制所有錯誤訊息，嚴重錯誤除外。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.KerberosAccount.KerberosAccountAssignment 物件。**Remove-CsKerberosAccountAssignment** Cmdlet 會接受 Kerberos 帳戶指派物件的管線執行個體。

## 傳回類型

無。**Remove-CsKerberosAccountAssignment** Cmdlet 不會傳回任何物件或值，而是刪除現有 Microsoft.Rtc.Management.WritableConfig.Settings.KerberosAccount.KerberosAccountAssignment 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsKerberosAccountAssignment](get-cskerberosaccountassignment.md)  
[New-CsKerberosAccountAssignment](new-cskerberosaccountassignment.md)  
[Set-CsKerberosAccountAssignment](set-cskerberosaccountassignment.md)

