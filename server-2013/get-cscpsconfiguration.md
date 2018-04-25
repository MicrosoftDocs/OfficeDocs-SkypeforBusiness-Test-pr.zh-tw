---
title: Get-CsCpsConfiguration
TOCTitle: Get-CsCpsConfiguration
ms:assetid: d81ee8fe-d02b-4f60-a4d5-6aa84f65d156
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398948(v=OCS.15)
ms:contentKeyID: 49292489
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsCpsConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回通話駐留服務的資訊。通話駐留是可以讓使用者「駐留」來電的服務。駐留通話會將來電轉接到指定範圍或軌道內的號碼，然後立即將來電設為保留。任何人 (不只是原來接聽電話的人) 只要輸入正確的號碼，即可從系統的任何電話回復通話。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsCpsConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsCpsConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 會擷取定義在您組織中使用之所有通話駐留服務組態的集合。

    Get-CsCpsConfiguration

## 範例 2

範例 2 只會擷取 Identity 為 site:Redmond1 的通話駐留服務組態。

    Get-CsCpsConfiguration -Identity site:Redmond1

## 範例 3

在範例 3 中，Filter 參數可用來傳回已在網站範圍設定的所有通話駐留服務組態。萬用字元 site:\* 會指示 **Get-CsCpsConfiguration** Cmdlet 只傳回 Identity 開頭為 site: 字串值的設定。

    Get-CsCpsConfiguration -Filter site:*

## 範例 4

如同範例 3，我們在這個範例中使用 Filter 參數來擷取所有已定義之通話保留服務組態的子集。在此範例中，我們以字串 ":re" 進行篩選，這會傳回名稱開頭是 re 字母之所有網站的通話駐留設定，例如 Redmond1、Redmond2 和 RemoteComputer。

    Get-CsCpsConfiguration -Filter *:re*

## 範例 5

範例 5 會傳回來電者等候時未播放音樂的所有通話駐留服務設定。為達成此目的，命令會先使用 **Get-CsCpsConfiguration** Cmdlet，以擷取設定供組織使用的所有通話駐留服務設定。然後，此集合會管線傳送到 **Where-Object** Cmdlet 套用篩選器，以將傳回的資料限制在 EnableMusicOnHold 屬性等於 (-eq) False 的項目。

    Get-CsCpsConfiguration | Where-Object {$_.EnableMusicOnHold -eq $False}

## 詳細描述

使用這個 Cmdlet 擷取一個或多個通話駐留服務組態。通話駐留服務組態會指定駐留通話後的動作。例如，如果保留通話在一段時間內沒有回應，則可自動轉接其他人 (例如系統管理員) 或回應群組。也可以設定來電在一段期間後響鈴，以確保不會忘掉來電。此外，可以設定通話駐留服務在駐留通話時，向等待的來電者播放的等候音樂。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsCpsConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsCpsConfiguration"}

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
<td><p>可讓您執行萬用字元搜尋，只擷取 Identity 值與萬用字元字串相符的設定。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>您要擷取之通話駐留服務設定的唯一識別碼。這個識別碼將是 Global 或 site:&lt;網站名稱&gt;，其中 &lt;網站名稱&gt; 是設定套用之網站的名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區本機複本擷取通話保留服務資訊，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

擷取 Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings 類型的一個或多個物件。

## 請參閱

#### 其他資源

[New-CsCpsConfiguration](new-cscpsconfiguration.md)  
[Remove-CsCpsConfiguration](remove-cscpsconfiguration.md)  
[Set-CsCpsConfiguration](set-cscpsconfiguration.md)  
[Set-CsCallParkServiceMusicOnHoldFile](set-cscallparkservicemusiconholdfile.md)

