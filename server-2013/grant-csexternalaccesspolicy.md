---
title: Grant-CsExternalAccessPolicy
TOCTitle: Grant-CsExternalAccessPolicy
ms:assetid: 451fef34-3021-4261-8494-b36420b04c82
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425942(v=OCS.15)
ms:contentKeyID: 49290769
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsExternalAccessPolicy

 

_**上次修改主題的時間：** 2015-03-09_

可讓您指派使用者或使用者群組的外部存取原則。外部存取原則可指定使用者是否可以：1) 和同盟組織中用工作階段初始通訊協定 (SIP) 帳戶的使用者通訊；2) 和使用公用立即訊息 (IM) 提供者 (例如 MSN) 之SIP 帳戶的使用者通訊；以及 3) 直接從網際網路存取 Lync Server，而無須登入內部網路。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Grant-CsExternalAccessPolicy -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-PolicyName <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會將外部存取原則 RedmondAccessPolicy 指派給 Active Directory 顯示名稱為 Ken Myer 的使用者。

    Grant-CsExternalAccessPolicy -Identity "Ken Myer" -PolicyName RedmondAccessPolicy

## 範例 2

範例 2 所示的命令會將外部存取原則 RedmondAccessPolicy 指派給在 Redmond 城市中工作的所有使用者。為達成此目的，命令會先使用 **Get-CsUser** Cmdlet 和 LdapFilter 參數傳回所有在 Redmond 工作的使用者集合 ；篩選值 "l=Redmond" 可將傳回的資料限制在 Redmond 城市中 (篩選器中的 l 是小寫 l，代表位置) 工作的使用者。然後，此集合會管線傳送到 **Grant-CsExternalAccessPolicy**，以將 RedmondAccessPolicy 原則指派給集合中的每一位使用者。

    Get-CsUser -LdapFilter "l=Redmond" | Grant-CsExternalAccessPolicy -PolicyName RedmondAccessPolicy

## 範例 3

範例 3 針對職稱為「業務代表」的所有使用者指派外部存取原則 SalesAccessPolicy。為達此目的，命令會先使用 **Get-CsUser** Cmdlet 及 LdapFilter 參數以傳回所有業務代表的集合；篩選值 "Title=Sales Representative" 會將傳回的集合限制在職稱為「業務代表」的使用者。接著會將此篩選集合以管線傳送至 **Grant-CsExternalAccessPolicy** Cmdlet，此 Cmdlet 會將原則 SalesAccessPolicy 指派給集合中的每位使用者。

    Get-CsUser -LdapFilter "Title=Sales Representative" | Grant-CsExternalAccessPolicy -PolicyName SalesAccessPolicy

## 範例 4

範例 4 所示的命令會將 BasicAccessPolicy 外部存取原則指派給尚未被明確指派個別使用者原則的所有使用者 (亦即，目前正由網站原則或全域原則管理的使用者)。為達成此目的，會使用 **Get-CsUser** Cmdlet 搭配 Filter 參數，以傳回適當的使用者集合；篩選值 {ExternalAccessPolicy -eq $Null} 可將傳回的資料限制在 ExternalAccessPolicy 屬性等於 (-eq) Null 值 ($Null) 的使用者帳戶。根據定義，僅當使用者尚未獲指派個別使用者原則時，ExternalAccessPolicy 才會是 Null。

    Get-CsUser -Filter {ExternalAccessPolicy -eq $Null} | Grant-CsExternalAccessPolicy -PolicyName BasicAccessPolicy

## 範例 5

範例 5 會將外部存取原則 USAccessPolicy 指派給在美國組織單位 (OU) 中有帳戶的所有使用者。命令會先呼叫 **Get-CsUser** Cmdlet 與 OU 參數；參數值 "ou=US,dc=litwareinc,dc=com" 會將傳回的資料限制在 US OU (美國組織單位) 中有帳戶的使用者。然後再將傳回的集合管線傳送到 **Grant-CsExternalAccessPolicy** Cmdlet，以將 USAccessPolicy 原則指派給集合中的每一位使用者。

    Get-CsUser -OU "ou=US,dc=litwareinc,dc=com" | Grant-CsExternalAccessPolicy -PolicyName USAccessPolicy

## 範例 6

例 6 會取消指派先前指派給任何已為 Lync Server 啟用之使用者的任何個別使用者外部存取原則。為達成此目的，命令會先呼叫 **Get-CsUser** Cmdlet (不含任何參數)，以傳回啟用 Lync Server 之所有使用者的集合。然後，此集合會管線傳送到 **Grant-CsExternalAccessPolicy** Cmdlet，以使用 "-PolicyName $Null" 語法移除先前指派給這些使用者的個別使用者外部存取原則。

    Get-CsUser | Grant-CsExternalAccessPolicy -PolicyName $Null

## 詳細描述

