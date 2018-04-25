---
title: Get-CsPersistentChatEndpoint
TOCTitle: Get-CsPersistentChatEndpoint
ms:assetid: 2c37edd6-6892-4b2d-8586-6f59ab668d4b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204764(v=OCS.15)
ms:contentKeyID: 49290440
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPersistentChatEndpoint

 

_**上次修改主題的時間：** 2015-03-09_

傳回設定供組織使用之常設聊天室端點的資訊。常設聊天室端點是 Active Directory 連絡人物件，可為 Lync Server 2013 之常設聊天室集區提供易記 URL。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsPersistentChatEndpoint [-Identity <UserIdParameter>] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Filter <String>] [-LdapFilter <String>] [-OU <OUIdParameter>] [-PersistentChatPoolFqdn <Fqdn>] [-ResultSize <Unlimited>]

## 範例

## 範例 1

範例 1 所示的命令會傳回設定供組織使用之所有常設聊天室端點的資訊。

    Get-CsPersistentChatEndpoint

## 範例 2

範例 2 會使用 Filter 參數傳回 Identity 為 "sip:pce@litwareinc.com" 之常設聊天室端點的資訊。此範例會以 SIP 位址做為 Identity。

    Get-CsPersistentChatEndpoint -Identity "sip:pce@litwareinc.com"

## 範例 3

範例 3 會傳回所有設定供常設聊天室集區 atl-pcpool-001.litwareinc.com 使用之常設聊天室端點的資訊。作法是加入 PoolFqdn 參數加上常設聊天室集區的完整網域名稱。

    Get-CsPersistentChatEndpoint -PersistentChatPoolFqdn atl-pcpool-001.litwareinc.com

## 詳細描述

常設聊天室服務 (取代舊版 Microsoft Lync Server 2010 所使用的群組聊天服務) 可為組織提供類似於網際網路論壇的訊息與共同作業功能，讓使用者可以即時交換訊息，以及隨時重啟與重新開始交談。交談可以特定的主題為主，而且可以選擇讓所有人參加，或是只讓特定的使用者群組參加。同樣地，您也可設定不同的聊天室讓所有人張貼訊息，或只讓指定的簡報者張貼訊息。

當您安裝常設聊天室服務時，會自動建立每個常設聊天室集區端點。此端點為 Active Directory 連絡人物件，負責維護集區的 URI。若所有的使用者都是執行 Lync 2013，此作法會比較有效率。

但您若是有使用者執行舊版的用戶端 (例如 Microsoft Lync 2010)，這些使用者在將其舊版用戶端指向集區時，可能會發現預設的常設聊天室 URI 十分不好使用。有鑑於此，系統管理員可以使用 [New-CsPersistentChatEndpoint](new-cspersistentchatendpoint.md) Cmdlet 另外建立一個連絡人物件，提供易記易用的 URI。 **Get-CsPersistentChatEndpoint** Cmdlet 可讓您傳回所有設定供組織使用之常設聊天室端點的資訊。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPersistentChatEndpoint"}

**Lync Server 控制台：** **Get-CsPersistentChatEndpoint** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>可讓您以替代認證來執行 <strong>Get-CsPersistentChatEndpoint</strong> Cmdlet。如果您用來登入 Windows 的帳戶不具有使用使用者物件所需的必要權限，可能就需要這一項。</p>
<p>若要使用 Credential 參數，您必須先使用 <strong>Get-Credential</strong> Cmdlet 來建立 PSCredential 物件。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>可讓您連線至指定的網域控制站擷取使用者資訊。若要連線至特定的網域控制站，請加入 DomainController 參數，並緊接其後指定完整網域名稱 (FQDN)。例如：</p>
<p>-DomainController &quot;atl-dc-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可讓您篩選 Lync Server 特定屬性來限制傳回的資料。例如，您可以將傳回的資料限制為已指派特定語音原則的常設聊天室端點，或是未指派特定語音原則的端點。</p>
<p>Filter 參數使用的 Windows PowerShell 篩選語法與 <strong>Where-Object</strong> Cmdlet 相同。例如，只傳回已指派個別使用者會議原則之端點的篩選如下所示，其中 ConferencingPolicy 代表 Active Directory 屬性，-ne 代表比較運算子 (不等於)，而 $Null (內建的 Windows PowerShell 變數) 代表篩選值：</p>
<p>-Filter {ConferencingPolicy -ne $Null}</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>要傳回之常設聊天室端點的唯一識別碼。端點 Identity 通常是以端點的 SIP 位址或顯示名稱來指定；例如：</p>
<p>-Identity &quot;sip:pcEndpoint1@litwareinc.com&quot;</p>
<p>不過，您也可以使用端點的完整 Identity；例如：</p>
<p>-Identity &quot;CN={33e5014b-dcba-46b5-9bf7-48f4d5fca69d}, CN=Application Contacts,CN=RTC Service,CN=Services,CN=Configuration,DC=litwareinc,DC=com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>LdapFilter</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可讓您篩選一般 Active Directory 屬性 (也就是非 Lync Server 專屬的屬性)，以限制傳回的資料。由於常設聊天室端點的非 Lync Server 屬性很少，所以此參數是用最小值。</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>可讓您傳回特定組織單位 (OU) 或容器中的使用者帳戶相關資訊。由於新常設聊天室端點全都建立在相同的 Active Directory 容器中 (ApplicationContacts/RTC Service/Services/Configuration)，所以此參數是用最小值。</p></td>
</tr>
<tr class="odd">
<td><p><em>PersistentChatPoolFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>與常設聊天室端點相關聯之常設聊天室集區的完整網域名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>ResultSize</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>可讓您限制 Cmdlet 傳回的記錄數。例如，若要傳回七位連絡人 (不考慮樹系中的使用者數目)，請加入 ResultSize 參數並將參數值設為 7。請注意，無法保證傳回哪七位使用者。</p>
<p>結果大小可以設為 0 和 2147483647 (含) 之間的任何數字。如果設為 0，命令會執行，但不會傳回資料。如果您將 ResultSize 設為 7，但樹系中只有三位連絡人，則命令會傳回這三位連絡人，然後完成執行而不會出現錯誤。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

字串值。**Get-CsPersistentChatEndpoint** Cmdlet 可以接受代表常設聊天室端點之 Identity 或 SIP 位址的字串值。

## 傳回類型

**Get-CsPersistentChatEndpoint** Cmdlet 會傳回 Microsoft.Rtc.Management.ADConnect.Schema.OCSPersistentChatContact 類別的執行個體。

## 請參閱

#### 其他資源

[New-CsPersistentChatEndpoint](new-cspersistentchatendpoint.md)  
[Remove-CsPersistentChatEndpoint](remove-cspersistentchatendpoint.md)

