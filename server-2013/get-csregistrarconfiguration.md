---
title: Get-CsRegistrarConfiguration
TOCTitle: Get-CsRegistrarConfiguration
ms:assetid: 67f2caf6-84a8-46d8-b034-7161e9841ab8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398483(v=OCS.15)
ms:contentKeyID: 49291177
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsRegistrarConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織目前所使用之登錄器組態設定的資訊。登錄器可用於驗證登入要求，以及維護使用者狀態與顯示狀態的資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsRegistrarConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsRegistrarConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回在組織中使用之所有登錄器組態設定的集合。

    Get-CsRegistrarConfiguration

## 範例 2

範例 2 會傳回登錄器組態設定的單一集合：為 Redmond 網站設定的設定 (-Identity site:Redmond)。

    Get-CsRegistrarConfiguration -Identity site:Redmond

## 範例 3

範例 3 會傳回在服務範圍指派之所有登錄器組態設定的資訊。為達此目的，命令會使用 Filter 參數及篩選值 "service:\*" (此篩選值可確保只會傳回 Identity 開頭為字串值 "service:" 的設定)。

    Get-CsRegistrarConfiguration -Filter "service:*"

## 範例 4

範例 4 會傳回關於啟用 DHCP 伺服器以登錄用戶端之登錄器組態設定的資訊。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsRegistrarConfiguration** Cmdlet，以傳回目前使用之所有登錄器組態設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 EnableDHCPServer 屬性等於 True 的設定。

    Get-CsRegistrarConfiguration | Where-Object {$_.EnableDHCPServer -eq $True}

## 範例 5

範例 5 會傳回允許每位使用者使用 8 個以上端點之所有登錄器組態設定的資訊。為達成此目的，命令會先使用 **Get-CsRegistrarConfiguration** Cmdlet，以傳回組織中所使用之所有登錄器組態設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，以挑出 MaxEndpointsPerUser 屬性大於 8 的設定。

    Get-CsRegistrarConfiguration | Where-Object {$_.MaxEndpointsPerUser -gt 8}

## 詳細描述

登錄器可說是 Lync Server 中最重要的元件，因為若無登錄器，使用者將無法登入系統，Lync Server 也無法追蹤使用者及其目前的狀態。當使用者登入 Lync Server 時，使用者用於登入的端點會傳送 REGISTER 要求給登錄器，而伺服器則會以要求用戶端裝置提出驗證認證做為回應。如果用戶端通過驗證 (亦即，如果用戶端呈現一組有效的認證)，即表示使用者通過驗證，而該端點的資訊 (例如 IP 位址、連接埠與使用者名稱等等) 也會一併記錄到登錄資料庫中。當使用者一登出，此資訊會隨即從資料庫移除。在登入後與登出前的這段時間，登錄器會隨時保持最新的狀態資訊，以路由進出使用者端的訊息。

登錄器組態設定用於協助管理端點與端點訂閱；這些設定可以在全域、網站或服務範圍內套用。(服務範圍的設定僅能搭配登錄程式服務使用)。**Get-CsRegistrarConfiguration** Cmdlet 可用於傳回關於組織中目前使用之所有登錄器組態集合的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsRegistrarConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsRegistrarConfiguration"}

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
<td><p>可讓您使用萬用字元傳回一或多個登錄器組態設定集合。例如，若要傳回在網站範圍所設定的所有設定，請使用下列語法：-Filter &quot;site:*&quot;。若要傳回在服務範圍所設定的所有設定，請使用下列語法：-Filter &quot;service:*&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要傳回之登錄器組態設定的唯一識別碼。若要傳回全域設定，請使用下列語法：-Identity global。若要傳回在網站範圍設定的設定，請使用類似下列的語法：-Identity site:Redmond。若要傳回服務層級的設定，請使用類似下列的語法：-Identity service:Registrar:atl-cs-001.litwareinc.com。</p>
<p>如果省略此參數，則 <strong>Get-CsRegistrarConfiguration</strong> Cmdlet 會傳回組織中目前使用的所有登錄器組態設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區 的本機複本擷取登錄器組態設定資料，而非從 中央管理存放區 本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsRegistrarConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsRegistrarConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.Registrar.RegistrarSettings 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsRegistrarConfiguration](new-csregistrarconfiguration.md)  
[Remove-CsRegistrarConfiguration](remove-csregistrarconfiguration.md)  
[Set-CsRegistrarConfiguration](set-csregistrarconfiguration.md)

