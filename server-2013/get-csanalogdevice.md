---
title: Get-CsAnalogDevice
TOCTitle: Get-CsAnalogDevice
ms:assetid: 92f56039-f112-45bb-8340-109b0837f828
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398748(v=OCS.15)
ms:contentKeyID: 49291690
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAnalogDevice

 

_**上次修改主題的時間：** 2015-03-09_

傳回您可以使用 Lync Server 加以管理之類比裝置的資訊。類比裝置是連接到公用交換電話網路的電話或其他裝置。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsAnalogDevice [-Identity <UserIdParameter>] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Filter <String>] [-LdapFilter <String>] [-OU <OUIdParameter>] [-ResultSize <Unlimited>]

## 範例

## 範例 1

範例 1 所示的命令會傳回所有目前設定供組織使用之類比裝置的集合。作法是呼叫不含任何參數的 **Get-CsAnalogDevice** Cmdlet。

    Get-CsAnalogDevice

## 範例 2

在範例 2 中，只會針對組織中的所有類比裝置傳回兩個屬性值：DisplayName 和 LineUri。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsAnalogDevice** Cmdlet，以傳回組織中所有類比裝置的所有屬性值。然後再將該集合管線傳送至 **Select-Object** Cmdlet，這會只選取並顯示 DisplayName 和 LineUri 屬性的值。

    Get-CsAnalogDevice | Select-Object DisplayName, LineUri

## 範例 3

範例 3 會傳回其 Active Directory 顯示名稱為 "Building 14 Receptionist" 之類比裝置的資訊。為達此目的，命令會呼叫 Get-**Get-CsAnalogDevice** 搭配 Filter 參數 (篩選值 {DisplayName -eq "Building 14 Receptionist"} 可將傳回的項目限制在 DisplayName 屬性等於 "Building 14 Receptionist" 的類比裝置)。

    Get-CsAnalogDevice -Filter {DisplayName -eq "Building 14 Receptionist"}

## 範例 4

範例 4 會傳回所有針對 192.168.0.240 閘道設定的類比裝置。作法是呼叫 **Get-CsAnalogDevice** Cmdlet 並搭配 Filter 參數；"192.168.0.240" 篩選值可確保傳回的物件只是 Gateway 屬性等於 192.168.0.240 的類比裝置。

    Get-CsAnalogDevice -Filter {Gateway -eq "192.168.0.240"}

## 範例 5

範例 5 所示的命令會傳回組織中所有類比傳真機的資訊。為了執行此工作，命令會呼叫 **Get-CsAnalogDevice** Cmdlet 並搭配 Filter 參數。篩選值 {AnalogFax -eq $True} 可將傳回的物件限制在 AnalogFax 屬性等於 True 的傳真機類比裝置。

    Get-CsAnalogDevice -Filter {AnalogFax -eq $True}

## 範例 6

範例 6 會傳回單一類比裝置 (即 LineUri (電話號碼) 等於 tel:+14255556001 的裝置)。

    Get-CsAnalogDevice -Filter {LineUri -eq "tel:+14255556001"}

## 範例 7

範例 7 會傳回區碼為 425 且電話首碼為 555 的所有類比裝置。為了執行此工作，會使用 **Get-CsAnalogDevice** Cmdlet 並搭配 Filter 參數 (篩選值 {LineUri -like "tel:+1425555\*"} 可將傳回的資料限制在 LineUri 屬性開頭為字元 "tel:+1425555" 的裝置，也就是以下列字元開頭的電話號碼：1425555 (例如 1-425-555-1298))。

    Get-CsAnalogDevice -Filter {LineUri -like "tel:+1425555*"}

## 範例 8

範例 8 會傳回所有在 Active Directory 網域服務的 Telecommunications OU 內具有連絡人物件之類比裝置的集合。為達成此目的，會呼叫 **Get-CsAnalogDevice** Cmdlet 並搭配 OU 參數；此參數值可將傳回的物件限制在於辨別名稱為 ou=Telecommunications,dc=litwareinc,dc=com 的 OU 中具有連絡人物件的類比裝置。

    Get-CsAnalogDevice -OU "ou=Telecommunications,dc=litwareinc,dc=com"

## 範例 9

範例 9 所示的命令會顯示如何傳回類比裝置的集合，然後為集合中的每個裝置指派語音原則。為達成此目的，會先呼叫不含任何參數的 **Get-CsAnalogDevice** Cmdlet；這樣會傳回所有設定供組織使用之類比裝置的集合。然後，此集合會管線傳送到 **Grant-CsVoicePolicy** Cmdlet，以將語音原則 AnalogVoicePolicy 指派給集合中的每個裝置。

    Get-CsAnalogDevice | Grant-CsVoicePolicy -PolicyName "AnalogVoicePolicy"

## 詳細描述

類比裝置包含電話、傳真機、數據機，以及與公用交換電話網路 (PSTN) 連接的聽障人士電傳通訊裝置 (TTY/TDD)。與利用 Enterprise Voice (Microsoft 提供的 Voice over Internet Protocol (VoIP) 解決方案) 的裝置不同，類比裝置不會使用數位封包傳輸資訊；而是使用連續訊號來傳輸資訊。此訊號通常稱做類比訊號，因此這類裝置稱做「類比裝置」。

