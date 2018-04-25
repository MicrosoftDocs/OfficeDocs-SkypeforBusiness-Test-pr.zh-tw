---
title: Get-CsMeetingConfiguration
TOCTitle: Get-CsMeetingConfiguration
ms:assetid: 3aa2d905-0ce0-4675-8543-c7bb9b4a3d1a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425875(v=OCS.15)
ms:contentKeyID: 49290639
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsMeetingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

**Get-CsMeetingConfiguration** Cmdlet 可讓您傳回組織目前所使用之會議組態設定的資訊。會議組態設定可用於指定使用者所能建立的會議類型，以及控制匿名使用者和電話撥入式會議使用者如何 (或能否) 加入這些會議。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsMeetingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsMeetingConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>] [-Tenant <Guid>]

## 範例

## 範例 1

範例 1 所示的命令會傳回組織中目前正在使用之所有會議組態設定的集合。

    Get-CsMeetingConfiguration

## 範例 2

在範例 2 中，只傳回一個會議組態設定的集合：Identity 為 site:Redmond 的設定。

    Get-CsMeetingConfiguration -Identity site:Redmond

## 範例 3

範例 3 會傳回已在服務範圍設定的所有會議組態設定。作法是加入 Filter 參數及篩選值 "service:\*"，以將傳回的資料限制為 Identity 屬性開頭為字元 "service:" 的設定。

    Get-CsMeetingConfiguration -Filter "service:*"

## 範例 4

範例 4 會傳回預設允許匿名使用者之會議組態設定的資訊。為達成此目的，命令會先不指定任何參數而直接使用 **Get-CsMeetingConfiguration** Cmdlet，以傳回目前所使用之所有會議組態設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 AdmitAnonymousByDefault 屬性等於 True 的設定。

    Get-CsMeetingConfiguration | Where-Object {$_.AdmitAnonymousUsersByDefault -eq $True}

## 詳細描述

會議是 Lync Server 不可或缺的一部分。**CsMeetingConfiguration** Cmdlet 可讓系統管理員控制使用者可以建立的會議類型，並決定會議處理匿名使用者與電話撥入式會議使用者的方式。例如，您可以設定會議，以便自動准許透過公用交換電話網路 (PSTN) 撥入的任何人加入會議。或者，您也可以設定會議，不自動允許電話撥入式使用者加入會議，而是送往會議大廳。這些電話撥入式使用者會一直停留在大廳，直到主持人准許他們加入會議為止。

**Get-CsMeetingConfiguration** Cmdlet 可讓您傳回組織中目前正在使用之會議組態設定的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsMeetingConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsMeetingConfiguration"}

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
<td><p>可讓您使用萬用字元傳回一或多個會議組態設定集合。若要傳回在網站範圍設定的所有設定集合，請使用下列語法：-Filter site:*。若要傳回在 Identity (唯一可以當做篩選依據的屬性) 中任何位置出現字串值 &quot;EMEA&quot; 的所有設定集合，請使用下列語法：-Filter *EMEA*。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>表示您要傳回之會議組態設定集合的唯一識別碼。若要參考全域設定，請使用下列語法：-Identity global。若要參考在網站範圍設定的集合，請使用類似下列的語法：-Identity site:Redmond。在服務範圍設定的設定可以使用類似如下的語法來擷取：-Identity service:UserServer:atl-cs-001.litwareinc.com。</p>
<p>若未指定此參數，則 <strong>Get-CsMeetingConfiguration</strong> Cmdlet 將會傳回用於組織之所有會議設定的集合。</p>
<p>請注意，如有指定 Identity，即無法使用萬用字元。如果您必須使用萬用字元，請改為包含 Filter 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取會議組態資料，而非從中央管理存放區本身擷取。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要擷取其會議組態設定之 Office 365 租用戶帳戶的全域唯一識別碼 (GUID)。</p>
<p>例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行此命令來傳回每位租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>倘若使用的是 Windows PowerShell 遠端工作階段並僅連線至 商務用 Skype Online，則無需包含 Tenant 參數。相反地，系統將會根據您的連線資訊自動填入租用戶識別碼。Tenant 參數主要用於混合式部署。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsMeetingConfiguration** Cmdlet 不接受管線傳送的資料。

## 傳回類型

**Get-CsMeetingConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.MeetingConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsMeetingConfiguration](new-csmeetingconfiguration.md)  
[Remove-CsMeetingConfiguration](remove-csmeetingconfiguration.md)  
[Set-CsMeetingConfiguration](set-csmeetingconfiguration.md)

