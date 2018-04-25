---
title: Get-CsImFilterConfiguration
TOCTitle: Get-CsImFilterConfiguration
ms:assetid: de9b24a1-8d17-4da1-89c2-db5b532674eb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398980(v=OCS.15)
ms:contentKeyID: 49292544
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsImFilterConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織中所設定的立即訊息 (IM) 連結篩選。這些篩選可用於禁止使用者傳送內含使用特定首碼之超連結的立即訊息 (例如首碼為 http 或 telnet 的連結)。這表示根據您的設定，這表示任何開頭為這些組合的統一資源識別元 (URI)，都會根據您的設定而轉換成無法點選的超連結或整個移除。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsImFilterConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsImFilterConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回設定供組織使用之所有 IM 超連結篩選的集合。這是隨時呼叫不含任何其他參數的 **Get-CsImFilterConfiguration** Cmdlet 時的運作方式。

    Get-CsImFilterConfiguration

## 範例 2

範例 2 會傳回一個 IM 篩選的設定：Identity 為 site:Redmond 的設定。由於身分識別必須是唯一的，因此這個命令絕對不會傳回一個以上的組態。

    Get-CsImFilterConfiguration -Identity site:Redmond

## 範例 3

範例 3 會使用 Filter 參數，以傳回已在網站層級進行設定之所有 IM 篩選的集合。萬用字元字串 site:\* 會指示 **Get-CsImFilterConfiguration** Cmdlet，只傳回 Identity 開頭字串值為 site: 的 IM 篩選組態。

    Get-CsImFilterConfiguration -Filter site:*

## 範例 4

在範例 4 中，在螢幕上顯示全域 IM 篩選組態的 Prefixes 屬性值，會「展開」此屬性值；這只是說明屬性及其值會以更為簡易及更易於讀取的格式顯示。為了執行此工作，會先使用 **Get-CsImFilterConfiguration** Cmdlet 來擷取全域 IM 篩選組態 (請注意，對 **Get-CsImFilterConfiguration** Cmdlet 的呼叫會以括弧括住。這樣會告知 Windows PowerShell 先執行以括弧括住的命令，然後由此繼續)。擷取組態之後，會在每一行顯示含一個首碼的 Prefixes 屬性值。

    (Get-CsImFilterConfiguration -Identity Global).Prefixes

## 詳細描述

傳送立即訊息時，使用者可以在該訊息的文字中內嵌 URI，讓交談中的其他參與者參考特定的網站或共用。您可以設定 Lync Server，以封鎖或停用具有特定首碼的超連結 (換句話說，參與者無法只是按一下連結，就前往 URI 所指的任何網站；他們必須手動複製連結並將其貼入瀏覽器)。

**Get-CsImFilterConfiguration** Cmdlet 會從立即訊息擷取所有用於篩選 URI 的設定。自行呼叫 (不使用任何參數) **Get-CsImFilterConfiguration** Cmdlet 會傳回可供全域及所有網站使用的所有 URI IM 篩選設定。您也可以指定 Identity，以顯示特定網站的設定 (或全域設定)。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsImFilterConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsImFilterConfiguration"}

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
<td><p>執行符合指定 Identity 模式之組態的萬用字元搜尋。例如，傳回含開頭為 site* (所有特定網站設定) 之識別身分的所有設定。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>您要擷取之設定的唯一識別碼。這可為全域或 site:&lt;網站名稱&gt;，其中 &lt;網站名稱&gt; 是這些設定套用的網站名稱，例如 site:Redmond。</p>
<p>完整資料類型：Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區本機複本擷取 IM 篩選器組態，而不從 中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

**Get-CsImFilterConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsImFilterConfiguration](new-csimfilterconfiguration.md)  
[Remove-CsImFilterConfiguration](remove-csimfilterconfiguration.md)  
[Set-CsImFilterConfiguration](set-csimfilterconfiguration.md)

