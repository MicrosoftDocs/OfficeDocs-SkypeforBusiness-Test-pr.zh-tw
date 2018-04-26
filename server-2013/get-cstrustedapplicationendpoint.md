---
title: Get-CsTrustedApplicationEndpoint
TOCTitle: Get-CsTrustedApplicationEndpoint
ms:assetid: f66ac464-31ef-4aa3-9b79-f9e67ebc1475
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413035(v=OCS.15)
ms:contentKeyID: 49292839
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTrustedApplicationEndpoint

 

_**上次修改主題的時間：** 2015-03-09_

擷取一或多個信任之應用程式端點的資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsTrustedApplicationEndpoint [-Identity <UserIdParameter>] [-ApplicationId <String>] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Filter <String>] [-OU <OUIdParameter>] [-ResultSize <Unlimited>] [-TrustedApplicationPoolFqdn <Fqdn>]

## 範例

## 範例 1

此範例會擷取 Lync Server 部署內所定義之所有受信任應用程式端點的資訊。

    Get-CsTrustedApplicationEndpoint

## 範例 2

範例 2 會擷取 SIP 位址為 endpoint1@litwareinc.com 之應用程式端點連絡人的資訊，請注意，在使用 SIP 位址做為 Identity 時，需要使用 sip: 首碼。

    Get-CsTrustedApplicationEndpoint -Identity "sip:endpoint1@litwareinc.com"

## 範例 3

範例 3 會擷取顯示名稱包含字串 "endpoint" 的所有受信任應用程式端點。為達此目的，命令會使用 Filter 參數。此參數的值可篩選出顯示名稱 (DisplayName) 包含 (-like) 字串端點 (\*endpoint\* - 萬用字元字串端點的前後可以有任何字元，也就是說端點可以出現在顯示名稱中的任何位置) 的端點物件。

    Get-CsTrustedApplicationEndpoint -Filter {DisplayName -like "*endpoint*"}

## 範例 4

範例 4 將傳回與應用程式 tapp2 相關聯的所有受信任應用程式端點。這是藉由將 tapp2 這個 ID 傳給 ApplicationId 參數來達成。請注意，我們並未提供集區 FQDN；這表示如果其 ID 為 tapp2 的應用程式存在多個集區上，則會擷取所有這些應用程式的端點。此命令的下一個部分會將傳回的一或多個物件傳送到 **Select-Object** Cmdlet，這樣只會顯示這些物件的 SipAddress、DisplayName 及 OwnerUrn 屬性。

    Get-CsTrustedApplicationEndpoint -ApplicationId tapp2 | Select-Object SipAddress, DisplayName, OwnerUrn

## 詳細描述

信任的應用程式端點是 Active Directory 連絡人物件，可讓呼叫路由傳送至信任的應用程式。此 Cmdlet 可以擷取 Active Directory 網域服務 中一或多個現有的端點連絡人物件。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsTrustedApplicationEndpoint** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsTrustedApplicationEndpoint"}

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
<td><p>適用於您要擷取的端點之受信任應用程式的應用程式 ID。</p></td>
</tr>
<tr class="even">
<td><p><em>Credential</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>可用來擷取端點的替代認證。您可以呼叫 <strong>Get-Credential</strong> Cmdlet 來擷取 PSCredential 物件。</p></td>
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
<td><p>要修改之應用程式端點的 Identity (辨別名稱)、SIP 位址或顯示名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>端點所在的 OU。</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>可擷取的端點記錄數目上限。</p></td>
</tr>
<tr class="even">
<td><p><em>TrustedApplicationPoolFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>與您要擷取之端點應用程式相關聯的受信任應用程式集區的完整網域名稱 (FQDN)。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

字串。接受代表使用者帳戶之 Identity 的管線字串值。

## 傳回類型

擷取 Microsoft.Rtc.Management.ADConnect.Schema.OCSADApplicationContact 類型的物件。

## 請參閱

#### 其他資源

[New-CsTrustedApplicationEndpoint](new-cstrustedapplicationendpoint.md)  
[Remove-CsTrustedApplicationEndpoint](remove-cstrustedapplicationendpoint.md)  
[Set-CsTrustedApplicationEndpoint](set-cstrustedapplicationendpoint.md)

