---
title: Get-CsTenantFederationConfiguration
TOCTitle: Get-CsTenantFederationConfiguration
ms:assetid: e5f836d0-6066-4c23-9594-6e3f1cbd39ef
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994072(v=OCS.15)
ms:contentKeyID: 52056248
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTenantFederationConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回 Microsoft Lync Online 租用戶的同盟組態設定的相關資訊。同盟組態設定是用來決定您的使用者可通訊的網域 (若有的話)。

**Get-CsTenantFederationConfiguration** Cmdlet 僅可與 商務用 Skype Online 搭配使用。

## 語法

    Get-CsTenantFederationConfiguration [[-Identity] <XdsIdentity>] [-Tenant <Nullable`1>] [-LocalStore] [-Verbose] Get-CsTenantFederationConfiguration [-Tenant <Nullable`1>] [-Filter <String>] [-LocalStore] [-Verbose]

## 範例

## 範例 1

練習 1 所示的命令會針對租用戶識別碼為 "bf19b7db-6960-41e5-a139-2aa373474354" 的租用戶傳回同盟組態資訊。您可使用類似下列的命令擷取租用戶識別碼：

Get-CsTenant | Select-Object TenantID

    Get-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354"

請注意，Tenant 參數是選用的。您也可以使用下列語法呼叫 Get-CsTenantFederationConfiguration：

    Get-CsTenantFederationConfiguration

## 範例 2

範例 2 會傳回在同盟允許的清單上針對租用戶 bf19b7db-6960-41e5-a139-2aa373474354 找到之所有網域的相關資訊 (允許的清單代表租用戶可建立同盟的所有網域)。為達成此目的，命令會先呼叫 **Get-CsTenantFederationConfiguration** Cmdlet，傳回指定租用戶的同盟資訊。然後，該資料會以管道方式傳送到 **Select-Object** Cmdlet，以使用 ExpandProperty「展開」AllowedList 屬性。展開屬性僅意味著會以易讀的格式在畫面顯示該屬性中儲存的所有資訊。

    Get-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" | Select-Object -ExpandProperty AllowedList

## 範例 3

上述命令會傳回組織中目前使用之所有租用戶的同盟設定。為執行此工作，命令會先呼叫不含任何參數的 **Get-CsTenant** Cmdlet，以傳回所有可用租用戶的集合。接著，該集合會以管道方式傳送到 **ForEach-Object** Cmdlet。ForEach-Object 會使用屬性值 TenantID (由 **Get-CsTenant** Cmdlet 傳回) 代表租用戶識別碼，以取得集合中的每個租用戶並呼叫 **Get-CsTenantFederationConfiguration** Cmdlet。

    Get-CsTenant | ForEach-Object {Get-CsTenantFederationConfiguration -Tenant $_.TenantId}

## 範例 4

在範例 4，只會傳回不允許與公用使用者同盟之租用戶的同盟設定資訊。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsTenant** Cmdlet，以傳回設定供組織使用之所有租用戶的集合。接著。該集合會以管道方式傳送到 **ForEach-Object** Cmdlet，取得集合中的每個租用戶，然後使用 **Get-CsTenantFederationConfiguration** Cmdlet 傳回同盟設定資訊。接下來，整個同盟設定資訊集會以管道方式傳送到 **Where-Object** Cmdlet，以僅挑出 AllowPublicUsers 屬性等於 (-eq) $False 的租用戶。

    Get-CsTenant | Select-Object TenantId | ForEach-Object {Get-CsTenantFederationConfiguration -Tenant $_.TenantId} | Where-Object {$_.AllowPublicUsers -eq $False}

## 詳細描述

同盟是一種服務，可讓使用者與其他網域的使用者交換 IM 和目前狀態資訊。有了 Lync Online，系統管理員就可以使用同盟組態設定來管理：

  - 使用者是否可以和其他網域的人員通訊，如果可以，則允許和哪些網域通訊。

  - 使用者是否可與在公用 IM 及目前狀態提供者 (如 Windows Live、AOL 和 Yahoo) 上擁有帳戶的人員通訊。

**Get-CsTenantFederationConfiguration** Cmdlet 可讓系統管理員傳回其 Lync Online 租用戶的同盟資訊。這個 Cmdlet 也可用於檢閱允許和封鎖清單 (這些清單列出允許及不允許使用者通訊的網域)。不過，系統管理員必須使用 **Get-CsTenantPublicProvider** Cmdlet 才能查看使用者獲允許可與之通訊的公用 IM 和目前狀態提供者。

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
<td><p>可讓您使用萬用字元，以傳回租用戶同盟組態設定的集合。由於每個租用戶限定必須是單一全域的同盟組態設定集合，所以不需要使用 Filter 參數。不過，這是 <strong>Get-CsTenantFederationConfiguration</strong> Cmdlet 的有效語法：</p>
<p>Get-CsTenantFederationConfiguration –Tenant &quot;bf19b7db-6960-41e5-a139-2aa373474354&quot; –Filter &quot;g*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>指定要傳回之租用戶同盟組態設定的集合。由於每個租用戶限定必須是單一全域的同盟設定集合，因此在呼叫 <strong>Get-CsTenantFederationConfiguration</strong> Cmdlet 時不需要加入此參數。如果選擇使用 Identity 參數，您也必須包含 Tenant 參數。例如：</p>
<p>Get-CsTenantFederationConfiguration -Tenant &quot;bf19b7db-6960-41e5-a139-2aa373474354&quot; –Identity &quot;global&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取租用戶同盟組態資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>正在傳回其同盟設定之租用戶帳戶的全域唯一識別碼 (GUID)，例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行下列命令傳回每個租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>如果您正在使用 Windows PowerShell 的遠端工作階段，並且僅連線至 商務用 Skype Online，您不需要包含 Tenant 參數，而是將會根據您的連線資訊自動填入租用戶識別碼。Tenant 參數主要用於混合部署。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Get-CsTenantFederationConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsTenantFederationConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.TenantFederationSettings 物件的執行個體。

## 請參閱

#### 其他資源

[Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md)

