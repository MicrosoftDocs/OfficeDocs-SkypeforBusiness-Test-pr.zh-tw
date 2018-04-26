---
title: New-CsKerberosAccount
TOCTitle: New-CsKerberosAccount
ms:assetid: 67ffa1b1-0ca5-410b-81f7-2375b9dbef3c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398485(v=OCS.15)
ms:contentKeyID: 49291186
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsKerberosAccount

 

_**上次修改主題的時間：** 2015-03-09_

建立供 Internet Information Services (IIS) 驗證之用的 Kerberos 帳戶。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsKerberosAccount -UserAccount <String> [-Confirm [<SwitchParameter>]] [-ContainerDN <String>] [-Force <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會建立一個新的 Kerberos 帳戶 (litwareinc\\kerberostest)，然後將該帳戶指派至 Redmond 網站。為達成此目的，範例中的第一個命令會建立名為 "litwareinc\\kerberostest" 的帳戶。該帳戶會建立在 Litwareinc.com 網域的 Computers 容器中。建立帳戶後，第二個命令會使用 **New-CsKerberosAccountAssignment** Cmdlet，將該 Kerberos 帳戶指派至 Redmond 網站。

進行新帳戶的指派後，最後一個命令會呼叫 **Enable-CsTopology** Cmdlet 讓變更生效。

    New-CsKerberosAccount -UserAccount "litwareinc\kerberostest" -ContainerDN "cn=Computers,dc=litwareinc,dc=com"
    
    New-CsKerberosAccountAssignment -UserAccount "litwareinc\kerberostest" -Identity "site:Redmond"
    Enable-CsTopology

## 詳細描述

在 Microsoft Office Communications Server 2007 和 Microsoft Office Communications Server 2007 R2 中，IIS 會以標準使用者帳戶執行。但這可能會帶來許多問題，其中包括密碼過期時，您會遺失 Web 服務 這項很難診斷的問題。為避免過期密碼的問題，Lync Server 可讓您 (為實際上不存在的電腦) 建立電腦帳戶，並將其用為網站內執行 IIS 之所有電腦的驗證主體。因為這些帳戶使用 Kerberos 驗證通訊協定，所以帳戶稱為 Kerberos 帳戶，新驗證處理序別名 Kerberos Web 驗證。如此可讓您使用單一帳戶來管理所有 IIS 伺服器。

若要在此單一驗證主體下執行伺服器，您必須先使用 **New-CsKerberosAccount** Cmdlet 建立新的電腦帳戶，然後將此帳戶指派給一或多個網站。完成指派後，請執行 **Enable-CsTopology** Cmdlet 來啟用帳戶與 Lync Server 網站之間的關聯。除此之外，這會在 Active Directory 網域服務 中建立所需之服務主體名稱 (SPN)。SPN 可讓用戶端應用程式找到特定服務。

誰可以執行這個 Cmdlet：您必須是網域系統管理員才能在本機執行 **New-CsKerberosAccount** Cmdlet。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsKerberosAccount\\b"}

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
<td><p><em>UserAccount</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>新帳戶的帳戶名稱，必須使用「網域名稱\使用者名稱」格式。例如：-UserAccount &quot;litwareinc\kerberostest&quot;。請注意，如果指定的帳戶已經存在，您的命令就會失敗。</p>
<p>此外請注意，儘管名稱為 UserAccount，但藉由執行 <strong>New-CsKerberosAccount</strong> Cmdlet 建立的帳戶其實為電腦帳戶，而非使用者帳戶。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>ContainerDN</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要在其中建立新帳戶之 Active Directory 容器的辨別名稱。例如：-ContainerDN &quot;ou=Finance,dc=litwareinc,dc=com&quot;。若未指定此參數，則 <strong>New-CsKerberosAccount</strong> Cmdlet 會在 Active Directory 的 Computers 容器中建立新帳戶。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\KerberosAccount.html&quot;。</p></td>
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

無。**New-CsKerberosAccount** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsKerberosAccount** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.KerberosAccount.KerberosAccount 物件的新執行個體。

## 請參閱

#### 其他資源

[New-CsKerberosAccountAssignment](new-cskerberosaccountassignment.md)

