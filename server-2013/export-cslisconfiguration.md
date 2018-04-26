---
title: Export-CsLisConfiguration
TOCTitle: Export-CsLisConfiguration
ms:assetid: 714bd67e-4cd6-4066-a065-59f7e079b6ad
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398539(v=OCS.15)
ms:contentKeyID: 49291282
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Export-CsLisConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

以壓縮格式將 Enterprise Voice 增強型 9-1-1 (E9-1-1) 組態匯出至檔案做為備份之用。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Export-CsLisConfiguration -FileName <String> <COMMON PARAMETERS>

    Export-CsLisConfiguration [-AsBytes <SwitchParameter>] <COMMON PARAMETERS>

    COMMON PARAMETERS:

## 範例

## 範例 1

此範例會從位置資訊伺服器 (LIS) 將整個 E9-1-1 組態匯出到名為 E911Config.bak 的備份檔。

    Export-CsLisConfiguration -FileName C:\E911Config.bak

## 範例 2

在此範例中，LIS 組態會儲存為變數 $lisconfig 中的位元組陣列。

    $lisconfig = Export-CsLisConfiguration -AsBytes

## 範例 3

範例 3 是範例 2 的更完整版，第一行相同，我們呼叫 **Export-CsLisConfiguration** Cmdlet 並搭配 AsBytes 參數，將 LIS 組態在 $lisconfig 變數中儲存為位元組陣列。此範例剩下的部分則顯示如何將該組態儲存到檔案中，再將組態匯回位置組態資料庫。

在第 2 行中，我們將 $lisconfig 的內容 (此內容是代表 LIS 組態的位元組陣列) 管線傳送到 Windows PowerShell**Set-Content** Cmdlet。將值指派給 **Set-Content** Cmdlet 的兩個參數：Path 與 Encoding。將要儲存組態的檔案完整路徑和檔案名稱指派給 Path 參數。在 Encoding 參數使用 byte 值，以確保組態會儲存為位元組陣列。

最後，在第三行會將組態匯回至位置組態資料庫。首先要呼叫 **Get-Content** Cmdlet 從檔案擷取內容。將 0 值傳遞到 ReadCount 屬性，這會告訴 **Get-Content** Cmdlet 一次讀取該檔案的所有內容，而非一次讀取一行。再次在 Encoding 參數使用 byte 值，指定我們要從檔案中讀取哪一類型的資料。最後將檔案名稱傳遞到 Path 參數。我們使用 **Get-Content** Cmdlet 所讀取的檔案內容會管線傳送到 **Import-CsLisConfiguration** Cmdlet，此 Cmdlet 會將儲存的組態匯入到位置資料庫。

    $lisconfig = Export-CsLisConfiguration -AsBytes
    $lisconfig | Set-Content -Path C:\E911Config.bak -Encoding byte
    Get-Content -ReadCount 0 -Encoding byte -Path C:\E911Config.bak  | Import-CsLisConfiguration

## 詳細描述

視組織規模的不同，在企業中實作 E9-1-1 可涉及將數千個子網路、連接埠、交換器以及無線存取點 (WAP) 與位置進行對應。E9-1-1 組態也包含 E9-1-1 網路路由供應商提供的網路服務相關資訊，和位置、市街地址以及它們是否已經驗證的資訊。實作 E9-1-1 需要大量的資訊與設定，建議您定期備份整個組態。您可以使用這個 Cmdlet 將 E9-1-1 組態備份至檔案，該 Cmdlet 會將整個組態儲存為壓縮格式。若要復原組態，請呼叫 **Import-CsLisConfiguration** Cmdlet。

此 Cmdlet 會建立新備份檔案，而不會覆寫現有檔案。這表示呼叫 Cmdlet 所指定的檔案名稱不能是現有檔案的名稱。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Export-CsLisConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Export-CsLisConfiguration"}

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
<td><p><em>FileName</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>您要儲存組態之檔案的路徑和檔案名稱。它不能是現有檔案的名稱。</p>
<p>如果您提供值給 AsBytes 參數，則無法提供值給 FileName 參數。如果您是遠端存取此 Cmdlet，則必須使用 AsBytes 而非 FileName。</p></td>
</tr>
<tr class="even">
<td><p><em>AsBytes</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回組態為位元組陣列。命令的輸出必須被指派至變數供稍後匯入(如果您不指派輸出至變數，代表組態的位元組陣列會向下捲動您的 Lync Server 管理命令介面 視窗)。您無法同時指定 AsBytes 參數和 FileName 參數；每次呼叫此 Cmdlet，只能使用其中一個參數。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

使用 AsBytes 參數時，會傳回位元組陣列 (Byte\[\])。

## 請參閱

#### 其他資源

[Import-CsLisConfiguration](import-cslisconfiguration.md)  
[Debug-CsLisConfiguration](debug-cslisconfiguration.md)  
[Publish-CsLisConfiguration](publish-cslisconfiguration.md)  
[Unpublish-CsLisConfiguration](unpublish-cslisconfiguration.md)  
[Test-CsLisConfiguration](test-cslisconfiguration.md)

