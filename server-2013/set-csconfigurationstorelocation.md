---
title: Set-CsConfigurationStoreLocation
TOCTitle: Set-CsConfigurationStoreLocation
ms:assetid: 1c69a872-8e78-4c78-ba27-f20f04dce59f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398258(v=OCS.15)
ms:contentKeyID: 49290260
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsConfigurationStoreLocation

 

_**上次修改主題的時間：** 2015-03-09_

設定中央管理存放區的 Active Directory 服務控制點。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsConfigurationStoreLocation -SqlServerFqdn <Fqdn> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalSettingsDomainController <Fqdn>] [-MirrorSqlInstanceName <String>] [-MirrorSqlServerFqdn <Fqdn>] [-Report <String>] [-SkipLookup <SwitchParameter>] [-SqlInstanceName <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令設定 Lync Server 中央管理存放區的 Active Directory 服務控制點。在此範例中，SCP 會指向電腦 atl-sql-001.litwareinc.com 以及 SQL Server 執行個體 Rtc。

    Set-CsConfigurationStoreLocation -SqlServerFqdn atl-sql-001.litwareinc.com -SqlInstanceName Rtc

## 範例 2

範例 2 所示的命令是範例 1 所示命令的另一種變化。此命令也設定 Lync Server 中央管理存放區的 Active Directory SCP。除此之外，與此作業成功 (或失敗) 相關的資訊會記錄到檔案 C:\\Logs\\Store\_Location.html 中。您可以加入 Report 參數加上記錄檔的完整路徑來產生此記錄檔。

    Set-CsConfigurationStoreLocation -SqlServerFqdn atl-sql-001.litwareinc.com -SqlInstanceName Rtc -Report C:\Logs\Store_Location.html

## 詳細描述

Active Directory 網域服務 會使用服務控制指標 (SCP) 來協助電腦尋找服務。例如，當您安裝 Lync Server 時，會建立服務控制點，以提供中央管理存放區的位置資訊，用來維護 Lync Server 資料。需要存取資料庫的電腦會連線至 Active Directory，並使用 SCP 中包含的資訊來協助它們找到正確的電腦，以及正確的 SQL Server 執行個體。

請注意，當您安裝 Lync Server 時，會自動為您建立中央管理存放區的 SCP。如果您需要將該資料庫移至其他電腦，或是您需要將該資料庫移至不同的 SQL Server 執行個體，您就需要更新對應的服務控制指標。此工作可以使用 **Set-CsConfigurationStoreLocation** Cmdlet 執行。當您執行時，**Set-CsConfigurationStoreLocation** Cmdlet 會在 Active Directory 中搜尋 SqlServer 參數所指定的電腦。然後，此 Cmdlet 會將儲存位置設定為該電腦的 FQDN。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsConfigurationStoreLocation** Cmdlet：RTCUniversalServerAdmins。

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
<td><p><em>SqlServerFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>安裝有中央管理存放區之電腦的完整網域名稱 (FQDN)。例如：-SqlServer atl-sql-001.litwareinc.com。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>儲存全域設定之網域控制站的 FQDN。如果全域設定是儲存在 Active Directory 的系統容器內，則此參數必須導向根網域控制器。如果全域設定儲存在組態容器中，則會使用任何一個網域控制站，且會省略此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>MirrorSqlInstanceName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>包含 Lync Server 鏡像資料庫表格與資料之 SQL Server 執行個體的名稱。例如：-SqlInstanceName &quot;rtc&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>MirrorSqlServerFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>已安裝中央管理存放區鏡像資料庫之電腦的完整網域名稱 (FQDN)。例如：-SqlServer atl-mirror-001.litwareinc.com。</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\ConfigurationStore.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>SkipLookup</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如果加上此參數，則 <strong>Set-CsConfigurationStoreLocation</strong> Cmdlet 將不會驗證指定的電腦及指定的 SQL Server 執行個體是否可使用，而只會變更服務控制指標。</p>
<p>若未加入此參數，則在變更 SCP 前，必須能夠使用指定的電腦及指定的 SQL Server 執行個體。</p></td>
</tr>
<tr class="odd">
<td><p><em>SqlInstanceName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>包含 Lync Server 表格與資料之 SQL Server 執行個體的名稱。例如：-SqlInstanceName &quot;rtc&quot;。</p></td>
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

無。**Set-CsConfigurationStoreLocation** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Set-CsConfigurationStoreLocation** Cmdlet 不會傳回任何物件或值。

## 請參閱

#### 其他資源

[Get-CsConfigurationStoreLocation](get-csconfigurationstorelocation.md)  
[Remove-CsConfigurationStoreLocation](remove-csconfigurationstorelocation.md)

