---
title: Import-CsLegacyConfiguration
TOCTitle: Import-CsLegacyConfiguration
ms:assetid: bd688c08-abb8-4c78-8e1b-b330412d4422
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412923(v=OCS.15)
ms:contentKeyID: 49292147
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Import-CsLegacyConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

**Import-CsLegacyConfiguration** Cmdlet 可讓您將許多組態設定從 Microsoft Office Communications Server 2007 R2 或 Microsoft Office Communications Server 2007 匯入 Lync Server。這樣有助於提供 Lync Server 和先前安裝之 Office Communications Server 2007 R2 或 Office Communications Server 2007 間的互通性。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Import-CsLegacyConfiguration [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-ReplaceExisting <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將來自 Communications Server 2007 或 Communications Server 2007 R2 的語音原則和其他設定與 Lync Server 的安裝合併。

    Import-CsLegacyConfiguration

## 範例 2

範例 2 所示的命令是範例 1 顯示的命令變化。不過，在此案例中包含 ReplaceExisting 參數。此參數指示 Cmdlet 使用匯入的資料來解決名稱衝突。例如，假設您嘗試匯入名為 LocalRoute 的語音路由，而在您的 Lync Server 安裝中已有同名的語音路由。因為您已加上 ReplaceExisting 參數，因此 Lync Server 路徑將由匯入的語音路徑所取代。

    Import-CsLegacyConfiguration -ReplaceExisting

## 詳細描述

**Import-CsLegacyConfiguration** Cmdlet 會與 **Merge-CsLegacyTopology** Cmdlet 搭配使用，讓組織可以從舊版的 Office Communications Server (Office Communications Server 2007 R2 或 Office Communications Server 2007) 移轉至 Lync Server。**Import-CsLegacyConfiguration** Cmdlet 可用來匯入語音原則、位置設定檔 (例如，撥號對應表)、語音路由、語音正規化規則、會議原則、外部存取原則、封存原則、目前狀態原則、Communicator Web Access URL 設定，以及電話撥入式會議存取號碼。

您必須先安裝 Windows Management Instrumentation (WMI) 回溯相容性介面套件，才可以執行 **Import-CsLegacyConfiguration** Cmdlet；您可以執行 OCSWMIBC.msi 來安裝此應用程式。安裝相容性介面套件之後，應接著執行 **Merge-CsLegacyTopology** Cmdlet。當 **Merge-CsLegacyTopology** Cmdlet 完成時，您應使用拓撲產生器來發佈合併的拓撲。發佈合併的拓撲之後，接著可呼叫 **Import-CsLegacyConfiguration** Cmdlet。**Import-CsLegacyConfiguration** Cmdlet 會使用 WMI 來讀取舊版 Office Communications Server 的舊資料。然後，**Import-CsLegacyConfiguration** Cmdlet 會取得擷取的資料，並在 Lync Server 中建立對應的物件。例如，針對在 Office Communications Server 安裝中找到的每一個語音原則，都會在新的 Lync Server 安裝中建立對應的語音原則。

每當您對下列任何 Office Communications Server 項目進行變更時，即應重新執行 **Import-CsLegacyConfiguration** Cmdlet：語音原則、位置設定檔、語音路由、語音正規化規則、會議原則、外部存取原則、封存原則、目前狀態原則、Communicator Web Access URL 設定，以及電話撥入式會議存取號碼。根據預設，當您重新執行 **Import-CsLegacyConfiguration** Cmdlet 時，只會匯入已新增至 Office Communications Server 拓撲的新項目。若要匯入修改的物件，必須執行下列兩項作業：首先，確認並未對組態之 Lync Server 複本中的對應項目 (例如，語音原則) 進行任何變更。其次，執行 **Import-CsLegacyConfiguration** Cmdlet 搭配 ReplaceExisting 參數；這會讓 **Import-CsLegacyConfiguration** Cmdlet 匯入修改的物件，並覆寫目前位於 Lync Server 中的對應物件。請注意，已從 Communications Server 2007 R2 拓撲刪除的物件不會在 Lync Server 中產生對應的刪除結果。您需要手動在 Lync Server 中移除這些物件。

請務必瞭解 **Move-CsLegacyUser** Cmdlet 依賴 **Import-CsLegacyConfiguration** Cmdlet 匯入的資訊。這表示，執行 **Move-CsLegacyUser** Cmdlet 時，您可能會收到錯誤訊息，告知您必須先執行 **Import-CsLegacyConfiguration** Cmdlet 才能繼續作業。如果發生此狀況，您必須先重新執行 **Import-CsLegacyConfiguration** Cmdlet，才能移動舊的使用者。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Import-CsLegacyConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Import-CsLegacyConfiguration"}

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
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>ReplaceExisting</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定，此參數會指示 <strong>Import-CsLegacyConfiguration</strong> Cmdlet 覆寫任何自從該 Cmdlet 上次執行後已變更之先前匯入的原則或設定。</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\ImportConfiguration.html&quot;</p></td>
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

無。**Import-CsLegacyConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Import-CsLegacyConfiguration** Cmdlet 不會傳回任何物件或值。

## 請參閱

#### 其他資源

[Import-CsLegacyConferenceDirectory](import-cslegacyconferencedirectory.md)  
[Merge-CsLegacyTopology](merge-cslegacytopology.md)  
[Move-CsLegacyUser](move-cslegacyuser.md)

