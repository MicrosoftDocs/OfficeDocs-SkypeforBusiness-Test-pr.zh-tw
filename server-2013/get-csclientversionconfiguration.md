---
title: Get-CsClientVersionConfiguration
TOCTitle: Get-CsClientVersionConfiguration
ms:assetid: ed39feda-ebcf-4ed6-a970-64543f150b16
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399072(v=OCS.15)
ms:contentKeyID: 49292718
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsClientVersionConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

擷取組織目前所使用之指定的用戶端版本組態設定集合。用戶端版本組態設定可指定 Lync Server 是否需要檢查登入系統之所有用戶端應用程式的版本號碼。如有啟用用戶端版本篩選，則用戶端應用程式存取系統的能力，將視相關用戶端版本原則中所設定的設定而定。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsClientVersionConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsClientVersionConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

在第一個範例中，呼叫 **Get-CsClientVersionConfiguration** Cmdlet 時未指定其他任何參數。這會導致 **Get-CsClientVersionConfiguration** 傳回組織目前所使用之所有用戶端版本組態設定的集合。

    Get-CsClientVersionConfiguration

## 範例 2

在此範例中， **Get-CsClientVersionConfiguration** Cmdlet 會傳回所有 Identity 為 site:Redmond 的用戶端版本組態設定。由於 Identity 必須是唯一的，因此這個命令絕對不會傳回一個以上的項目。

    Get-CsClientVersionConfiguration -Identity site:Redmond

## 範例 3

範例 3 會傳回已在網站範圍內套用的所有用戶端版本組態設定。作法是加入 Filter 參數和篩選值 "site:\*"。此篩選值會指示 **Get-CsClientVersionConfiguration** Cmdlet 只傳回 Identity 開頭為 "site:" 字串值的設定。

    Get-CsClientVersionConfiguration -Filter "site:*"

## 範例 4

範例 4 會傳回目前已停用的所有用戶端版本組態設定。為了執行此工作，命令會先使用 **Get-CsClientVersionConfiguration** Cmdlet，以傳回設定供組織使用之所有用戶端版本設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet 以套用篩選，將集合限制在 Enabled 屬性等於 False 的設定。

    Get-CsClientVersionConfiguration | Where-Object {$_.Enabled -eq $False}

## 詳細描述

Lync Server 讓系統管理員有相當大的彈性空間可指定使用者用來登入系統的用戶端軟體 (以及同樣重要的該軟體版本號碼)。例如，沒有任何技術上的原因非要使用者使用 Lync Server 登入 Lync；也沒有任何技術限制不讓使用者使用 Microsoft Office Communicator 2007 R2 登入。

然而，也可能是一些非技術上的原因造成您不想要使用者使用 Office Communicator 2007 R2 登入。例如， Office Communicator 2007 R2 並不支援 Lync 中所有的功能，因此使用 Office Communicator 2007 R2 登入的使用者其使用經驗，會與使用 Lync 登入的使用者不同。這會對您的使用者造成一些困擾；也對服務台人員造成困擾，因為他們必須支援許多不同的用戶端應用程式。

如果您的組織有這個問題，則可以運用用戶端版本篩選功能來指定可使用哪些用戶端應用程式登入 Lync Server。當您安裝 Lync Server 時，會安裝並啟用一組全域的用戶端版本組態設定。這些設定會用於決定是否啟用用戶端版本篩選。除了全域設定外，用戶端版本組態設定也會在網站範圍套用；在那些狀況下，網站設定會優先於全域設定。

**Get-CsClientVersionConfiguration** Cmdlet 讓您能夠擷取組織目前所使用之用戶端版本組態設定的資訊。請注意，此 Cmdlet 不會傳回任何允許或不允許用戶端應用程式的資訊。若要擷取該資訊，請使用 **Get-CsClientVersionPolicy** Cmdlet。

另請注意，用戶端版本組態並非一個安全性功能。該技術可仰賴用戶端應用程式的自行報告，且不會嘗試確認應用程式是否真的是應用程式，而該應用程式的版本號碼就如其所聲明般。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsClientVersionConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsClientVersionConfiguration"}

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
<td><p>讓您能夠使用萬用字元，以傳回一或多個用戶端版本組態設定的集合。若要傳回在網站範圍所設定之所有設定集合，請使用下列語法：-Filter site:*。若要傳回在 Identity (您唯一可篩選的屬性) 中某處有字串值 &quot;EMEA&quot; 的所有設定集合，請使用下列語法：-Filter *EMEA*。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>指出要傳回之用戶端版本組態設定集合的唯一識別碼。若要參考全域設定，請使用下列語法：-Identity global。若要參照在此網站範圍設定的集合，請使用如下語法：-Identity site:Redmond。您無法在指定 Identity 時使用萬用字元。如果您必須使用萬用字元，請改為包含 Filter 參數。</p>
<p>若未指定此參數，則 <strong>Get-CsClientVersionConfiguration</strong> Cmdlet 將傳回組織所使用的所有用戶端版本組態設定集合。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區 的本機複本擷取用戶端版本組態資料，而非從 中央管理存放區 本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Get-CsClientVersionConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsClientVersionConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsClientVersionConfiguration](new-csclientversionconfiguration.md)  
[Remove-CsClientVersionConfiguration](remove-csclientversionconfiguration.md)  
[Set-CsClientVersionConfiguration](set-csclientversionconfiguration.md)

