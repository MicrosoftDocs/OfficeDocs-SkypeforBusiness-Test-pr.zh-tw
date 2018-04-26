---
title: Set-CsKerberosAccountAssignment
TOCTitle: Set-CsKerberosAccountAssignment
ms:assetid: 16a964d2-2515-4a37-9686-3e377de58b14
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398232(v=OCS.15)
ms:contentKeyID: 49290211
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsKerberosAccountAssignment

 

_**上次修改主題的時間：** 2015-03-09_

將 IIS Internet Information Services (IIS) 驗證所使用的 Kerberos 帳戶關聯到網站。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsKerberosAccountAssignment [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsKerberosAccountAssignment [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-UserAccount <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將現有的 Kerberos 帳戶 (litwareinc\\keberostest) 關聯到 Redmond 網站，然後使用 **Enable-CsTopology** Cmdlet 啟用新關聯。為達成此目的，範例中的第一個命令使用 **Set-CsKerberosAccountAssignment** Cmdlet 將帳戶 litwareinc\\keberostest 關聯到 Redmond 網站；接著，第二個命令會呼叫 **Enable-CsTopology** Cmdlet，以在 Active Directory 中建立必要的服務主體名稱，並啟用已修改的帳戶指派。

    Set-CsKerberosAccountAssignment -UserAccount "litwareinc\keberostest" -Identity "site:Redmond"
    Enable-CsTopology

## 詳細描述

在 Microsoft Office Communications Server 2007 和 Microsoft Office Communications Server 2007 R2 中，IIS 會以標準使用者帳戶執行。但這可能會帶來許多問題，其中包括密碼過期時，您會遺失 Web 服務這項很難診斷的問題。為避免過期密碼的問題，Lync Server 可讓您 (為實際上不存在的電腦) 建立電腦帳戶，並將其用為網站內執行 IIS 之所有電腦的驗證主體。因為這些帳戶使用 Kerberos 驗證通訊協定，所以帳戶稱為 Kerberos 帳戶，新驗證處理序別名 Kerberos Web 驗證。如此可讓您使用單一帳戶來管理所有 IIS 伺服器。

若要在這個新的驗證主體下執行伺服器，您必須先使用 **New-CsKerberosAccount** Cmdlet 建立電腦帳戶，然後將此帳戶指派給一或多個網站。完成指派後，請執行 **Enable-CsTopology** Cmdlet 來啟用帳戶與 Lync Server 網站之間的關聯。除此之外，還會在 Active Directory 網域服務 中建立所需之服務主體名稱 (SPN)。SPN 讓用戶端應用程式能夠找到特定的服務。

**Set-CsKerberosAccountAssignment** Cmdlet 可讓您變更指派給指定網站的 Kerberos 帳戶。此 Cmdlet 是供已經與某帳戶相關聯的網站使用。若要將帳戶指派給目前與 Kerberos 帳戶沒有關聯的網站，請改用 **New-CsKerberosAccountAssignment** Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsKerberosAccountAssignment** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsKerberosAccountAssignment"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>已指派 Kerberos 帳戶之網站的唯一識別碼 (這是該網站的 Identity，而不是電腦帳戶的 Identity)。例如：-Identity &quot;site:Redmond&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>KerberosAccountAssignment 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserAccount</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要指派之帳戶的帳戶名稱，必須使用「網域名稱\使用者名稱」格式。例如：-UserAccount &quot;litwareinc\kerberostest&quot;。帳戶的使用者名稱部分 (kerberostest) 是 NETBIOS 名稱，且最多可以包含 15 個字元。</p>
<p>請注意，除了名稱 UserAccount，此帳戶實際上是電腦帳戶，不是使用者帳戶。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.KerberosAccount.KerberosAccountAssignment 物件。**Set-CsKerberosAccountAssignment** Cmdlet 接受管線傳送的 Kerberos 帳戶指派物件執行個體。

## 傳回類型

**Set-CsKerberosAccountAssignment** Cmdlet 不會傳回任何物件或值，而會修改現有的 Microsoft.Rtc.Management.WritableConfig.Settings.KerberosAccount.KerberosAccountAssignment 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsKerberosAccountAssignment](get-cskerberosaccountassignment.md)  
[New-CsKerberosAccount](new-cskerberosaccount.md)  
[New-CsKerberosAccountAssignment](new-cskerberosaccountassignment.md)  
[Remove-CsKerberosAccountAssignment](remove-cskerberosaccountassignment.md)

