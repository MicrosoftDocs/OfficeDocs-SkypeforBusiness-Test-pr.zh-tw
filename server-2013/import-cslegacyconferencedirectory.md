---
title: Import-CsLegacyConferenceDirectory
TOCTitle: Import-CsLegacyConferenceDirectory
ms:assetid: 5ecb9bf9-cbce-48a6-966c-ecbdac59cb3a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398418(v=OCS.15)
ms:contentKeyID: 49291060
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Import-CsLegacyConferenceDirectory

 

_**上次修改主題的時間：** 2015-03-09_

**Import-CsLegacyConferenceDirectory** Cmdlet 可讓您將會議目錄從 Microsoft Office Communications Server 2007 R2 匯入 Lync Server，這有助於 Lync Server 與 Office Communications Server 2007 R2 彼此能夠互通。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Import-CsLegacyConferenceDirectory [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將會議目錄從 Communications Server 2007 R2 匯入至 Lync Server。

    Import-CsLegacyConferenceDirectory

## 詳細描述

**Import-CsLegacyConferenceDirectory** Cmdlet 與 **Merge-CsLegacyTopology** Cmdlet 搭配使用，可讓組織從 Office Communications Server 2007 R2 移轉至 Lync Server。 **Import-CsLegacyConfiguration** Cmdlet 會將會議目錄從 Communications Server 2007 R2 匯入 Lync Server。

在可以執行 **Import-CsLegacyConferenceDirectory** Cmdlet 之前，必須先安裝 Windows Management Instrumentation (WMI) 回溯相容性介面套件；此應用程式是藉由執行 OCSWMIBC.msi 來進行安裝 (在 Lync Server 安裝 DVD 中的 Setup 資料夾內可以找到 OCSWMIBC.msi)。安裝回溯相容性介面套件後，接著應該執行 **Merge-CsLegacyTopology** Cmdlet。

**Merge-CsLegacyTopology** Cmdlet 完成執行後，您可以呼叫 **Import-CsLegacyConferenceDirectory** Cmdlet。 **Import-CsLegacyConferenceDirectory** Cmdlet 會先使用 WMI 從 Communications Server 2007 R2 讀取舊版資料，然後以擷取的資料在 Lync Server 中建立對應的物件：對於在您安裝之 Communications Server 2007 R2 中找到的每個會議目錄，都會在您新安裝之 Lync Server 中建立一個對應的目錄。

每次在 Communications Server 2007 R2 環境中新增、刪除或移動會議目錄時，都應該重新執行 **Import-CsLegacyConferenceDirectory** Cmdlet。每次執行 **Merge-CsLegacyTopology** Cmdlet 時，也應執行 **Import-CsLegacyConferenceDirectory** Cmdlet；這樣才能確保會議目錄與拓撲保持同步。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Import-CsLegacyConferenceDirectory** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Import-CsLegacyConferenceDirectory"}

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
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\ImportDirectories.html&quot;</p></td>
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

無。 **Import-CsLegacyConferenceDirectory** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Import-CsLegacyConferenceDirectory** Cmdlet 不會傳回任何物件或值。

## 請參閱

#### 其他資源

[Import-CsLegacyConfiguration](import-cslegacyconfiguration.md)  
[Merge-CsLegacyTopology](merge-cslegacytopology.md)  
[Move-CsLegacyUser](move-cslegacyuser.md)

