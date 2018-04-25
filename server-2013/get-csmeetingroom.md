---
title: Get-CsMeetingRoom
TOCTitle: Get-CsMeetingRoom
ms:assetid: ce361cb8-042c-4708-8f9c-7e67a34a570d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205277(v=OCS.15)
ms:contentKeyID: 49292351
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsMeetingRoom

 

_**上次修改主題的時間：** 2015-03-09_

傳回設定供組織使用之所有 Lync Server 2013 會議室的資訊。會議室是專為小型會議室之視訊會議及共同作業案例而設計的會議裝置。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsMeetingRoom [-Identity <UserIdParameter>] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Filter <String>] [-LdapFilter <String>] [-OU <OUIdParameter>] [-ResultSize <Unlimited>]

## 範例

## 範例 1

範例 1 所示的命令會傳回設定供組織使用之所有會議室的資訊。

    Get-CsMeetingRoom

## 範例 2

範例 2 會傳回單一會議室的資訊：SIP 位址為 sip:RedmondMeetingRoom@litwareinc.com 的系統。

    Get-CsMeetingRoom -Identity "sip:RedmondMeetingRoom@litwareinc.com"

## 範例 3

範例 3 所示的命令會傳回已指派個別使用者語音原則 RedmondVoicePolicy 之所有會議室的資訊。為達此目的，命令會加入 Filter 參數搭配篩選值 {VoicePolicy –eq "RedmondVoicePolicy}。此篩選值會將傳回的資料限制在 VoicePolicy 屬性等於 (-eq) RedmondVoicePolicy 的會議室。

    Get-CsMeetingRoom -Filter {VoicePolicy -eq "RedmondVoicePolicy"}

## 詳細描述

在 Lync Server 中，會議室是安裝在會議室中，提供下列進階會議功能的內建電腦設備：

  - 單鍵加入會議功能

  - 多格檢視視訊庫

  - 在會議室畫面前方提供觸控式白板

  - 整合行事曆供查看排程會議

  - 內容共用及切換

若要管理這些新端點裝置，您必須為裝置建立並啟用 Microsoft Exchange Server 2013資源信箱帳戶，然後再啟用 Lync Server 2013的資源帳戶。請注意，沒有任何 Cmdlet 可以為 Lync Server 建立或移除會議室。您必須使用 [Enable-CsMeetingRoom](enable-csmeetingroom.md) Cmdlet 啟用會議室，以及使用 [Disable-CsMeetingRoom](disable-csmeetingroom.md) Cmdlet 停用會議室。另外還必須有資源帳戶，才可啟用會議室。停用會議室只會從會議室集合中移除該會議室，而不會刪除資源信箱帳戶。

若要傳回已獲指派此 Cmdlet 之所有角色型存取控制 (RBAC) 角色的清單 (包括您自行建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsMeetingRoom"}

**Lync Server 控制台:** **Get-CsMeetingRoom** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p>可讓您以替代認證來執行 <strong>Get-CsMeetingRoom</strong> Cmdlet。如果您用來登入 Windows 的帳戶不具有使用連絡人物件所需的必要權限，可能就需要這一項。</p>
<p>若要使用 Credential 參數，您必須先使用 <strong>Get-Credential</strong> Cmdlet 來建立 PSCredential 物件。如需詳細資訊，請參閱 <strong>Get-Credential</strong> Cmdlet 說明主題。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>可讓您連線至指定的網域控制站，以擷取會議室資訊。若要連線至特定的網域控制站，請加入 DomainController 參數，後面加上電腦名稱 (例如，atl-dc-001) 或其完整網域名稱 (FQDN) (例如，atl-dc-001.litwareinc.com)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您篩選 Lync Server 特定屬性來限制傳回的資料。例如，您可以將傳回的資料限制於已指派或未指派特定語音原則的會議室。</p>
<p>Filter 參數使用的 Windows PowerShell 篩選語法與 Where-Object Cmdlet 幾乎相同。例如，只傳回已指派語音原則 RedmondVoicePolicy 之會議室的篩選如下所示：</p>
<p>{VoicePolicy -eq &quot;RedmondVoicePolicy&quot;}</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>表示要擷取之會議室的 Identity。一般可以使用下列四種格式的其中一種來指定會議室識別：1) 會議室的 SIP 位址；2) 會議室的使用者主要名稱 (UPN)；3) 會議室的網域名稱和登入名稱，必須是「網域\登入」格式 (例如 litwareinc\room14)；4) 會議室的 Active Directory 顯示名稱 (例如 Room 14)。</p>
<p>您也可以使用會議室的 Active Directory 辨別名稱來參考會議室帳戶。</p>
<p>使用「顯示名稱」做為會議室 Identity 時，可以使用星號 (*) 萬用字元。例如，若 Identity 為 &quot;*Redmond*&quot;，則會傳回所有顯示名稱包含字串值 &quot;Redmond&quot; 的會議室。</p></td>
</tr>
<tr class="odd">
<td><p><em>LdapFilter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您篩選一般 Active Directory 屬性 (也就是非 Lync Server 專屬的屬性)，以限制傳回的資料。例如，您可以將傳回的資料限制於屬於特定部門的會議室。LdapFilter 參數使用 LDAP 查詢語言建立篩選。例如，只傳回 Redmond 市所找到之會議室的篩選如下所示：</p>
<p>-LdapFilter &quot;l=Redmond&quot;</p>
<p>在該語法中，&quot;l&quot; (小寫的 L) 代表 Active Directory 屬性 (位置)，&quot;=&quot; 代表比較運算子 (等於)，而 &quot;Redmond&quot; 代表篩選值。</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>可讓您傳回特定組織單位 (OU) 或容器中的會議室相關資訊。OU 參數會從指定的 OU 及其任何子 OU 傳回資料。例如，如果 Finance OU 有兩個子 OU (AccountsPayable 和 AccountsReceivable)，則會從這三個 OU 中的每一個 OU 傳回會議室。</p>
<p>指定 OU 時，請使用該容器的辨別名稱 (DN)；例如：</p>
<p>-OU &quot;OU=MeetingRooms,dc=litwareinc,dc=com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>可讓您限制 Cmdlet 傳回的記錄數。例如，若要傳回七個會議室 (不考慮樹系中的會議室數目)，請加入 ResultSize 參數並將參數值設為 7。請注意，無法保證傳回哪七個會議室。</p>
<p>結果大小可以設為 0 和 2147483647 (含) 之間的任何數字。如果設為 0，命令會執行，但不會傳回資料。如果您將 ResultSize 設為 7，但樹系中只有三個會議室，則命令會傳回這三個會議室，然後完成執行而不會出現錯誤。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

字串。 **Get-CsMeetingRoom** Cmdlet 接受代表已啟用做為 Lync Server 2013 會議室之使用者帳戶 Identity 的管線傳送字串值。

## 傳回類型

**Get-CsMeetingRoom** Cmdlet 會傳回 Microsoft.Rtc.Management.ADConnect.Schema.OCSADMeetingRoom 物件的執行個體。

## 請參閱

#### 其他資源

[Disable-CsMeetingRoom](disable-csmeetingroom.md)  
[Enable-CsMeetingRoom](enable-csmeetingroom.md)  
[Move-CsMeetingRoom](move-csmeetingroom.md)  
[Set-CsMeetingRoom](set-csmeetingroom.md)

