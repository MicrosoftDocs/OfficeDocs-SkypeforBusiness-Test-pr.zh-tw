---
title: Get-CsWebServiceConfiguration
TOCTitle: Get-CsWebServiceConfiguration
ms:assetid: 28582668-839c-4b04-8211-928c91634672
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425751(v=OCS.15)
ms:contentKeyID: 49290417
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsWebServiceConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織所使用之所有 Web 服務組態設定的資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsWebServiceConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsWebServiceConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 會傳回組織目前所使用之所有 Web 服務組態設定的資訊。

    Get-CsWebServiceConfiguration

## 範例 2

範例 2 所示的命令傳回 Identity 為 site:Redmond 的 Web 服務 組態設定資訊。

    Get-CsWebServiceConfiguration -Identity site:Redmond

## 範例 3

範例 3 傳回網站範圍指派的所有 Web 服務 組態設定。為達成此目的，會在呼叫 **Get-CsWebServiceConfiguration** Cmdlet 時加入 Filter 參數；篩選值 "site:\*" 確保只有 Identity 以字串值 "site:" 為開頭的那些設定才會傳回。

    Get-CsWebServiceConfiguration -Filter "site:*"

## 範例 4

範例 4 的命令會傳回所有不允許個人識別碼 (PIN) 驗證的 Web 服務組態設定。作法是先呼叫 **Get-CsWebServiceConfiguration** Cmdlet 傳回目前所使用的所有 Web 服務 組態設定。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 UsePinAuth 屬性等於 False 的設定。

    Get-CsWebServiceConfiguration | Where-Object {$_.UsePinAuth -eq $False}

## 範例 5

範例 5 會傳回最大群組擴充大小大於 100 的所有 Web 服務組態設定。為達成此目的，命令會先使用 **Get-CsWebServiceConfiguration** Cmdlet 傳回目前所使用的所有 Web 服務組態設定。接著，此資訊會管線傳送到 **Where-Object** Cmdlet，這會只選取 MaxGroupSizeToExpand 屬性大於 100 的設定。

    Get-CsWebServiceConfiguration | Where-Object {$_.MaxGroupSizeToExpand -gt 100}

## 詳細描述

許多 Lync Server 元件為 Web 元件：這些元件使用 Web 服務或網頁來執行工作。例如，使用者利用 Web 服務搜尋通訊錄的新連絡人，或使用群組擴充來檢視通訊群組的個別成員。同樣地，從電話撥入式會議到 Lync Server 控制台等元件都是使用網頁做為 Lync Server 和使用者之間的介面。

**CsWebServiceConfiguration** Cmdlet 可讓系統管理員管理整個組織的 Web 服務組態設定，包括群組擴充、憑證設定及允許之驗證方法等項目的管理。因為您可以在全域、網站和服務範圍設定不同的設定 (雖然只針對 Web Services 服務)，所以可以為不同的使用者和不同的位置自訂 Web 服務 功能。

**Get-CsWebServiceConfiguration** Cmdlet 可讓您傳回目前所使用之 Web 服務 組態設定的詳細資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsWebServiceConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsWebServiceConfiguration"}

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
<td><p>可讓您在指定要傳回的 Web 服務 組態設定集合時使用萬用字元。例如，此語法會傳回網站範圍設定的所有設定：-Filter &quot;site:*&quot;。</p>
<p>您無法在同一個命令中同時使用 Filter 與 Identity 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要傳回之 Web 服務 組態設定的唯一識別碼。若要傳回全域設定，請使用下列語法：-Identity global。若要傳回在此網站範圍設定的設定，請使用下列語法：-Identity &quot;site:Redmond.&quot;可使用下列語法傳回 Service-scope 設定：-Identity &quot;service:WebServer:atl-cs-001.litwareinc.com&quot;。</p>
<p>您無法在同一個命令中同時使用 Filter 與 Identity 參數。如果您沒有指定其中一個參數，<strong>Get-CsWebServiceConfiguration</strong> Cmdlet 會傳回組織中目前所使用之所有 Web 服務 設定的集合。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區本機複本擷取 Web 服務組態資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsWebServiceConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsWebServiceConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Web.WebServiceSettings 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsWebServiceConfiguration](new-cswebserviceconfiguration.md)  
[Remove-CsWebServiceConfiguration](remove-cswebserviceconfiguration.md)  
[Set-CsWebServiceConfiguration](set-cswebserviceconfiguration.md)

