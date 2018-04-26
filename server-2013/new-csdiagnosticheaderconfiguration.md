---
title: New-CsDiagnosticHeaderConfiguration
TOCTitle: New-CsDiagnosticHeaderConfiguration
ms:assetid: 5322e63e-c02c-4dec-8206-04f701258d6b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398350(v=OCS.15)
ms:contentKeyID: 49290927
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsDiagnosticHeaderConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

建立新的診斷標頭組態設定集合。診斷標頭組態設定可指定是否要在 SIP 訊息中加入可用於疑難排解及錯誤報告的標頭資訊。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsDiagnosticHeaderConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-SendToExternalNetworks <$true | $false>] [-SendToOutsideUnauthenticatedUsers <$true | $false>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會建立 Redmond 網站 (-Identity site:Redmond) 的新診斷標頭組態。除了指定 Identity，命令還使用 SendToOutsideAuthenticatedUsers 參數和參數值 $True；這可讓資訊傳送給不在內部網路中之已驗證的使用者。

    New-CsDiagnosticHeaderConfiguration -Identity site:Redmond -SendToOutsideUnauthenticatedUsers $True

## 範例 2

範例 2 所示的命令會示範如何建立最初只存在於記憶體內的診斷標頭設定集合。為達成此目的，範例中的第一個命令會呼叫 **New-CsDiagnosticHeaderConfiguration** Cmdlet 並使用 Identity 和 InMemorys 參數。產生的物件會儲存在 $x 變數中。

建立虛擬設定後，命令 2 和 3 可分別用來修改 SendToOutsideUnauthenticatedUsers 和 SendToExternalNetworks 屬性的值。最後，命令 4 用來將虛擬診斷標頭組態設定轉換為套用到 Redmond 網站的實際設定集合。請注意，最後一個命令是必要項目。如果您沒有呼叫 **Set-CsDiagnosticHeaderConfiguration** Cmdlet，則不會將設定套用至網站，而且只要您結束 Windows PowerShell 工作階段或刪除變數 $x，虛擬設定就會消失。

    $x = New-CsDiagnosticHeaderConfiguration -Identity site:Redmond -InMemory
    $x.SendToOutsideUnauthenticatedUsers = $True
    $x.SendToExternalNetworks = $True
    Set-CsDiagnosticHeaderConfiguration -Instance $x

## 詳細描述

系統管理員可選擇將 ms-diagnostic 標頭附加至每則於組織內傳送的 SIP 訊息。此訊息 (一般使用者看不到) 包含有助於疑難排解連線問題或報告錯誤的資訊。例如，診斷標頭可包含啟用用戶端應用程式 (例如 Lync) 的錯誤代碼，以在發生特定情況時採取預先決定動作。

若是在內部網路內傳送的 SIP 訊息，有幾個理由可以不包含這些診斷標頭：它們對訊息大小的影響最小，且對於要解決連線問題的系統管理員來說可能是沒價值的工具。但是，診斷標頭也包含了一些您可能不想讓內部網路以外人員看到的資訊，像是 SIP 伺服器的完整網域名稱 (FQDN)。因此，診斷標頭組態設定可讓您決定是否傳送診斷標頭給外部網路使用者 (例如，同盟網域的使用者) 和/或外部使用者 (外部使用者係指從內部網路之外進行連線，且尚未經過驗證的使用者)。

根據預設，診斷標頭不會包含在傳送給外部網路或未驗證的使用者的訊息中。不過，您可以修改全域診斷標頭設定，以將標頭包含在給外部網路和/或未驗證的使用者的訊息中。或者，您可以在網站範圍或服務範圍 (針對 Edge Server 或登錄器服務) 建立自訂設定。這樣一來，您就可以選擇包含從某一個網站或經由某一個 Edge Server 傳送的訊息診斷標頭，同時不允許從其他網站或經由其他 Edge Server 傳送的訊息診斷標頭。

使用 **New-CsDiagnosticHeaderConfiguration** Cmdlet 建立自訂的診斷標頭設定。如上述，可在網站範圍或服務範圍上建立新設定 (雖然只針對 Edge Server 和登錄器服務)。請記住，每一個網站或服務只能有一個這種設定集合。例如，假設您嘗試建立 Redmond 網站的新集合，而該網站已託管一個診斷標頭設定集合。在這種情況下，您的命令會失敗。同樣地，如果您嘗試在全域範圍建立新集合，您的命令會失敗。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsDiagnosticHeaderConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsDiagnosticHeaderConfiguration"}

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
<td><p>要建立之診斷標頭組態設定的唯一識別碼。若要在網站範圍建立新設定集合，請使用如下語法：-Identity &quot;site:Redmond&quot;。若要在服務範圍建立新設定集合，請使用如下語法：-Identity &quot;service:EdgeServer:atl-cs-001.litwareinc.com&quot;。</p>
<p>您無法在全域範圍建立新設定。此外，如果指定的網站或服務 (例如，site:Redmond) 已託管設定集合，則您無法在網站或服務範圍建立新設定。</p></td>
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
<td><p><em>SendToExternalNetworks</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若設為 True，系統就會在傳送給外部使用者的訊息中附加診斷標頭。</p></td>
</tr>
<tr class="even">
<td><p><em>SendToOutsideUnauthenticatedUsers</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，會在傳送給外部使用者的訊息附加診斷標頭。外部使用者係指從內部網路之外進行連線 (例如，經由 Proxy 伺服器)，且尚未經過驗證的使用者。</p>
<p>預設值為 False。</p></td>
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

無。**New-CsDiagnosticHeaderConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsDiagnosticHeaderConfiguration** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.Diagnostics.DiagnosticHeaderSettings 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsDiagnosticConfiguration](get-csdiagnosticconfiguration.md)  
[Remove-CsDiagnosticHeaderConfiguration](remove-csdiagnosticheaderconfiguration.md)  
[Set-CsDiagnosticHeaderConfiguration](set-csdiagnosticheaderconfiguration.md)

