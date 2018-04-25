---
title: Set-CsTestUserCredential
TOCTitle: Set-CsTestUserCredential
ms:assetid: e613fad9-e91b-4bce-a67d-b1c9860ab34d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205341(v=OCS.15)
ms:contentKeyID: 49292629
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTestUserCredential

 

_**上次修改主題的時間：** 2015-03-09_

建立新的監看員節點測試使用者。監看員節點是定期使用 Microsoft System Center Operations Manager 及 Lync Server 2013 綜合交易，以驗證 Lync Server 元件是否如預期運作的電腦。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Set-CsTestUserCredential -Credential <PSCredential> <COMMON PARAMETERS>

    Set-CsTestUserCredential -Password <String> -UserName <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: -SipAddress <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將 SIP 位址為 sip:kenmyer@litwareinc.com 的使用者設定為監看員節點測試使用者。請注意，當您將帳戶設定為監看員節點測試使用者時，也必須提供使用者名稱 (以「網域名稱\\使用者名稱」的格式) 和密碼。

    Set-CsTestUserCredential -SipAddress "sip:kenmyer@litwareinc.com" -UserName "litwareinc\kenmyer" -Password "07Apples"

## 範例 2

上述範例所示的命令也會將 SIP 位址為 sip:kenmyer@litwareinc.com 的使用者設為監看員節點測試使用者，但此範例會使用 Credential 參數，而非 UserName 和 Password 參數。為達成此目的，範例中的第一個命令會使用 **Get-Credential** Cmdlet，以建立帳戶 litwareinc\\kenmyer 的 Windows PowerShell 命令列介面認證物件；然後將該認證物件儲存於名為 $x 的變數中 (請注意，建立認證物件時，必須提供 litwareinc\\kenmyer 帳戶的密碼)。範例中的第二個命令接著會使用 Credential 參數和參數值 $x 來設定測試認證。

    $x = Get-Credential "litwareinc\kenmyer"
    
    Set-CsTestUserCredential -SipAddress "sip:kenmyer@litwareinc.com" -Credential $x

## 詳細描述

若您是使用 System Center Operations Manager 與 Lync Server 2013，可以選擇設定「監看員節點」電腦。監看員節點是定期 (且自動) 執行綜合交易的電腦。綜合交易是指測試 Lync Server 各種功能的 Cmdlet。例如確認使用者能否登錄到 Lync Server 的綜合交易；驗證使用者能否使用 Lync Server 交換立即訊息與目前狀態資訊的綜合交易；驗證使用者能否進行資料共同作業與應用程式共用會議的綜合交易；以及驗證使用者能否在公用交換電話網路上撥打電話的綜合交易等等。一如前文所述，這些綜合交易會定期執行，如有任何失敗，還會發出警示通知系統管理員系統可能發生問題。

許多綜合交易都需要測試使用者。例如，您必須要有兩個使用者帳戶，並嘗試利用這兩個帳戶交換立即訊息，才能測試兩位使用者之間是否能夠交換立即訊息。當您設定監看員節點時，至少必須指派兩位使用者給該節點。任何有效的 Active Directory 使用者帳戶只要能夠使用 Lync Server 2013 並已登錄為測試帳戶，都可以擔任測試使用者。若要登錄為測試帳戶，請使用 **Set-CsTestUserCredential** Cmdlet。若您之後決定不再使用某帳戶做為測試帳戶，可以使用 [Remove-CsTestUserCredential](remove-cstestusercredential.md) Cmdlet 取消登錄該帳戶。此 Cmdlet 只可防止帳戶被用來做為監看員節點測試帳戶，而無法刪除、停用或修改帳戶。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsTestUserCredential"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Set-CsTestUserCredential** Cmdlet 所執行的功能。

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
<td><p><em>Credential</em></p></td>
<td><p>必要</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>可讓您使用 Windows PowerShell 認證物件 (而不是 Password 和 UserName 參數) 設定測試認證，此作法可確保在螢幕上輸入使用者密碼時，會將密碼進行遮罩處理。</p>
<p>若要使用 Credential 參數，您必須先使用 <strong>Get-Credential</strong> Cmdlet 建立 PSCredential 物件，然後將產生的物件儲存於變數中。例如：</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>接著再將此變數用為 Credential 參數的參數值。</p></td>
</tr>
<tr class="even">
<td><p><em>Password</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>設定測試使用者認證之帳戶的密碼 (請注意，此密碼在螢幕上會以純文字顯示)。例如：</p>
<p>-Password &quot;p@ssw0rd&quot;</p>
<p>如果使用 Credential 參數，便無須使用 Password 或 UserName 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>SipAddress</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>設定測試使用者認證之帳戶的 SIP 位址。例如：</p>
<p>-SipAddress &quot;sip:kenmyer@litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>UserName</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>設定用於測試認證之帳戶的使用者名稱。使用者名稱可以是 SamAccountName 或 Active Directory DisplayName，例如：</p>
<p>-UserName &quot;Ken Myer&quot;</p>
<p>您也可以使用「網域名稱\使用者名稱」格式指定 UserName。例如：</p>
<p>-UserName &quot;litwareinc\kenmyer&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>描述執行命令後的結果，但無須實際執行命令。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Set-CsTestUserCredential** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。反之，**Set-CsTestUserCredential** Cmdlet 會修改現有的 System.Management.Automation.PSCredential 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsTestUserCredential](get-cstestusercredential.md)  
[Remove-CsTestUserCredential](remove-cstestusercredential.md)