除了類比電話，以及利用 Enterprise Voice 的電話外，還有另一種類別的電話：數位非 IP 電話。這類電話專屬於當初購機時的專用交換機 (PBX) 系統，無法使用 Lync Server Cmdlet 來管理。

為了讓系統管理員能夠管理組織的類比裝置，Lync Server 讓您能夠將類比裝置與 Active Directory 連絡人物件產生關聯。在裝置已與連絡人物件產生關聯後，您便可藉由執行指派原則與撥號對應表至該連絡人等作業，來管理類比裝置。

**Get-CsAnalogDevice** Cmdlet 可讓您擷取設定供組織使用的類比裝置相關資訊。如果您呼叫不含任何參數的 **Get-CsAnalogDevice** Cmdlet，此 Cmdlet 會傳回您所有類比裝置的資訊。選用的參數則提供讓您篩選資訊的各種方法；例如，您可以傳回所有在指定 OU 中具有連絡人物件的裝置，或所有位於某指定建築物中的類比裝置。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsAnalogDevice** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。可以使用 **Grant-CsOUPermission** Cmdlet，為特定網站或特定 Active Directory OU 指派執行此 Cmdlet 的權限。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsAnalogDevice"}

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
<td><p>可讓您以替代認證來執行 <strong>Get-CsAnalogDevice</strong> Cmdlet。如果您用來登入 Windows 的帳戶不具有使用連絡人物件所需的必要權限，可能就需要這一項。</p>
<p>若要使用 Credential 參數，您必須先使用 <strong>Get-Credential</strong> Cmdlet 來建立 PSCredential 物件。如需詳細資訊，請參閱 <strong>Get-Credential</strong> Cmdlet 說明主題。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>可讓您連線至指定的網域控制站，以擷取連絡人資訊。若要連線至特定的網域控制站，請加入 DomainController 參數，後面加上該電腦的完整網域名稱 (FQDN) (如 atl-cs-001.litwareinc.com)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您篩選 Lync Server 特定屬性來限制傳回的資料。例如，您可以將傳回的資料限制在已指派特定語音原則的類比裝置連絡人物件，或未指派特定語音原則的連絡人。</p>
<p>Filter 參數使用的 Windows PowerShell 篩選語法與 <strong>Where-Object</strong> Cmdlet 相同。例如，只會傳回傳真機的篩選看起來如下，其中 AnalogFax 代表 Active Directory 屬性、-eq 代表比較運算子 (等於)，而 $True (內建的 Windows PowerShell 變數) 代表篩選值：</p>
<p>-Filter {AnalogFax -eq $True}</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>類比裝置的唯一識別碼。類比裝置使用關聯連絡人物件的 Active directory 辨別名稱來識別。根據預設，類比裝置使用 GUID (全域唯一識別碼) 做為一般名稱，這表示裝置的 Identity 通常會與此類似：CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com。</p></td>
</tr>
<tr class="odd">
<td><p><em>LdapFilter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您篩選一般 Active Directory 屬性 (也就是非 Lync Server 專屬的屬性)，以限制傳回的資料。例如，您可以將傳回的資料限制在已指派特定部門或位於特定建築物的連絡人物件。</p>
<p>在建立篩選時，LdapFilter 參數會使用 LDAP 查詢語言。例如，只有在連絡人物件代表 Redmond 市中的類比裝置時，才會傳回連絡人物件的篩選器看起來如下：</p>
<p>-LdapFilter &quot;l=Redmond&quot;</p>
<p>在上述篩選中，&quot;l&quot; 代表 Active Directory 屬性 (位置)，&quot;=&quot; 代表比較運算子 (等於)，而 &quot;Redmond&quot; 代表篩選值。</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>可讓您從特定 Active Directory 組織單位 (OU) 傳回連絡人物件。這會從指定的 OU 及其任何子 OU 傳回資料。例如，如果 Finance OU 有兩個子 OU -- AccountsPayable 和 AccountsReceivable -- 則會從這三個 OU 中的每一個 OU 傳回共同的類比裝置資訊。</p>
<p>指定 OU 時，請使用該容器的辨別名稱；例如：-OU &quot;OU=Finance,dc=litwareinc,dc=com&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>可讓您限制命令傳回的記錄數。例如，若要傳回七個類比裝置 (而不考慮樹系中有多少類比裝置)，請加上 ResultSize 參數並將參數值設為 7。請注意，無法保證會傳回哪七個電話。如果您將 ResultSize 設為 7，但樹系中只有三個類比裝置，則命令會傳回這三個裝置，然後以沒有錯誤的狀態完成。</p>
<p>結果大小可以設為 0 和 2147483647 (含) 之間的任何數字。如果設為 0，命令會執行，但不會傳回資料。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

字串。**Get-CsAnalogDevice** Cmdlet 會接受管線傳送的字串值，該值代表類比裝置的 Identity。

## 傳回類型

**Get-CsAnalogDevice** Cmdlet 會傳回 Microsoft.Rtc.Management.ADConnect.Schema.OCSADAnalogDeviceContact 物件的執行個體。

## 請參閱

#### 其他資源

[Move-CsAnalogDevice](move-csanalogdevice.md)  
[New-CsAnalogDevice](new-csanalogdevice.md)  
[Remove-CsAnalogDevice](remove-csanalogdevice.md)  
[Set-CsAnalogDevice](set-csanalogdevice.md)

