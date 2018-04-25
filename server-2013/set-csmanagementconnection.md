---
title: Set-CsManagementConnection
TOCTitle: Set-CsManagementConnection
ms:assetid: f7cf19ba-6c56-4f74-9757-843e1ca0c9a1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413045(v=OCS.15)
ms:contentKeyID: 49292852
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsManagementConnection

 

_**上次修改主題的時間：** 2015-03-09_

修改 中央管理存放區的管理連線。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsManagementConnection -Connection <String> -StoreProvider <FileSystem | Sql | Memory> [-Confirm [<SwitchParameter>]] [-EnableCaching <$true | $false>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會變更連至在 atl-sql-001.litwareinc.com 電腦上找到之 SQL Server 執行個體 rtcbackup 的管理連線。

    Set-CsManagementConnection -StoreProvider Sql -Connection "atl-sql-001.litwareinc.com\rtcbackup"

## 範例 2

在範例 2 中，管理連線已設定為檔案系統，更明確地說，是設定為本機電腦上的資料夾 C:\\TestTopology。

    Set-CsManagementConnection -StoreProvider FileSystem -Connection "C:\TestTopology"

## 詳細描述

Lync Server 的組態資料儲存在 中央管理存放區中。 Windows PowerShell 和管理複本服務都必須能找到此資料庫。安裝 Lync Server 時，在 Active Directory 網域服務 中會建立一個服務控制點，提供有關此資料庫的位置資訊。通常，電腦要靠這個服務控制點連線到 中央管理存放區。如果想知道有關此連線背後的詳細資訊 (亦即，如果您想知道 中央管理存放區 在哪部電腦上執行，連至該 中央管理存放區 的 SQL Server 連線相關資訊)，只需執行 **Get-CsManagementConnection** Cmdlet 即可。

大致上來說，在設定管理連線之後，不需變更該連線。但是，在發生硬體或軟體失敗時，您可能需要暫時使用單一連線；例如，您可以將電腦設定為可從本機複本作業。 **Set-CsManagementConnection** Cmdlet 會給予您一種方法，來提供 中央管理存放區 的新位置。

請注意，使用暫時管理連線時對 Lync Server 所進行的任何變更，在切換回原始連線時將不會持續存在。(執行 **Remove-CsManagementConnection** Cmdlet 就能切換回來)。例如，假設您決定暫時使用檔案系統來做為存放區提供者。您變更管理連線，然後建立數個新的語音原則 (其中每個原則都將具現化為 XML 檔案)。在切換回原始管理連線時，這些新的語音原則將會消失；這是因為它們不曾記錄於現在使用的 中央管理存放區 中。

也請您記住，藉由執行此 Cmdlet 所做的變更只會影響本機電腦。您無法使用 **Set-CsManagementConnection** Cmdlet 變更其他電腦上的管理連線。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsManagementConnection** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。

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
<td><p><em>Connection</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>用來做為管理連線之 SQL Server 執行個體或檔案系統資料夾的位置資訊。</p>
<p>例如，如果新的管理連線是連至 atl-sql-001.litwareinc.com 電腦上名為 rtcbackup 的 SQL Server 執行個體，請使用下列語法：-Connection &quot;atl-sql-001.litwareinc.com\rtcbackup&quot;。</p>
<p>如果想要建立連至資料夾 C:\TestTopology 的管理連線，請使用下列語法：-Connection &quot;C:\TestTopology&quot;。如果資料夾不存在， <strong>Set-CsManagementConnection</strong> Cmdlet 將建立資料夾。</p></td>
</tr>
<tr class="even">
<td><p><em>StoreProvider</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Store.StoreProvider</p></td>
<td><p>指出用於組態資訊的後端存放區類型。若要在 SQL Server 中儲存組態資料，請以類似下列的方式來設定 StoreProvider：-StoreProvider Sql。若要將組態資料儲存至檔案系統，請使用下列語法：-StoreProvider FileSystem。除非受到 Microsoft 支援人員的指示，否則不應修改 StoreProvider 屬性。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableCaching</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True ($True) 時，會啟用管理連線的快取。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Set-CsManagementConnection** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Set-CsManagementConnection** Cmdlet 不會傳回值或物件，而是會設定 Microsoft.Rtc.Management.Store.StoreProvider 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsManagementConnection](get-csmanagementconnection.md)  
[Remove-CsManagementConnection](remove-csmanagementconnection.md)  
[Set-CsConfigurationStoreLocation](set-csconfigurationstorelocation.md)

