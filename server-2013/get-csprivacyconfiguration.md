---
title: Get-CsPrivacyConfiguration
TOCTitle: Get-CsPrivacyConfiguration
ms:assetid: f10ebf4a-1af5-48cf-96dc-4f5d56281848
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413002(v=OCS.15)
ms:contentKeyID: 49292763
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPrivacyConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織目前所使用之隱私權組態設定的資訊。隱私權組態設定可指定使用者所能使用的資訊量。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsPrivacyConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsPrivacyConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>] [-Tenant <Guid>]

## 範例

## 範例 1

範例 1 所示的命令會傳回組織目前所使用的所有隱私組態設定。

    Get-CsPrivacyConfiguration

## 範例 2

範例 2 會傳回隱私權組態設定的單一集合：Identity 為 site:Redmond 的設定。

    Get-CsPrivacyConfiguration -Identity site:Redmond

## 範例 3

範例 3 會傳回所有在網站範圍內指派之所有隱私組態設定的資訊。為達此目的，會加上 Filter 參數並搭配篩選值 "site:\*"。此篩選值可確保只會傳回 Identity (唯一可篩選的屬性) 頭為字元 "site:" 的設定。

    Get-CsPrivacyConfiguration -Filter "site:*"

## 範例 4

範例 4 所示的命令會傳回已啟用隱私模式之所有隱私組態設定的資訊。作法是先呼叫不含任何參數的 **Get-CsPrivacyConfiguration** Cmdlet，以傳回所有隱私設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 EnablePrivacyMode 屬性等於 True 的設定。

    Get-CsPrivacyConfiguration | Where-Object {$_.EnablePrivacyMode -eq $True}

## 詳細描述

Lync Server 可以提供使用者與其他人共用大量目前狀態資訊的機會：他們可以發佈自己的相片、提供詳細的位置資訊，並將自己的目前狀態資訊自動提供給組織內的每一個人 (而不是只將此資訊提供給其連絡人清單上的人)。

有些使用者很高興有這個機會能將此資訊提供給他們的同事，但也有一些使用者不願意分享此資料 (例如，許多人對於將他們的照片放在目前狀態資料中會有疑慮)。一般而言，使用者可控制是否分享哪些資訊；例如，使用者可勾選或取消勾選核取方塊，來控制是否要與他人分享其位置資訊。此外，隱私權組態 Cmdlet 可讓系統管理員管理使用者的隱私權設定。在某些情況下，系統管理員可以啟用或停用設定；舉例來說，如果 AutoInitiateContacts 屬性設為 True，則會自動將小組成員新增至每個使用者的連絡人清單中；如果設為 False，則不會將小組成員自動新增至每個使用者的連絡人清單中。

在其他狀況下，系統管理員可在 Lync Server 中設定預設值，同時仍讓使用者有權利變更這些值。例如會預設發佈使用者的位置資料，但使用者有權利停止發佈位置。透過將 PublishLocationDataByDefault 屬性設為 False，系統管理員可變更此行為：在此狀況下，預設不會發佈位置資料，但使用者仍有權利選擇發佈此資料。

隱私權組態設定會套用在全域範圍、網站範圍與服務範圍 (雖然僅適用於 User Server 服務)。**Get-CsPrivacyConfiguration** Cmdlet 讓您能夠擷取組織目前所使用之所有隱私組態設定的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsPrivacyConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPrivacyConfiguration"}

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
<td><p>讓您能夠使用萬用字元，傳回一或多個隱私組態設定的集合。例如，若要傳回已在網站範圍內設定的所有設定，您可以使用下列語法：-Filter &quot;site:*&quot;。若要傳回在服務範圍所設定的所有設定，請使用下列語法：-Filter &quot;service:*&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要擷取之隱私組態設定的唯一識別碼。若要傳回全域設定，請使用下列語法：-Identity global。若要傳回在此網站範圍設定的設定，請使用下列語法：-Identity site:Redmond。若要修改服務層級的設定，請使用下列語法：-Identity service:UserServer:atl-cs-001.litwareinc.com</p>
<p>若未指定此參數，則 <strong>Get-CsPrivacyConfiguration</strong> Cmdlet 會傳回組織目前所使用的所有隱私組態設定。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區 的本機複本擷取私密性組態資料，而非從 中央管理存放區 本身擷取。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要擷取隱私權組態設定之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。</p>
<p>例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行下列命令傳回每個租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>倘若使用的是 Windows PowerShell 遠端工作階段並僅連線至 商務用 Skype Online，則無需包含 Tenant 參數。相反地，系統將會根據您的連線資訊自動填入租用戶識別碼。Tenant 參數主要用於混合式部署。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsPrivacyConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsPrivacyConfiguration** Cmdlet 會傳回現有的 Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PrivacyConfiguration 物件執行個體。

## 請參閱

#### 其他資源

[New-CsPrivacyConfiguration](new-csprivacyconfiguration.md)  
[Remove-CsPrivacyConfiguration](remove-csprivacyconfiguration.md)  
[Set-CsPrivacyConfiguration](set-csprivacyconfiguration.md)

