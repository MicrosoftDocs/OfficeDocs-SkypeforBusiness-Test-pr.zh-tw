---
title: Test-CsKerberosAccountAssignment
TOCTitle: Test-CsKerberosAccountAssignment
ms:assetid: 442bbb32-7ad1-40c4-bf17-42ecde0a7286
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425938(v=OCS.15)
ms:contentKeyID: 49290753
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsKerberosAccountAssignment

 

_**上次修改主題的時間：** 2015-03-09_

驗證指派給網站之 Kerberos 帳戶的設定。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Test-CsKerberosAccountAssignment -Identity <XdsIdentity> [-Report <String>]

## 範例

## 範例 1

範例 1 所示的命令會驗證指派給 Redmond 網站的 Kerberos 帳戶已正確設定，並如預期般運作。

    Test-CsKerberosAccountAssignment -Identity site:Redmond

## 詳細描述

在 Microsoft Office Communications Server 2007 和 Microsoft Office Communications Server 2007 R2 中，IIS 會以標準使用者帳戶執行。但這可能會帶來許多問題，其中包括密碼過期時，您會遺失 Web 服務這項很難診斷的問題。為避免過期密碼的問題，Lync Server 可讓您 (為實際上不存在的電腦) 建立電腦帳戶，並將其用為網站內執行 IIS 之所有電腦的驗證主體。因為這些帳戶使用 Kerberos 驗證通訊協定，所以帳戶稱為 Kerberos 帳戶，新驗證處理序別名 Kerberos Web 驗證。如此可讓您使用單一帳戶來管理所有 IIS 伺服器。

**Test-CsKerberosAccountAssignment** Cmdlet 可讓您驗證 Kerberos 帳戶是否已與指定網站相關聯、此帳戶是否已正確設定，以及此帳戶是否如預期般運作。

誰可以執行這個 Cmdlet：若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsKerberosAccountAssignment"}

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
<td><p>已指派 Kerberos 帳戶之網站的名稱。例如：-Identity &quot;site:Redmond&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\TestKerberos.html&quot;。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Test-CsKerberosAccountAssignment** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Test-CsKerberosAccountAssignment** Cmdlet 不會傳回任何物件或值。

## 請參閱

#### 其他資源

[Get-CsKerberosAccountAssignment](get-cskerberosaccountassignment.md)  
[New-CsKerberosAccountAssignment](new-cskerberosaccountassignment.md)  
[Remove-CsKerberosAccountAssignment](remove-cskerberosaccountassignment.md)  
[Set-CsKerberosAccountAssignment](set-cskerberosaccountassignment.md)

