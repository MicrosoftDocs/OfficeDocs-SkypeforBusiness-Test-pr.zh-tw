---
title: Get-CsTenant
TOCTitle: Get-CsTenant
ms:assetid: 7b642117-5ca7-4a5b-bca7-16b0ae694ae2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994044(v=OCS.15)
ms:contentKeyID: 52056132
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTenant

 

_**上次修改主題的時間：** 2015-03-09_

傳回已設定供組織使用之 商務用 Skype Online 租用戶的相關資訊。租用戶是指線上使用者群組。在許多情況下，您可能只需要單一租用戶。不過，如果不同的使用者群組有不同的管理需求，商務用 Skype Online 可為具有多個租用戶的單一組織提供支援。

Get-CsTenant 僅可與 商務用 Skype Online 搭配使用。

## 語法

    Get-CsTenant [[-Identity] <OUIdParameter>] [-Filter <String>] [-ResultSize <Unlimited`1>] [-Verbose]

## 範例

## 範例 1

範例 1 所示的命令會傳回設定供組織使用之所有租用戶的資訊。

    Get-CsTenant

## 範例 2

範例 2 會傳回單一租用戶 (即 Identity 為 "bf19b7db-6960-41e5-a139-2aa373474354" 的租用戶) 的資訊。

    Get-CsTenant -Identity "bf19b7db-6960-41e5-a139-2aa373474354"

## 範例 3

上述命令顯示另一種可傳回單一租用戶資訊的方式。在此範例中，作法是一起加入 Filter 參數與篩選值 {DisplayName –eq "Fabrikam"}。該語法只會傳回顯示名稱為 Fabrikam 之租用戶的相關資訊。

    Get-CsTenant -Filter {DisplayName -eq "Fabrikam"}

## 範例 4

範例 4 所示的命令會傳回 ServiceInstance 等於 "LitwareincCommunicationsOnline/San Antonio" 之所有租用戶的資訊。為達此目的，命令會加入 Filter 參數及篩選值 {ServiceInstance -eq "LitwareincCommunicationsOnline/San Antonio"}。此篩選值會將傳回的資料限制為 ServiceInstance 屬性等於 (-eq) "LitwareincCommunicationsOnline/San Antonio" 的租用戶。

    Get-CsTenant -Filter {ServiceInstance -eq "LitwareincCommunicationsOnline/San Antonio"}

## 範例 5

範例 5 會傳回國家或地區顯示名稱等於 Australia 之所有租用戶的資訊。作法是搭配使用 Filter 參數及參數值 {CountryOrRegionDisplayName -eq "Australia"}。

    Get-CsTenant -Filter {CountryOrRegionDisplayName -eq "Australia"}

## 詳細描述

在 商務用 Skype Online 中，租用戶代表在服務上擁有帳戶的使用者群組。許多組織只需要單一租用戶來容納其所有使用者帳戶。不過，商務用 Skype Online 的管理通常會以租用戶為單位逐一執行。這表示相同租用戶中的所有使用者都會有相同的語音原則、相同的同盟組態設定等等。如果您需要以某種方式管理部分使用者，並以另一種方式管理其他使用者，您可以考慮使用多個租用戶，讓每個租用戶有專屬的原則和設定集合。

不論擁有的租用戶數目為何，都可以使用 **Get-CsTenant** Cmdlet 傳回這些租用戶的相關資訊。

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
<td><p>可讓您使用 Active Directory 屬性傳回資料，而且不必指定完整的 Active Directory 辨別名稱。例如，若要使用租用戶顯示名稱擷取租用戶，請使用類似下列的語法：</p>
<p>Get-CsTenant –Filter {DisplayName –eq &quot;FabrikamTenant&quot;}</p>
<p>若要傳回使用 Fabrikam 網域的所有租用戶，請使用下列語法：</p>
<p>Get-CsTenant –Filter {Domains –like &quot;*fabrikam*&quot;}</p>
<p>Filter 參數使用的 Windows PowerShell 篩選語法與 Where-Object Cmdlet 相同。</p>
<p>同一個命令中不可同時使用 Identity 參數與 Filter 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>租用戶的 Active Directory 辨別名稱。例如：</p>
<p>-Identity &quot;OU=bf19b7db-6960-41e5-a139-2aa373474354,OU=OCS Tenants,dc=litwareinc,dc=com&quot;</p>
<p>如果您未加入 Identity 或 Filter 參數，則 <strong>Get-CsTenant</strong> Cmdlet 會傳回您所有租用戶的資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited`1</p></td>
<td><p>可讓您限制 Cmdlet 傳回的記錄數。例如，若要傳回 7 個租用戶 (不考慮樹系中的租用戶數目)，請加入 ResultSize 參數並將參數值設為 7。請注意，系統無法保證傳回哪 7 個使用者。</p>
<p>結果大小可以設為 0 到 2147483647 (含) 之間的任何數字。如果設為 0，命令會執行，但不會傳回資料。如果您將租用戶設為 7，但樹系中只有三個連絡人，則命令會傳回那三個租用戶，然後完成執行且不會出現錯誤。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

**Get-CsTenant** Cmdlet 接受以管道方式傳送的 Microsoft.Rtc.Management.ADConnect.Schema.TenantObject 物件執行個體，以及代表 商務用 Skype Online 租用戶之 Identity 的字串值 (例如 "OU=bf19b7db-6960-41e5-a139-2aa373474354,OU=OCS Tenants,dc=vdomain,dc=com")。

## 傳回類型

**Get-CsTenant** Cmdlet 會傳回 Microsoft.Rtc.Management.ADConnect.Schema.TenantObject 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsOnlineUser](get-csonlineuser.md)

