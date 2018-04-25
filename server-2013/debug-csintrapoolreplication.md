---
title: Debug-CsIntraPoolReplication
TOCTitle: Debug-CsIntraPoolReplication
ms:assetid: 9882f703-07c7-46fe-b525-7efd1326503c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205103(v=OCS.15)
ms:contentKeyID: 49291747
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Debug-CsIntraPoolReplication

 

_**上次修改主題的時間：** 2015-03-09_

藉由比較特定使用者在主要前端伺服器與複本前端伺服器上所儲存的資料，確認集區的複寫內容是否一致。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Debug-CsIntraPoolReplication -UserUri <UserIdParameter> <COMMON PARAMETERS>

    Debug-CsIntraPoolReplication -ConferenceDirectory <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會使用 SIP 位址為 "sip:kenmyer@litwareinc.com" 的使用者，來驗證前端伺服器上的複寫狀態。

    Debug-CsIntraPoolReplication -UserUri "sip:kenmyer@litwareinc.com"

## 範例 2

範例 2 會使用在 Redmond OU 中擁有使用者帳戶的所有使用者驗證複寫狀態。為達此目的，命令會先呼叫 Get-CsUser 搭配 OU 參數 (參數值 "OU=Redmond,dc=litwareinc,dc=com" 可將傳回的資料限制在於 Redmond OU 中所找到的使用者帳戶)。然後再將這些帳戶管線傳送到 ForEach-Object Cmdlet，接著使用 Debug-CsIntraPoolReplication Cmdlet 驗證 OU 中每個帳戶的複寫狀態。

    Get-CsUser -OU "OU=Redmond,dc=litwareinc,dc=com" | ForEach-Object {Debug-CsIntraPoolReplication $_.Identity}

## 範例 3

範例 3 所示的命令會使用一對使用者 SIP 位址來驗證複寫狀態。為達此目的，會將這兩個 SIP 位址 (括以引號，並使用逗號分隔) 管線傳送到 ForEach-Object Cmdlet，以對每個 SIP 位址執行 Debug-CsIntraPoolReplication Cmdlet。

    "sip:kenmyer@litwareinc.com","sip:pilar@litwareinc.com" | ForEach-Object {Debug-CsIntraPoolReplication -UserUri $_}

## 範例 4

範例 4 會驗證 ID 為 13 之會議目錄的複寫狀態。

    Debug-CsIntraPoolReplication -ConferenceDirectory 13

## 範例 5

範例 5 顯示如何為安置在指定登錄器集區上的所有使用者驗證複寫狀態。為達此目的，命令會先呼叫 Get-CsUser 搭配 Filter 參數 (篩選值 {RegistrarPool –eq "atl-cs-001.litwareinc.com"} 可將傳回的資料限制在安置於 atl-cs-001.litwareinc.com 登錄器集區上的使用者帳戶)。然後再將這些帳戶管線傳送到 Debug-CsIntraPoolReplication Cmdlet，以驗證集區中每位使用者的複寫狀態。

    Get-CsUser -Filter {RegistrarPool -eq "atl-cs-001.litwareinc.com"} | Debug-CsIntraPoolReplication UserUri {$_.Identity}

## 詳細描述

Debug-CsIntraPoolReplication Cmdlet 可讓系統管理員驗證主要前端伺服器與其複本前端伺服器之間的複寫狀態。作法有兩種：1) 驗證指定使用者在前端伺服器與其所有複本伺服器上的資料是否一致；或 2) 驗證前端伺服器與其所有複本伺服器上的會議目錄資料是否一致。執行上述作業時，Debug-CsIntraPoolReplication 會先連線到主要前端伺服器，然後再建構內含使用者或會議目錄資料的 XML 檔案。接著連線到複本伺服器並建構類似的 XML 檔案，進而驗證在 XML 檔案中選取的內容是否一致。

Debug-CsIntraPoolReplication Cmdlet 會取得一或多個使用者帳戶 (或一個會議目錄)，並向主要前端伺服器及其所有複本前端伺服器查詢該帳戶 (或會議目錄) 的相關資料，以驗證集區的複寫狀態。接著再比較從主要前端伺服器及複本伺服器擷取的資訊。若資料相符，便會認為集區間的複寫如預期運作。

請注意，只能使用安置在 Lync Server 2013上的使用者或會議目錄來呼叫此 Cmdlet。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Debug-CsIntraPoolReplication"}

**Lync Server 控制台：**Lync Server 控制台不提供 Debug-CsIntraPoolReplication Cmdlet 所執行的功能。

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
<td><p><em>ConferenceDirectory</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>可讓您驗證會議目錄複寫狀態。會議目錄應使用目錄 Identity 來指定；您可以使用下列命令來擷取會議目錄 Identity：</p>
<p>Get-CsConferenceDirectory | Select-Object Identity, ServiceId</p>
<p>同一個命令中不可同時使用 ConferenceDirectory 參數及 UserUri 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>UserUri</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>測試集區間複寫時所採用之使用者帳戶的 SIP 位址。例如：</p>
<p>-UserUri &quot;sip:kenmyer@litwareinc.com&quot;</p>
<p>同一個命令中不可同時使用 ConferenceDirectory 參數及 UserUri 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

字串或 Microsoft.Rtc.Management.ADConnect.Schema.ADUser 物件。Debug-CsIntraPoolReplication 接受管線傳送的字串值，其代表已針對 Lync Server 啟用之使用者帳戶的 SIP 位址或 Active Directory 顯示名稱。該 Cmdlet 也會為已啟用 Lync Server 的使用者，接受管線傳送的 Active Directory 使用者物件執行個體。

## 傳回類型

Debug-CsIntraPoolReplication 會傳回 Microsoft.Rtc.Management.UserPinservice.Data.syncReplicationDetails 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsManagementStoreReplicationStatus](get-csmanagementstorereplicationstatus.md)  
[Test-CsReplica](test-csreplica.md)

