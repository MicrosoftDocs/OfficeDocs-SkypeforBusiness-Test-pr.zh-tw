---
title: Set-CsKerberosAccountPassword
TOCTitle: Set-CsKerberosAccountPassword
ms:assetid: 837292b9-3c08-4c3c-a49d-3f9492518ddd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398659(v=OCS.15)
ms:contentKeyID: 49291515
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsKerberosAccountPassword

 

_**上次修改主題的時間：** 2015-03-09_

從指派有 Kerberos 帳戶的網站中找出所有執行 Web 服務的伺服器，然後更新這些伺服器上的 Internet Information Service (IIS) 組態設定。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsKerberosAccountPassword -UserAccount <String> <COMMON PARAMETERS>

    Set-CsKerberosAccountPassword -FromComputer <Fqdn> -ToComputer <Fqdn> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會設定 Kerberos 帳戶 litwareinc\\kerberostest 的密碼。

    Set-CsKerberosAccountPassword -UserAccount "litwareinc\kerberostest"

## 範例 2

在範例 2 中，已將 Kerberos 帳戶密碼從電腦 atl-cs-001.litwareinc.com 複製到電腦 dublin-cs-001.litwareinc.com。

    Set-CsKerberosAccountPassword -FromComputer "atl-cs-001.litwareinc.com" -ToComputer "dublin-cs-001.litwareinc.com"

## 詳細描述

在 Microsoft Office Communications Server 2007 和 Microsoft Office Communications Server 2007 R2 中，IIS 會以標準使用者帳戶執行。但這可能會帶來許多問題，其中包括密碼過期時，您會遺失 Web 服務這項很難診斷的問題。為避免過期密碼的問題，Lync Server 可讓您 (為實際上不存在的電腦) 建立電腦帳戶，並將其用為網站內執行 IIS 之所有電腦的驗證主體。因為這些帳戶使用 Kerberos 驗證通訊協定，所以帳戶稱為 Kerberos 帳戶，新驗證處理序別名 Kerberos Web 驗證。如此可讓您使用單一帳戶來管理所有 IIS 伺服器。

若要在這個新的驗證主體下執行伺服器，您必須先使用 **New-CsKerberosAccount** Cmdlet 建立電腦帳戶，然後將此帳戶指派給一或多個網站。完成指派後，請執行 **Enable-CsTopology** Cmdlet 來啟用帳戶與 Lync Server 網站之間的關聯。除此之外，還會在 Active Directory 網域服務 中建立所需之服務主體名稱 (SPN)。SPN 讓用戶端應用程式能夠找到特定的服務。

建立新的關聯之後，**Set-CsKerberosAccountPassword** Cmdlet 會提供一種方法來修改指派給帳戶的密碼，以及 (同等重要的) 在使用特定 Kerberos 測試帳戶來進行 Kerberos Web 驗證的每部電腦上更新密碼。

此外，此 Cmdlet 亦可使用 ToComputer 和 FromComputer 參數，將此組態資訊從某部電腦複製到另一部電腦。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsKerberosAccountPassword** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsKerberosAccountPassword"}

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
<td><p><em>FromComputer</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>要將 Kerberos 帳戶密碼複製到另一部電腦之電腦的完整網域名稱 (FQDN)。如果您使用 UserAccount 參數，則無法使用此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>ToComputer</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>要在其中複製 Kerberos 帳戶密碼的電腦 FQDN。如果您使用 UserAccount 參數，則無法使用此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserAccount</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>應變更密碼之帳戶的帳戶名稱。此帳戶名稱必須使用「網域名稱\使用者名稱」的格式；例如：-UserAccount &quot;litwareinc\kerberostest&quot;。</p>
<p>請注意，除了名稱 UserAccount，此帳戶實際上是電腦帳戶，不是使用者帳戶。</p></td>
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
<td><p>隱藏顯示當執行命令時可能發生的任何非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\SetKerberosPassword.html&quot;。</p></td>
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

無。

## 傳回類型

**Set-CsKerberosAccountPassword** Cmdlet 不會傳回任何物件或值，而會修改現有的 Microsoft.Rtc.Management.WritableConfig.Settings.KerberosAccount.KerberosAccount 物件執行個體。