安裝 Lync Server 時，只允許使用者彼此交換立即訊息和目前狀態資訊：根據預設，他們只能與 Active Directory 網域服務 中具有 SIP 帳戶的其他人員通訊。此外，不允許使用者透過網際網路存取 Lync Server；而是在他們可以登入 Lync Server 之前，必須登入您的內部網路。

這可能足以符合您的通訊需求。如果不符合您的需求，您可以使用外部存取原則，擴充使用者通訊和共同作業的能力。外部存取原則可以授與 (或撤銷) 使用者執行下列任何或全部作業的能力：

1\. 與具有含同盟組織 SIP 帳戶的人員通訊。請注意，啟用同盟將不會自動提供使用者這項功能。而是您必須啟用同盟，然後指派使用者外部存取原則，給予他們與同盟使用者通訊的權限。

2\. 透過公用立即訊息服務 (例如 MSN) 與具有 SIP 帳戶的人員通訊。

3\. 透過網際網路存取 Lync Server，而不必先登入您的內部網路。這讓使用者可以使用 Lync，並從網路咖啡廳或其他遠端位置登入 Lync Server。

當您安裝 Lync Server 時，系統會自動為您建立全域外部存取原則。除了此全域原則外，您也可以使用 **New-CsExternalAccessPolicy** Cmdlet 建立在網站範圍或個別使用者範圍設定的其他外部存取原則。

若原則是在網站範圍建立的，則會自動將該原則指派給該網站，例如系統會自動將 Identity 為 site:Redmond 的外部存取原則指派給 Redmond 網站。相反地，在個別使用者範圍建立的原則不會自動指派給任何人。而是必須明確將這些原則指派給使用者或使用者群組。指派個別使用者原則是 **Grant-CsExternalAccessPolicy** Cmdlet 的工作。

請注意，個別使用者原則一律優先於網站原則與全域原則。例如，假設您建立一個允許與同盟的使用者通訊的個別使用者原則，並將該原則指派給 Ken Myer。只要該原則為生效中，便允許 Ken 與同盟的使用者通訊，即使是 Ken 的網站原則或全域原則不允許這類通訊。這是因為個別使用者原則優先於其他原則。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Grant-CsExternalAccessPolicy** Cmdlet：RTCUniversalUserAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsExternalAccessPolicy"}

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
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>要接受指派原則之使用者帳戶的 Identity。可以使用下列四種格式的其中一種來指定使用者識別：1) 使用者的 SIP 位址；2) 使用者的使用者主體名稱 (UPN)；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (如 litwareinc\kenmyer)；4) 使用者的 Active Directory 顯示名稱 (如 Ken Myer)。也可以透過使用者的 Active Directory 辨別名稱來參考使用者識別。</p>
<p>此外，您在指定使用者 Identity 時，可以使用星號 (*) 萬用字元。例如，Identity &quot;* Smith&quot; 會傳回所有顯示名稱是以字串 &quot; Smith&quot; 結束的使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>允許在指派新原則時，指定要連線網域控制站的完整網域名稱 (FQDN)。若未指定此參數， <strong>Grant-CsExternalAccessPolicy</strong> Cmdlet 會先連線到第一個可用的網域控制站。</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>可讓您透過代表已指派原則的使用者之管線傳遞使用者物件。根據預設， <strong>Grant-CsExternalAccessPolicy</strong> Cmdlet 不會透過管線傳遞任何物件。</p></td>
</tr>
<tr class="odd">
<td><p><em>PolicyName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要指派之原則的「名稱」。簡單來說，PolicyName 是原則 Identity 減去原則範圍 (&quot;tag:&quot;prefix)。例如，Identity 為 tag:Redmond 的原則，其 PolicyName 會等於 Redmond；Identity 為 tag:RedmondAccessPolicy 的原則，其 PolicyName 就等於 RedmondAccessPolicy。</p>
<p>若要取消指派先前指派給使用者的個別使用者原則，請將 PolicyName 參數設為 $Null。</p></td>
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

字串值或 Microsoft.Rtc.Management.ADConnect.Schema.ADUser 物件。 **Grant-CsExternalAccessPolicy** Cmdlet 會接受代表使用者帳戶 Identity 之字串值的管線傳送資料。Cmdlet 也接受管線傳送的使用者物件輸入。

## 傳回類型

根據預設， **Grant-CsExternalAccessPolicy** Cmdlet 不會傳回值或物件，但若是加入 PassThru 參數，將會傳回 Microsoft.Rtc.Management.ADConnect.Schema.OCSUserOrAppContact 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsExternalAccessPolicy](get-csexternalaccesspolicy.md)  
[New-CsExternalAccessPolicy](new-csexternalaccesspolicy.md)  
[Remove-CsExternalAccessPolicy](remove-csexternalaccesspolicy.md)  
[Set-CsExternalAccessPolicy](set-csexternalaccesspolicy.md)

