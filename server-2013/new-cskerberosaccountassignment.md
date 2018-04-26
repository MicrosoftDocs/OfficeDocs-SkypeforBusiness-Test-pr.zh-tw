---
title: New-CsKerberosAccountAssignment
TOCTitle: New-CsKerberosAccountAssignment
ms:assetid: 02145fe6-8b7a-4508-8b3c-b9671b5bfcff
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398074(v=OCS.15)
ms:contentKeyID: 49289902
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsKerberosAccountAssignment

 

_**上次修改主題的時間：** 2015-03-09_

將 Internet Information Services (IIS) 驗證所使用的 Kerberos 帳戶指派給網站。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsKerberosAccountAssignment -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-UserAccount <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將 Kerberos 帳戶 (litwareinc\\kerberostest) 指派給 Redmond 網站，然後呼叫 **Enable-CsTopology** Cmdlet 以啟用此指派。為達成此目的，範例中的第一個命令會使用 **New-CsKerberosAccountAssignment** Cmdlet，讓 "litwareinc\\kerberostest" 帳戶和 Redmond 網站產生關聯。接著，第二個命令會呼叫 **Enable-CsTopology** Cmdlet 以在 AD DS 中建立必要的 SPN，以及啟用新指派的項目。

    New-CsKerberosAccountAssignment -UserAccount "litwareinc\kerberostest" -Identity "site:Redmond"
    Enable-CsTopology

## 詳細描述

在 Microsoft Office Communications Server 2007 和 Microsoft Office Communications Server 2007 R2 中，IIS 會以標準使用者帳戶執行。但這可能會帶來許多問題，其中包括密碼過期時，您會遺失 Web 服務這項很難診斷的問題。為避免過期密碼的問題，Lync Server 可讓您 (為實際上不存在的電腦) 建立電腦帳戶，並將其用為網站內執行 IIS 之所有電腦的驗證主體。因為這些帳戶使用 Kerberos 驗證通訊協定，所以帳戶稱為 Kerberos 帳戶，新驗證處理序別名 Kerberos Web 驗證。如此可讓您使用單一帳戶來管理所有 IIS 伺服器。

若要在這個新的驗證主體下執行伺服器，您必須先使用 **New-CsKerberosAccount** Cmdlet 建立電腦帳戶，然後將此帳戶指派給一或多個網站。完成指派後，請執行 **Enable-CsTopology** Cmdlet 來啟用帳戶與 Lync Server 網站之間的關聯。除此之外，還會在 Active Directory 網域服務 中建立所需之服務主體名稱 (SPN)。SPN 讓用戶端應用程式能夠找到特定的服務。

**New-CsKerberosAccountAssignment** Cmdlet 可讓您將 Kerberos 帳戶指派給目前與帳戶無關聯的網站。若要變更已與 Kerberos 帳戶建立關聯的網站，請改用 **Set-CsKerberosAccountAssignment** Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsKerberosAccountAssignment** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsKerberosAccountAssignment"}

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
<td><p>要指派 Kerberos 帳戶之網站的唯一識別碼。(這是網站的識別，而非電腦帳戶)。例如：-Identity &quot;site:Redmond&quot;。</p></td>
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
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
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

無。**New-CsKerberosAccountAssignment** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsKerberosAccountAssignment** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.KerberosAccount.KerberosAccountAssignment 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsKerberosAccountAssignment](get-cskerberosaccountassignment.md)  
[New-CsKerberosAccount](new-cskerberosaccount.md)  
[Remove-CsKerberosAccountAssignment](remove-cskerberosaccountassignment.md)  
[Set-CsKerberosAccountAssignment](set-cskerberosaccountassignment.md)

