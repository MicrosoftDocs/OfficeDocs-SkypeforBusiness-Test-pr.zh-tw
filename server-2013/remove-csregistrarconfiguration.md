---
title: Remove-CsRegistrarConfiguration
TOCTitle: Remove-CsRegistrarConfiguration
ms:assetid: 67ee01a1-fdfe-4994-b03a-57a332aa45be
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398482(v=OCS.15)
ms:contentKeyID: 49291178
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsRegistrarConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除現有的登錄器組態設定集合。登錄器可用於驗證登入要求，以及維護使用者狀態與顯示狀態的資訊。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsRegistrarConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會刪除指派給 Redmond 網站的登錄器組態設定。刪除這些設定時，Redmond 網站中的登錄器將會自動使用全域登錄器設定。

    Remove-CsRegistrarConfiguration -Identity site:Redmond

## 範例 2

範例 2 會刪除已指派給服務範圍的所有登錄器組態設定。為達此目的，命令會先呼叫 **Get-CsRegistrarConfiguration** Cmdlet 並搭配 Filter 參數；篩選值 "service:\*" 將傳回的資料限制在 Identity 開頭字元為 "service:" 的設定。接著將篩選後的集合管線傳送到 **Remove-CsRegistrarConfiguration** Cmdlet，以刪除該集合中的每個項目。

    Get-CsRegistrarConfiguration -Filter "service:*" | Remove-CsRegistrarConfiguration

## 範例 3

範例 3 會刪除 EnableDHCPServer 屬性為 True 的所有登錄器組態設定。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsRegistrarConfiguration** Cmdlet，以傳回目前使用之所有登錄器組態設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 EnableDHCPServer 屬性等於 True 的設定。接著將篩選後的集合管線傳送到 **Remove-CsRegistrarConfiguration** Cmdlet，以刪除集合中的每個項目。

    Get-CsRegistrarConfiguration | Where-Object {$_.EnableDHCPServer -eq $True} | Remove-CsRegistrarConfiguration

## 詳細描述

登錄器可能是 Lync Server 中最重要的元件；畢竟，若無登錄器，使用者將無法登入系統，且 Lync Server 也無法追蹤使用者及其目前的狀態。當使用者登入 Lync Server 時，使用者從中登入的端點會傳送 REGISTER 要求給登錄器；而伺服器則以要求用戶端裝置提出驗證認證做為回應。如果用戶端通過此挑戰 (即用戶端出示一組有效認證)，則使用者通過驗證，而且端點資訊 (例如 IP 位址、連接埠和使用者名稱) 會記錄到註冊資料庫中。當使用者登出時，這項資訊便會從資料庫移除。在登入後與登出前的這段時間，登錄器會保持最新的狀態資訊，並協助路由要給該使用者和該使用者傳來的訊息。

登錄器組態設定用於協助管理端點與端點訂閱；這些設定可以在全域、網站或服務範圍內套用。(服務範圍的設定僅能搭配登錄程式服務使用)。

**Remove-CsRegistrarConfiguration** Cmdlet 可讓您移除已在網站範圍或服務範圍套用的登錄器組態設定。請注意，這不會刪除或解除安裝任何登錄程式；它只會移除管理那些登錄程式的組態設定。如果這些設定不存在於網站範圍或服務範圍，則會使用全域設定管理登錄器。

**Remove-CsRegistrarConfiguration** Cmdlet 也可以針對通用登錄器組態設定來執行。不過，在該情況下將不會移除設定；因為您無法刪除全域設定，而是將該全域集合中的所有屬性重設為預設值。例如，如果您已將 MinEndpointExpiration 屬性的值變更為 500，該值將會重設回 300。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsRegistrarConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsRegistrarConfiguration e"}

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
<td><p>要移除之登錄器組態設定的唯一識別碼。若要移除在網站範圍設定的設定，請使用類似下列的語法：-Identity site:Redmond。若要移除服務層級的設定，請使用類似下列的語法：-Identity service:Registar:atl-cs-001.litwareinc.com。</p>
<p>請注意， <strong>Remove-CsRegistrarConfiguration</strong> Cmdlet 也可以針對全域設定 (-Identity global) 來執行。不過，在該情況下將不會移除全域設定，而是將全域集合中的所有屬性重設為預設值。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.Registrar.RegistrarSettings 物件。 **Remove-CsRegistrarConfiguration** Cmdlet 接受管線傳送的登錄器設定物件執行個體。

## 傳回類型

無。反之， **Remove-CsRegistrarConfiguration** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.WritableConfig.Settings.Registrar.RegistrarSettings 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsRegistrarConfiguration](get-csregistrarconfiguration.md)  
[New-CsRegistrarConfiguration](new-csregistrarconfiguration.md)  
[Set-CsRegistrarConfiguration](set-csregistrarconfiguration.md)

