---
title: Get-CsConfigurationStoreLocation
TOCTitle: Get-CsConfigurationStoreLocation
ms:assetid: abfda147-02fa-46a5-a988-d83daf4cc455
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412814(v=OCS.15)
ms:contentKeyID: 49291989
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsConfigurationStoreLocation

 

_**上次修改主題的時間：** 2015-03-09_

回報中央管理存放區的 Active Directory 服務控制點位置。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsConfigurationStoreLocation [-GlobalSettingsDomainController <Fqdn>] [-Report <String>]

## 範例

## 範例 1

範例 1 所示的命令會傳回至裝載中央管理存放區之電腦 (或集區) 的 SQL Server 路徑。

    Get-CsConfigurationStoreLocation

## 範例 2

範例 2 是範例 1 所示命令的變化；但在此案例中，當您執行 **Get-CsConfigurationStoreLocation** Cmdlet 時，會包含 Report 參數來指定產生報告的路徑。

    Get-CsConfigurationStoreLocation -Report "C:\Logs\ConfigurationStore.html"

## 詳細描述

Active Directory 網域服務 會使用服務控制指標 (SCP) 來協助電腦尋找服務。例如，當您安裝 Lync Server 時，會建立服務控制點，以提供中央管理存放區的位置資訊，用來維護 Lync Server 資料。需要存取資料庫的電腦會連線至 Active Directory，並使用 SCP 中包含的資訊來協助它們找到正確的電腦，以及正確的 SQL Server 執行個體。

**Get-CsConfigurationStoreLocation** Cmdlet 可用來回報連至執行中央管理存放區之電腦的 SQL Server 路徑 (例如，atl-sql-001.litwareinc.com/rtc)。

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
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>儲存全域設定之網域控制器的完整網域名稱 (FQDN)。如果全域設定是儲存在 Active Directory 的系統容器內，則此參數必須導向根網域控制器。如果全域設定儲存在組態容器中，則會使用任何一個網域控制站，且會省略此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\ConfigurationStore.html&quot;</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsConfigurationStoreLocation** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

字串。**Get-CsConfigurationStoreLocation** Cmdlet 會回報組態存放區的位置。

## 請參閱

#### 其他資源

[Remove-CsConfigurationStoreLocation](remove-csconfigurationstorelocation.md)  
[Set-CsConfigurationStoreLocation](set-csconfigurationstorelocation.md)

