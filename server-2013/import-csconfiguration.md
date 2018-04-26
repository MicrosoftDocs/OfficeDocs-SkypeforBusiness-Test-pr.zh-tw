---
title: Import-CsConfiguration
TOCTitle: Import-CsConfiguration
ms:assetid: 9a9c27f2-313c-4327-aeed-c47852a831ec
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398800(v=OCS.15)
ms:contentKeyID: 49291773
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Import-CsConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

將您的 Lync Server 拓撲、原則及組態設定匯入中央管理存放區或本機電腦。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Import-CsConfiguration -ByteInput <Byte[]> <COMMON PARAMETERS>

    Import-CsConfiguration -FileName <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會從名稱為 C:\\Config.zip 的檔案將目前的拓撲、組態設定及原則匯入到中央管理存放區。

    Import-CsConfiguration -FileName "C:\Config.zip"

## 範例 2

範例 2 顯示一開始時如何將資料複寫到位於周邊網路上的電腦。在此範例中，組態資料已匯出到名稱為 Config.zip 的檔案；此檔案已複製到位於周邊網路上該部電腦上的 C:\\ 資料夾。接著使用 Import-CsConfiguration 匯入該資料，並加上 LocalStore 參數，讓資料匯入到本機電腦，而非中央管理存放區。

    Import-CsConfiguration -FileName "C:\Config.zip" -LocalStore

## 範例 3

範例 3 所示的兩個命令會匯出目前的拓撲、組態設定及原則，然後將該資料匯入本機電腦，且全都不需要使用 .ZIP 檔案。為達成此目的，第一個命令使用 **Export-CsConfiguration** Cmdlet 和 AsBytes 參數，將目前的拓撲、組態設定及原則匯出為位元組陣列；此位元組陣列會儲存在名為 $x 的變數中。第二個命令使用 **Import-CsConfiguration** Cmdlet 和 ByteInput 參數來匯入儲存在 $x 的資訊。LocalStore 參數會導致資料匯入本機電腦，而非中央管理存放區。最終效果是資料從中央管理存放區複製到本機電腦。

    $x = Export-CsConfiguration -AsBytes
    Import-CsConfiguration -ByteInput $x -LocalStore

## 詳細描述

執行 Lync Server 服務或伺服器角色的電腦必須擁有目前拓撲的複本、目前的組態設定及目前的原則等等，才能夠以其指定的角色運作。Lync Server 負責確保此資訊會傳送到每部需要它的電腦。

Import-CsConfiguration Cmdlet 和 Export-CsConfiguration Cmdlet 可用於在中央管理存放區升級期間備份與還原您的 Lync Server 拓撲、組態設定與原則。**Export-CsConfiguration** Cmdlet 可讓您將資料匯出至 .ZIP 檔案；然後可以使用 **Import-CsConfiguration** Cmdlet 讀取該 .ZIP 檔案，並將拓撲、設定及原則還原至中央管理存放區。接下來，Lync Server 的複寫服務會將還原的資訊複寫到執行服務的電腦。

初始設定位於周邊網路上的電腦時 (例如 Edge Server)，也會使用匯出與匯入組態資料的功能。設定位於周邊網路上的電腦時，必須先使用 CsConfiguration Cmdlet 執行手動複寫：您需要使用 **Export-CsConfiguration** Cmdlet 匯出組態資料，然後將 .ZIP 檔案複製到周邊網路中的電腦。接下來，您可以使用 **Import-CsConfiguration** Cmdlet 及 LocalStore 參數來匯入資料。您只需要執行此動作一次；之後就會自動進行複寫。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Import-CsConfiguration** Cmdlet：RTCUniversalServerAdmins。除了必須是 RTCUniversalServerAdmins 的成員以外，您還必須是本機系統管理員或具有本機組態複寫器權限，才能執行這個 Cmdlet。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Import-CsConfiguration"}

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
<td><p>從變數中儲存的位元組陣列讀取拓撲資訊。此位元組陣列是在呼叫 <strong>Export-CsConfiguration</strong> Cmdlet 時使用 ByteInput 參數所建立的。</p>
<p>您無法在同一個命令中同時使用 ByteInput 參數和 FileName 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>FileName</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>Export-CsConfiguration 所建立之 .ZIP 檔案的路徑。例如：-FileName &quot;C:\Config.zip&quot;。請注意，您必須在呼叫 <strong>Import-CsConfiguration</strong> Cmdlet 時加入 FileName 或 ByteInput 參數，但不可同時加入兩者。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>略過執行該命令時，可能出現的任何非嚴重錯誤提示。若要將 Force 參數設為 True，請使用下列語法：</p>
<p>-Force:$True</p></td>
</tr>
<tr class="even">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>將組態資料複製到本機電腦，而非複製到中央管理存放區。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Import-CsConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Import-CsConfiguration** Cmdlet 不會傳回任何值或物件。

## 請參閱

#### 其他資源

[Export-CsConfiguration](export-csconfiguration.md)

