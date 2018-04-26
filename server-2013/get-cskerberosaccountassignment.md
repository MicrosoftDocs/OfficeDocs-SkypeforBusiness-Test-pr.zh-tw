---
title: Get-CsKerberosAccountAssignment
TOCTitle: Get-CsKerberosAccountAssignment
ms:assetid: 6eaba274-1693-42a7-841d-513bc1153647
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398526(v=OCS.15)
ms:contentKeyID: 49291269
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsKerberosAccountAssignment

 

_**上次修改主題的時間：** 2015-03-09_

傳回設定供組織使用之 Kerberos 帳戶指派的資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsKerberosAccountAssignment [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsKerberosAccountAssignment [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回目前在組織中使用之所有 Kerberos 帳戶指派的資訊。

    Get-CsKerberosAccountAssignment

## 範例 2

範例 2 會傳回單一 Kerberos 帳戶指派的資訊：Redmond 網站的帳戶指派。

    Get-CsKerberosAccountAssignment -Identity "site:Redmond"

## 範例 3

範例 3 會傳回已經指派給字串值出現在其網站 Identity 的任何位置之網站的所有 Kerberos 帳戶相關資訊。作法是加入Filter 參數與篩選值 "\*Redmond"。

    Get-CsKerberosAccountAssignment -Filter "*Redmond*"

## 範例 4

範例 4 會傳回所有 Kerberos 帳戶指派的資訊，其中已指派之帳戶的身分識別會包含字串值 "litwareinc"。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsKerberosAccountAssignment** Cmdlet，以傳回目前所使用之所有 Kerberos 帳戶指派的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出帳戶的身分識別包含 "litwareinc" 字串值的帳戶指派。(請注意，儘管參數名稱為 UserAccount，但所指的帳戶實為電腦帳戶。)

    Get-CsKerberosAccountAssignment | Where-Object {$_.UserAccount -match "litwareinc"}

## 詳細描述

在 Microsoft Office Communications Server 2007 和 Microsoft Office Communications Server 2007 R2 中，IIS 會以標準使用者帳戶執行。但這可能會帶來許多問題，其中包括密碼過期時，您會遺失 Web 服務 這項很難診斷的問題。為避免過期密碼的問題，Lync Server 可讓您 (為實際上不存在的電腦) 建立電腦帳戶，並將其用為網站內執行 IIS 之所有電腦的驗證主體。因為這些帳戶使用 Kerberos 驗證通訊協定，所以帳戶稱為 Kerberos 帳戶，新驗證處理序別名 Kerberos Web 驗證。如此可讓您使用單一帳戶來管理所有 IIS 伺服器。

若要在這個新的驗證主體下執行伺服器，您必須先使用 **New-CsKerberosAccount** Cmdlet 建立電腦帳戶，然後將此帳戶指派給一或多個網站。完成指派後，請執行 **Enable-CsTopology** Cmdlet 來啟用帳戶與 Lync Server 網站之間的關聯。除此之外，還會在 Active Directory 網域服務 中建立所需之服務主體名稱 (SPN)。SPN 讓用戶端應用程式能夠找到特定的服務。

**Get-CsKerberosAccountAssignment** Cmdlet 可讓您傳回組織中目前所使用之 Kerberos 帳戶指派的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsKerberosAccountAssignment** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsKerberosAccountAssignment"}

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
<td><p>可讓您在指定要傳回的 Kerberos 帳戶指派時使用萬用字元。例如，下列語法會傳回包含字串值 &quot;Europe&quot;:-Filter &quot;*Europe*&quot;。</p>
<p>請勿在同一個命令中同時使用 Identity 和 Filter 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>已指派 Kerberos 帳戶之網站的唯一識別碼；例如：-Identity &quot;site:Redmond&quot;。(注意，這是該網站的 Identity，而非電腦帳戶的 Identity)。您無法在指定網站 Identity 時使用萬用字元。若要使用萬用字元，請改用 Filter 參數。</p>
<p>若未加入 Identity 和 Filter 參數，<strong>Get-CsKerberosAccountAssignment</strong> Cmdlet 會傳回設定供組織使用的所有 Kerberos 帳戶指派。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取 Kerberos 指派資料，而非從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsKerberosAccountAssignment** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsKerberosAccountAssignment** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.KerberosAccount.KerberosAccountAssignment 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsKerberosAccountAssignment](new-cskerberosaccountassignment.md)  
[Remove-CsKerberosAccountAssignment](remove-cskerberosaccountassignment.md)  
[Set-CsKerberosAccountAssignment](set-cskerberosaccountassignment.md)

