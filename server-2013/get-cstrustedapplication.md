---
title: Get-CsTrustedApplication
TOCTitle: Get-CsTrustedApplication
ms:assetid: e6623931-3bac-4146-92a9-4465396e9fe6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399025(v=OCS.15)
ms:contentKeyID: 49292642
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTrustedApplication

 

_**上次修改主題的時間：** 2015-03-09_

擷取信任之應用程式的設定。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsTrustedApplication [-ApplicationId <String>] [-TrustedApplicationPoolFqdn <String>] <COMMON PARAMETERS>

    Get-CsTrustedApplication [-Identity <ExternalApplicationIdentity>] <COMMON PARAMETERS>

    Get-CsTrustedApplication [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS:

## 範例

## 範例 1

此範例會擷取定義於 Lync Server 部署內所有受信任應用程式的資訊。

    Get-CsTrustedApplication

## 範例 2

範例 2 會擷取 Identity 為 TrustPool.litwareinc.com/urn:application:tapp2 的信任應用程式。請注意，可以省略 urn:application:首碼。**Get-CsTrustedApplication** Cmdlet 會自動新增首碼並擷取正確的應用程式。

    Get-CsTrustedApplication -Identity TrustPool.litwareinc.com/tapp2

## 範例 3

範例 3 會擷取所有受信任應用程式，其識別身分符合指定為 Filter 值的萬用字元字串。在此案例中，利用 Filter 值 \*trust\*，命令會擷取在 Identity 任何位置中具有字串 “trust” 的所有受信任應用程式。此字串可包含於 Identity、集區 FQDN，或應用程式 ID 的任何部分。因此這個命令會擷取含識別身分 (如 TrustedPool.litwareinc.com/urn:application:application1、Pool1.litwareinc.com/urn:application:trustedapp，與 Pool1.litwareinc.com/urn:application:trust) 的受信任應用程式。

    Get-CsTrustedApplication -Filter *trust*

## 範例 4

範例 4 會傳回與範例 2 (其中將 Identity 指定為唯一的參數) 相同的結果。兩個範例間唯一的差異是：範例 2 會根據 Identity 擷取受信任應用程式，由受信任集區 FQDN 加上應用程式 ID 所組成。在此範例中，輸入應用程式 ID 與受信任集區 FQDN 以做為兩個個別參數的值：ApplicationId 與 TrustedApplicationPoolFqdn。

    Get-CsTrustedApplication -ApplicationId tapp2 -TrustedApplicationPoolFqdn TrustPool.litwareinc.com

## 範例 5

範例 5 會擷取集區 TrustPool.litwareinc.com 上的所有受信任應用程式。該範例以呼叫 **Get-CsTrustedApplication** Cmdlet 開始。這會傳回定義於 Lync Server 部署中之所有受信任應用程式的集合。接著將此集合傳送給 **Where-Object** Cmdlet，它會逐項查看集合以找出 TrustedApplicationPoolFqdn 屬性等於 (-eq) TrustPool.litwareinc.com 的集合。

    Get-CsTrustedApplication | Where-Object {$_.TrustedApplicationPoolFqdn -eq "TrustPool.litwareinc.com"}

## 詳細描述

受信任應用程式是由取得信任狀態之第三方開發的應用程式，可做為 Lync Server 的部分執行，但這並不是產品的內建部分。這個 cmdlet 可讓您擷取一或多個受信任應用程式的連接埠，以及可全域路由傳送使用者代理 URI (GRUU) 設定。

當您使用此 Cmdlet 來擷取單一受信任應用程式時，您必須提供 Identity 參數值。Identity 是應用程式常駐之集區的完整網域名稱 (FQDN)，隨後接著正斜線 (/) 和應用程式 ID。例如，TrustPool.litwareinc.com/tapp2，其中 TrustPool.litwareinc.com 是集區 FQDN，而 tapp2 是應用程式 ID。請注意，當您以呼叫此 Cmdlet 的方式擷取應用程式時，您將會看到如下所示的 ID：TrustPool.litwareinc.com/urn:application:tapp2。注意首碼 urn:application:在應用程式名稱 (tapp2) 之前。此首碼是 Identity 的一部分，但是在您指定 Identity 參數值時則不需要。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsTrustedApplication** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsTrustedApplication\\b"}

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
<td><p>應用程式的名稱。可以包含應用程式 ID 首碼，但並非必要。例如，urn:application:tapp1 及 tapp1 的 ApplicationId 值會同時傳回相同的應用程式。如果您提供 ApplicationId 值，您無法提供 Identity 值，但您必須提供 TrustedApplicationPoolFqdn 參數值。</p></td>
</tr>
<tr class="even">
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>包含萬用字元的字串，可讓您根據符合指定之萬用字元字串的 Identity 值來擷取受信任應用程式。識別身分由受信任應用程式集區 FQDN 加上正斜線 (/) 與受信任應用程式 ID 所組成。Filter 值會比對 Identity 的任何部分 (FQDN 與應用程式 ID 兩者)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.ExternalApplicationIdentity</p></td>
<td><p>您要擷取之受信任應用程式的唯一識別碼。Identity 值必須以 &lt;集區 FQDN&gt;/&lt;應用程式識別碼&gt; 格式輸入，其中「集區 FQDN」是應用程式所在之集區的 FQDN，而「應用程式識別碼」是應用程式的名稱。請注意，如有指定 Identity，即不可指定 ApplicationID 或 TrustedApplicationPoolFqdn。</p></td>
</tr>
<tr class="even">
<td><p><em>TrustedApplicationPoolFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>應用程式所在之受信任應用程式集區的 FQDN。如果您提供 TrustedApplicationPoolFqdn 值，您無法提供 Identity 值，但您必須提供 ApplicationID 參數值。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

傳回 Microsoft.Rtc.Management.Xds.DisplayTrustedApplication 類型的物件。

## 請參閱

#### 其他資源

[New-CsTrustedApplication](new-cstrustedapplication.md)  
[Remove-CsTrustedApplication](remove-cstrustedapplication.md)  
[Set-CsTrustedApplication](set-cstrustedapplication.md)

