---
title: Remove-CsDiagnosticHeaderConfiguration
TOCTitle: Remove-CsDiagnosticHeaderConfiguration
ms:assetid: d71b79f1-49f2-4a6c-8b3e-ca909e8d5f49
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398941(v=OCS.15)
ms:contentKeyID: 49292445
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsDiagnosticHeaderConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

刪除組織目前所使用的一或多個診斷標頭組態設定集合。診斷標頭組態設定可指定是否要在 SIP 訊息中加入標頭資訊，以供疑難排解及錯誤報告時使用。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsDiagnosticHeaderConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會移除 Identity 為 site:Redmond 的診斷標頭組態設定。

    Remove-CsDiagnosticHeaderConfiguration -Identity site:Redmond

## 範例 2

範例 2 所示的命令會刪除已在服務範圍套用的所有診斷標頭組態設定。為成達此目的，命令會先呼叫 **Get-CsDiagnosticHeaderConfiguration** Cmdlet 搭配 Filter 參數。篩選值 "service:\*" 會將傳回的資料限制在 Identity 開頭為 "service:" 字元的設定。然後將此篩選後的集合管線傳送到 **Remove-CsDiagnosticHeaderConfiguration** Cmdlet，以刪除集合中的每一個項目。

    Get-CsDiagnosticHeaderConfiguration -Filter service:* | Remove-CsDiagnosticHeaderConfiguration

## 範例 3

範例 3 會刪除所有允許傳送到外部網路的診斷標頭組態設定。為達成此目的，命令會先使用 **Get-CsDiagnosticHeaderConfiguration** Cmdlet 傳回目前使用的所有診斷標頭設定集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 SendToExternalNetworks 屬性等於 True 的設定。接著將這些設定管線傳送到 **Remove-CsDiagnosticHeaderConfiguration** Cmdlet，以刪除允許傳送到外部網路的每一個設定。

    Get-CsDiagnosticHeaderConfiguration | Where-Object {$_.SendToExternalNetworks -eq $True} | Remove-CsDiagnosticHeaderConfiguration

## 詳細描述

系統管理員可以選擇在每則傳送到組織的 SIP 訊息上附加 ms-diagnostics 標頭。此訊息 (一般使用者看不到) 包含有助於疑難排解連線問題或報告錯誤的資訊。例如，發生特定的狀況時，診斷標頭中的錯誤碼可讓用戶端應用程式採取預先決定的動作。

若是在內部網路內傳送的 SIP 訊息，有幾個理由可以不包含這些診斷標頭：它們對訊息大小的影響最小，且對於要解決連線問題的系統管理員來說可能是沒價值的工具。但是，診斷標頭也包含了一些您可能不想讓內部網路以外人員看到的資訊，像是 SIP 伺服器的完整網域名稱 (FQDN)。因此，診斷標頭組態設定可讓您決定是否傳送診斷標頭給外部網路使用者 (例如，同盟網域的使用者) 和/或外部使用者 (外部使用者係指從內部網路之外進行連線，且尚未經過驗證的使用者)。

或者，您可以在網站範圍或服務範圍 (針對 Edge Server 或登錄器服務) 建立自訂設定。這樣一來，您就可以選擇包含從某一個網站或經由某一個 Edge Server 傳送的訊息診斷標頭，同時不允許從其他網站或經由其他 Edge Server 傳送的訊息診斷標頭。

不論是在網站範圍或服務範圍內建立的新集合，您都可以在稍後使用 **Remove-CsDiagnosticHeaderConfiguration** Cmdlet 予以移除。您也可以針對全域集合執行此 Cmdlet。但在此情況下，全域集合並不會遭到移除，原因在於您無法移除全域集合。而是會將全域集合中的兩個屬性 (SendToExternalNetworks 和 SendToOutsideUnauthenticatedUsers) 重設為預設值 (兩者皆為 False)。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsDiagnosticHeaderConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsDiagnosticHeaderConfiguration"}

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
<td><p>要移除之診斷標頭組態設定的唯一識別碼。若要移除在此網站範圍設定的設定，請使用類似下列的語法：-Identity &quot;site:Redmond&quot;。若要移除在服務範圍設定的設定，請使用下列語法：-Identity &quot;service:EdgeServer:atl-edge-001.litwareinc.com&quot;。</p>
<p><strong>Remove-CsDiagnosticHeaderConfiguration</strong> Cmdlet 也可以針對全域組態設定來執行；在該情況下，請使用下列語法：–Identity global。不過，請注意，不會實際移除全域設定；但是，會將在全域設定中找到的屬性重設為其預設值。</p></td>
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
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Settings.Diagnostics.DiagnosticHeaderSettings 物件。**Remove-CsDiagnosticHeaderConfiguration** Cmdlet 接受診斷標頭設定物件的管線執行個體。

## 傳回類型

無。反之，**Remove-CsDiagnosticHeaderConfiguration** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.WritableConfig.Settings.Diagnostics.DiagnosticHeaderSettings 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsDiagnosticHeaderConfiguration](get-csdiagnosticheaderconfiguration.md)  
[New-CsDiagnosticHeaderConfiguration](new-csdiagnosticheaderconfiguration.md)  
[Set-CsDiagnosticHeaderConfiguration](set-csdiagnosticheaderconfiguration.md)

