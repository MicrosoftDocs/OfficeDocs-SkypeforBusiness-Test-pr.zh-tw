---
title: Remove-CsTestUserCredential
TOCTitle: Remove-CsTestUserCredential
ms:assetid: 49290251-276d-41d5-bcfd-077018d74f59
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204870(v=OCS.15)
ms:contentKeyID: 49290814
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsTestUserCredential

 

_**上次修改主題的時間：** 2015-03-09_

從設為監看員節點測試使用者的使用者集合中移除指定的使用者。監看員節點是定期使用 Microsoft System Center Operations Manager 及 Lync Server 2013 綜合交易，以驗證 Lync Server 元件是否如預期運作的電腦。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Remove-CsTestUserCredential -SipAddress <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會從設為監看員節點測試使用者的使用者集合中，移除 SIP 位址為 sip:kenmyer@litwareinc.com 的使用者。

    Remove-CsTestUserCredential "sip:kenmyer@litwareinc.com"

## 範例 2

範例 2 所示的命令會移除已設為監看員節點測試使用者的所有使用者 (請注意，這不會刪除使用者帳戶，只會刪除為監看員節點測試使用者的狀態)。為達成此目的，範例中的第一個命令會將 Windows PowerShell $ErrorActionPreference 變數的值設為 "SilentlyContinue"；這會隱藏當 **Remove-CsTestUserCredential** Cmdlet 嘗試從尚未設為監看員節點測試使用者的使用者移除測試認證時，所出現的錯誤訊息。

在隱藏錯誤訊息的情況下，範例中的第二個命令會使用 **Get-CsUser** Cmdlet 傳回已啟用 Lync Server 2013之所有使用者的集合。然後，此集合會管線傳送到 **ForEach-Object** Cmdlet。**ForEach-Object** Cmdlet 會依序處理集合中的每個使用者帳戶，對每個帳戶執行 **Remove-CsTestUserCredential** Cmdlet，以移除做為監看員節點測試使用者的使用者。

範例中的最後一個命令會將 $ErrorActionPreference 的值重設為 "Continue"。

    $ErrorActionPreference = "SilentlyContinue"
    
    Get-CsUser | ForEach-Object {Remove-CsTestUserCredential -SipAddress $_.SipAddress}
    
    $ErrorActionPreference = "Continue"

## 詳細描述

若您是使用 System Center Operations Manager 與 Lync Server 2013，可以選擇設定「監看員節點」電腦。監看員節點是定期 (或自動) 執行綜合交易的電腦。綜合交易是指測試 Lync Server 各種功能的 Cmdlet。例如確認使用者能否登錄到 Lync Server 的綜合交易；驗證使用者能否使用 Lync Server 交換立即訊息與目前狀態資訊的綜合交易；驗證使用者能否進行資料共同作業與應用程式共用會議的綜合交易；以及驗證使用者能否在公用交換電話網路上撥打電話的綜合交易等等。一如前文所述，這些綜合交易會定期執行，如有任何失敗，還會發出警示通知系統管理員系統可能發生問題。

許多綜合交易都需要測試使用者。例如，您必須要有兩個使用者帳戶，並利用這兩個帳戶交換立即訊息，才能測試使用者之間是否能夠交換立即訊息。當您設定監看員節點時，您至少須指派兩位使用者給該節點。任何有效的 Active Directory 使用者帳戶只要能夠使用 Lync Server 2013 並已登錄為測試帳戶，都可以擔任測試使用者。若要登錄為測試帳戶，請使用 [Set-CsTestUserCredential](set-cstestusercredential.md) Cmdlet。若您之後決定不再使用某帳戶做為測試帳戶，可以使用 **Remove-CsTestUserCredential** Cmdlet 取消登錄該帳戶。此 Cmdlet 只可防止帳戶被用為監看員節點測試帳戶，而無法刪除、停用或修改帳戶。

若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsTestUserCredential"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Remove-CsTestUserCredential** Cmdlet 所執行的功能。

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
<td><p><em>SipAddress</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>要移除測試使用者認證之帳戶的 SIP 位址。例如：</p>
<p>-SipAddress &quot;sip:kenmyer@litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。</p></td>
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
<td><p>描述執行命令後的結果，但無須實際執行命令。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Remove-CsTestUserCredential** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。反之，**Remove-CsTestUserCredential** Cmdlet 會刪除現有的 System.Management.Automation.PSCredential 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsTestUserCredential](get-cstestusercredential.md)  
[Set-CsTestUserCredential](set-cstestusercredential.md)

