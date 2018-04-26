---
title: Get-CsTestUserCredential
TOCTitle: Get-CsTestUserCredential
ms:assetid: 2af8d526-005c-40fb-957c-5b2ee5bce432
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204759(v=OCS.15)
ms:contentKeyID: 49290407
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTestUserCredential

 

_**上次修改主題的時間：** 2015-03-09_

傳回可以讓您知道使用者是否已設為監看員節點測試使用者的資訊。監看員節點是定期使用 Microsoft System Center Operations Manager 2007 R2 及 Lync Server 2013 綜合交易，以驗證 Lync Server 元件是否如預期運作的電腦。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsTestUserCredential -SipAddress <String>

## 範例

## 範例 1

如果使用者 sip:kenmyer@litwareinc.com 已設定為監看員節點測試使用者，範例 1 顯示的命令會傳回該使用者的資訊。如果該使用者尚未設為測試使用者，則 **Get-CsTestUserCredential** Cmdlet 會傳回錯誤。

    Get-CsTestUserCredential -SipAddress "sip:kenmyer@litewareinc.com"

## 範例 2

範例 2 所示的命令會傳回已設為監看員節點測試使用者的所有使用者清單。為達成此目的，範例中的第一個命令會將 Windows PowerShell 命令列介面的 $ErrorActionPreference 變數值設為 "SilentlyContinue"；這會隱藏當 **Get-CsTestUserCredential** Cmdlet 嘗試針對尚未設為監看員節點測試使用者的使用者，傳回測試使用者資訊時，所顯示的任何錯誤訊息。

在隱藏錯誤訊息的情況下，範例中的第二個命令會使用 **Get-CsUser** Cmdlet 傳回已啟用 Lync Server 2013 之所有使用者的集合。然後，此集合會管線傳送到 **ForEach-Object** Cmdlet。**ForEach-Object** Cmdlet 會依序處理集合中的每個使用者帳戶，對每個帳戶執行 **Get-CsTestUserCredential** Cmdlet，以查看使用者是否已設為測試使用者。如果使用者已設為測試使用者，螢幕上會顯示該使用者的資訊。如果使用者尚未設為測試使用者，則螢幕上不會顯示任何資訊。

範例中的最後一個命令會將 $ErrorActionPreference 的值重設為 "Continue"。

    $ErrorActionPreference = "SilentlyContinue"
    Get-CsUser | ForEach-Object {Get-CsTestUserCredential -SipAddress $_.SipAddress}
    $ErrorActionPreference = "Continue"

## 詳細描述

若您是使用 System Center Operations Manager 與 Lync Server 2013，可以選擇設定「監看員節點」電腦。監看員節點是定期 (或自動) 執行綜合交易的電腦。綜合交易是指測試 Lync Server 各種功能的 Cmdlet。例如確認使用者能否登錄到 Lync Server 的綜合交易；驗證使用者能否使用 Lync Server 交換立即訊息與目前狀態資訊的綜合交易；驗證使用者能否進行資料共同作業與應用程式共用會議的綜合交易；以及驗證使用者能否在公用交換電話網路上撥打電話的綜合交易等等。一如前文所述，這些綜合交易會定期執行，如有任何失敗，還會發出警示通知系統管理員系統可能發生問題。

許多綜合交易都需要測試使用者。例如，您必須要有兩個使用者帳戶，並利用這兩個帳戶交換立即訊息，才能測試使用者之間是否能夠交換立即訊息。當您設定監看員節點時，您至少須指派兩位使用者給該節點。任何有效的 Active Directory 使用者帳戶只要能夠使用 Lync Server 2013並已登錄為測試帳戶，都可以擔任測試使用者。若要登錄為測試帳戶，請使用 [Set-CsTestUserCredential](set-cstestusercredential.md) Cmdlet。若您之後決定不再使用某帳戶做為測試帳戶，可以使用 [Remove-CsTestUserCredential](remove-cstestusercredential.md) Cmdlet 取消登錄該帳戶。此 Cmdlet 只可防止帳戶被用為監看員節點測試帳戶，而無法刪除、停用或修改帳戶。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsTestUserCredential"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Get-CsTestUserCredential** Cmdlet 所執行的功能。

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
<td><p>要檢查其測試使用者認證之帳戶的 SIP 位址。例如：</p>
<p>-SipAddress &quot;sip:kenmyer@litwareinc.com&quot;</p>
<p>在呼叫 <strong>Get-CsTestUserCredential</strong> Cmdlet 時，必須包含 SipAddress 參數。如果未包含，系統會提示您輸入該位址。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsTestUserCredential** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsTestUserCredential** Cmdlet 會傳回 System.Management.Automation.PSCredential 物件的執行個體。

## 請參閱

#### 其他資源

[Remove-CsTestUserCredential](remove-cstestusercredential.md)  
[Set-CsTestUserCredential](set-cstestusercredential.md)

