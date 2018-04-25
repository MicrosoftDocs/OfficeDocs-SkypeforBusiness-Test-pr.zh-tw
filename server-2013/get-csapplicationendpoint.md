---
title: Get-CsApplicationEndpoint
TOCTitle: Get-CsApplicationEndpoint
ms:assetid: 820d3bbd-0348-4272-bdb3-c3d612d0836a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398655(v=OCS.15)
ms:contentKeyID: 49291499
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsApplicationEndpoint

 

_**上次修改主題的時間：** 2015-03-09_

擷取應用程式服務的端點。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsApplicationEndpoint [-Identity <UserIdParameter>] [-ApplicationId <String>] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Filter <String>] [-OU <OUIdParameter>] [-PoolFqdn <Fqdn>] [-ResultSize <Unlimited>]

## 範例

## 範例 1

此範例會擷取 Lync Server 部署內定義之所有應用程式端點的資訊。

    Get-CsApplicationEndpoint

## 範例 2

範例 2 會擷取所有其顯示名稱中出現字串 “endpoint” 的應用程式端點。為達此目的，命令會使用 Filter 參數。利用此參數值進行篩選，可以尋找顯示名稱 (DisplayName) 包含 (-like) 字串端點 (\*endpoint\* - 萬用字元代表字串端點前後的任意字元，表示端點可以出現在顯示名稱中的任意位置) 的端點物件。

    Get-CsApplicationEndpoint -Filter {DisplayName -like "*endpoint*"}

## 範例 3

範例 3 會傳回所有與應用程式 urn:application:tapp2 相關聯的應用程式端點。這是藉由將 tapp2 這個 ID 傳給 ApplicationId 參數來達成。請注意，我們並未提供集區 FQDN；這表示如果其 ID 為 tapp2 的應用程式存在多個集區上，則會擷取所有這些應用程式的端點。此命令的下個部分會將傳回的物件傳送至 **Select-Object** Cmdlet，以只顯示這些物件的 Identity、SipAddress、DisplayName 和 OwnerUrn 屬性。

    Get-CsApplicationEndpoint -ApplicationId tapp2 | Select-Object Identity, SipAddress, DisplayName, OwnerUrn

## 詳細描述

此 Cmdlet 會從 Active Directory 網域服務 擷取一或多個應用程式連絡人。這些物件儲存於 Active Directory 內 RTC 服務的應用程式連絡人容器中。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsApplicationEndpoint** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsApplicationEndpoint"}

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
<td><p><em>ApplicationId</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>您要擷取之應用程式端點的應用程式識別碼。應用程式 ID 是端點 OwnerUrn 屬性的值。例如，如果 OwnerUrn 屬性的值為 urn:application:Caa，則應用程式 ID 為 urn:application:Caa。但是，您只能輸入尾碼 (在此範例中為 Caa) 來擷取端點。例如：-ApplicationId Caa</p></td>
</tr>
<tr class="even">
<td><p><em>Credential</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>將用於繼續執行 Get 作業的替代認證。您可以呼叫 Windows PowerShell Cmdlet <strong>Get-Credential</strong> 來擷取 PSCredential 物件。</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>容許您指定網域控制站。若未指定網域控制站，則會使用第一個可用的網域控制站。</p></td>
</tr>
<tr class="even">
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您篩選 Lync Server 的特定屬性來限制傳回的資料。例如，您可以將傳回的資料限制在其顯示名稱或 SIP 位址符合特定萬用字元模式的連絡人。</p>
<p>Filter 參數使用的 Windows PowerShell 篩選語法與 <strong>Where-Object</strong> Cmdlet 相同。例如，只傳回已啟用 Enterprise Voice 之連絡人的篩選看起來如下所示：{EnterpriseVoiceEnabled -eq $True}，其中 EnterpriseVoiceEnabled 代表 Active Directory 屬性；-eq 代表比較運算子 (等於)；$True (內建的 Windows PowerShell 變數) 代表篩選值。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>要擷取之應用程式端點的 Identity、SIP 位址或顯示名稱。Identity 由端點的辨別名稱組成。這通常會包含一個全域唯一識別碼 (GUID) 做為 CN 的一部分，例如：CN={8811fefe-e0bb-4fab-ae39-7aaeddd423dc},CN=Application Contacts,CN=RTC Service,CN=Services,CN=Configuration,DC=Vdomain,DC=com。</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>端點所在的組織單位 (OU)。</p></td>
</tr>
<tr class="odd">
<td><p><em>PoolFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>應用程式端點所在之集區的完整網域名稱 (FQDN)。</p></td>
</tr>
<tr class="even">
<td><p><em>ResultSize</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>可擷取的端點記錄數目上限。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

字串。接受代表應用程式端點之 Identity 的管線字串值。

## 傳回類型

擷取 Microsoft.Rtc.Management.ADConnect.Schema.OCSADApplicationContact 類型的物件。

## 請參閱

#### 其他資源

[Move-CsApplicationEndpoint](move-csapplicationendpoint.md)

