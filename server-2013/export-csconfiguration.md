---
title: Export-CsConfiguration
TOCTitle: Export-CsConfiguration
ms:assetid: 7da7e133-e405-466c-a852-06a4fb678c59
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398627(v=OCS.15)
ms:contentKeyID: 49291442
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Export-CsConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

將您的 Lync Server 拓撲、原則及組態設定匯出至檔案。此檔案可在升級、硬體故障或其他問題造成資料遺失時，用於將此資訊還原到中央管理存放區。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Export-CsConfiguration [-AsBytes <SwitchParameter>] <COMMON PARAMETERS>

    Export-CsConfiguration -FileName <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會將 Lync Server 資料從中央管理存放區匯出至名為 C:\\Config.zip 的檔案。

    Export-CsConfiguration -FileName "C:\Config.zip"

## 詳細描述

執行 Lync Server 服務或伺服器角色的電腦必須擁有目前拓撲的複本、目前的組態設定及目前的原則，才能夠以其指定的角色運作。Lync Server 負責確保此資訊會傳送到每部需要它的電腦。

在中央管理存放區升級期間，您可使用 **Export-CsConfiguration** Cmdlet 和 **Import-CsConfiguration** Cmdlet 備份與還原您的 Lync Server 拓撲、組態設定與原則。**Export-CsConfiguration** Cmdlet 可讓您將資料匯出至 .ZIP 檔案；然後可以使用 **Import-CsConfiguration** Cmdlet 讀取該 .ZIP 檔案，並將拓撲、組態設定及原則還原至中央管理存放區。接下來，Lync Server 的複寫服務會將還原的資訊複寫到其他執行 Lync Server 服務的電腦。

初始設定位於周邊網路上的電腦時 (例如 Edge Server)，也可以使用匯出與匯入組態資料的功能。設定周邊網路上的電腦時，必須先使用 CsConfiguration Cmdlet 執行手動複寫：您需要使用 **Export-CsConfiguration** Cmdlet 匯出組態資料，然後將 .ZIP 檔案複製到周邊網路中的電腦。接下來，您可以使用 **Import-CsConfiguration** Cmdlet 及 LocalStore 參數來匯入資料。您只需要執行此動作一次；之後就會自動進行複寫。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Export-CsConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Export-CsConfiguration"}

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
<td><p>執行 <strong>Export-CsConfiguration</strong> Cmdlet 時要建立之 .ZIP 檔案的路徑。例如：-FileName &quot;C:\Config.zip&quot;。請注意，您必須在呼叫 <strong>Export-CsConfiguration</strong> Cmdlet 時加入 FileName 或 AsBytes 參數，但不可同時加入。</p></td>
</tr>
<tr class="even">
<td><p><em>AsBytes</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>以位元組陣列的方式傳回拓撲資訊；然後，傳回的資料必須以變數儲存，以便供 <strong>Import-CsConfiguration</strong> Cmdlet 使用。在同一個命令中無法同時使用 AsBytes 和 FileName。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏顯示當執行命令時可能發生的任何非嚴重錯誤訊息。若要將 Force 參數設為 True，請使用下列語法：</p>
<p>-Force:$True</p></td>
</tr>
<tr class="even">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從本機電腦擷取組態資料，而非從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Export-CsConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

如果搭配 AsBytes 參數呼叫 **Export-CsConfiguration** Cmdlet，則會以位元組陣列的格式傳回組態資訊。

## 請參閱

#### 其他資源

[Import-CsConfiguration](import-csconfiguration.md)

