---
title: Import-CsLisConfiguration
TOCTitle: Import-CsLisConfiguration
ms:assetid: 579c0c38-311b-4961-b924-11731403d9f2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398380(v=OCS.15)
ms:contentKeyID: 49290981
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Import-CsLisConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

從備份檔案匯入 Enterprise Voice 的增強型 9-1-1 (E9-1-1) 組態。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Import-CsLisConfiguration -FileName <String> <COMMON PARAMETERS>

    Import-CsLisConfiguration -ByteInput <Byte[]> <COMMON PARAMETERS>

    COMMON PARAMETERS:

## 範例

## 範例 1

此範例從名稱為 E911Config.back 的備份檔案將 E9-1-1 組態匯入至位置組態資料庫。

    Import-CsLisConfiguration -FileName C:\E911Config.bak

## 範例 2

範例 2 示範如何使用 **Import-CsLisConfiguration** Cmdlet 的 ByteInput 參數。第 1 行所示為呼叫 **Export-CsLisConfiguration** Cmdlet 加上 AsBytes 參數。此命令的輸出為包含 LIS 組態的位元組陣列。系統會將此陣列指派給 $lisconfig 變數。第二行會呼叫 **Import-CsLisConfiguration** Cmdlet。ByteInput 參數會收到 $lisconfig 的值，此值是包含我們所匯出位元組陣列的變數。這會將該位元組陣列匯回位置組態。

    $lisconfig = Export-CsLisConfiguration -AsBytes 
    Import-CsLisConfiguration -ByteInput $lisconfig

## 範例 3

範例 3 是範例 2 的更完整版，第一行相同，我們呼叫 **Export-CsLisConfiguration** Cmdlet 並搭配 AsBytes 參數，將 LIS 組態在 $lisconfig 變數中儲存為位元組陣列。此範例剩下的部分則顯示如何將該組態儲存到檔案中，再將組態匯回位置組態資料庫。

在第 2 行中，我們將 $lisconfig 的內容 (此內容是代表 LIS 組態的位元組陣列) 管線傳送到 Windows PowerShell**Set-Content** Cmdlet。將值指派給 **Set-Content** Cmdlet 的兩個參數：Path 與 Encoding。將要儲存組態的檔案完整路徑和檔案名稱指派給 Path 參數。在 Encoding 參數使用 byte 值，以確保組態會儲存為位元組陣列。

最後，在第三行會將組態匯回至位置組態資料庫。首先要呼叫 **Get-Content** Cmdlet 從檔案擷取內容。將 0 值傳遞到 ReadCount 屬性，這會告訴 **Get-Content** Cmdlet 一次讀取該檔案的所有內容，而非一次讀取一行。再次在 Encoding 參數使用 byte 值，指定我們要從檔案中讀取哪一類型的資料。最後將檔案名稱傳遞到 Path 參數。我們使用 **Get-Content** Cmdlet 所讀取的檔案內容會管線傳送到 **Import-CsLisConfiguration** Cmdlet，此 Cmdlet 會將儲存的組態匯入到位置資料庫。

    $lisconfig = Export-CsLisConfiguration -AsBytes
    $listconfig | Set-Content -Path C:\E911Config.bak -Encoding byte
    Get-Content -ReadCount 0 -Encoding byte -Path C:\E911Config.bak | Import-CsLisConfiguration

## 詳細描述

視組織規模的不同，在組織中實作 E9-1-1 會涉及將數千個子網路、連接埠、交換器以及無線存取點與位置進行對應。E9-1-1 組態也包含 E9-1-1 網路路由供應商提供的位置資訊伺服器 (LIS) 相關資訊，和位置、市街地址以及它們是否已經驗證的資訊。實作 E9-1-1 需要大量的資訊與設定，強烈建議您定期備份整個組態。您可以呼叫 **Export-CsLisConfiguration** Cmdlet 將整個 E9-1-1 組態備份到檔案。呼叫 **Import-CsLisConfiguration** Cmdlet 會從該檔案還原組態。

透過呼叫此 Cmdlet 來還原組態，並不會覆寫現有的組態。它會插入已移除的資訊，但不會移除在備份檔案建立後才新增的現有記錄。

重要：因為從備份中匯入並不會取代現有的記錄，任何已變更的記錄均將還原，而您可能只剩孤立的位置。例如，假設您已定義一個 Location 值為 Building30/Room10 的無線存取點 (WAP)。您應呼叫 **Export-CsLisConfiguration** Cmdlet 備份您的組態。之後，您將無線存取點的 Location 屬性修改成 Building30/Rooms20-40。如果您接著呼叫 **Import-CsLisConfiguration** Cmdlet 來還原備份的組態，該 WAP 的位置會是 Building30/Room10 (備份前的位置)，但 Building30/Rooms20-40 的位置仍然存在於位置組態資料庫中。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Import-CsLisConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Import-CsLisConfiguration"}

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
<td><p><em>ByteInput</em></p></td>
<td><p>必要</p></td>
<td><p>System.Byte[]</p></td>
<td><p>傳遞到此參數的值是包含 LIS 組態位元組陣列的變數，此陣列是由 <strong>Export-CsLisConfiguration</strong> Cmdlet 加上 AsBytes 參數所建立的。</p></td>
</tr>
<tr class="even">
<td><p><em>FileName</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>表示您要從備份檔匯入組態時，該備份檔的名稱。您無法指定 FileName 與 ByteInput。每次呼叫此 Cmdlet 都只能夠與這兩個參數的其中一個搭配使用。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Byte\[\]。接受來自匯出的 LIS 組態的位元組陣列。位元組陣列必須以單一記錄傳送。請參閱範例 3。

## 傳回類型

這個 Cmdlet 不會傳回值。

## 請參閱

#### 其他資源

[Export-CsLisConfiguration](export-cslisconfiguration.md)  
[Publish-CsLisConfiguration](publish-cslisconfiguration.md)  
[Unpublish-CsLisConfiguration](unpublish-cslisconfiguration.md)  
[Debug-CsLisConfiguration](debug-cslisconfiguration.md)  
[Test-CsLisConfiguration](test-cslisconfiguration.md)

