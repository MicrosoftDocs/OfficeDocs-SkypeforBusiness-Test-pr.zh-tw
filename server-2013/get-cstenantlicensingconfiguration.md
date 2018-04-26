---
title: Get-CsTenantLicensingConfiguration
TOCTitle: Get-CsTenantLicensingConfiguration
ms:assetid: 0df23143-f1aa-4850-b0f7-750422762925
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362770(v=OCS.15)
ms:contentKeyID: 56269061
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTenantLicensingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

表示指定租用戶的授權資訊是否提供於 Lync 系統管理中心。

此 Cmdlet 僅可與 Lync Online 搭配使用。

## 語法

    Get-CsTenantLicensingConfiguration [-Filter] <Object>] [-Identity] <Object>] [-Tenant] <Object>] [-LocalStore]

## 詳細說明

Get-CsTenantLicensingConfiguration Cmdlet 可表示指定租用戶的授權資訊是否提供於 Lync 系統管理中心。此 Cmdlet 會傳回類似以下資訊：

Identity : Global  
Status : Enabled

若是 Status 為 Enabled，則授權資訊會提供於 Lync 系統管理中心。如果不是，則授權資訊並不會提供於 Lync 系統管理中心。

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
<td><p><strong>Filter</strong></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您使用萬用字元傳回租用戶授權組態設定集合。因為各個租用戶限制為授權組態設定的單一全域集合，因此無需使用 Filter 參數。</p></td>
</tr>
<tr class="even">
<td><p><strong>Identity</strong></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>指定要傳回的租用戶授權組態設定集合。因為各個租用戶限制為授權設定的單一全域集合，因此在呼叫 Get-CsTenantLicensingConfiguration Cmdlet 時無需包含此參數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>LocalStore</strong></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取租用戶授權組態資料，而非從中央管理存放區本身擷取。</p></td>
</tr>
<tr class="even">
<td><p><strong>Tenant</strong></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要傳回其授權設定之租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行下列命令傳回各個租用戶的租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Get-CsTenantLicensingConfiguration Cmdlet 不接受以管線方式輸入。

## 傳回類型

Get-CsTenantLicensingConfiguration Cmdlet 會傳回 Deserialized.Microsoft.Rtc.Management.WritableConfig.Settings.TenantConfiguration.TenantLicensingConfiguration 物件的執行個體。

## 範例

範例 1 所示的命令會傳回目前租用戶的授權組態資訊：

    Get-CsTenantLicensingConfiguration

