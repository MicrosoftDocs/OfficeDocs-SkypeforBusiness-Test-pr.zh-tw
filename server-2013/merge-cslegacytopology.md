---
title: Merge-CsLegacyTopology
TOCTitle: Merge-CsLegacyTopology
ms:assetid: 396d6c84-7b38-41ae-9273-665f76cdd9ea
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425870(v=OCS.15)
ms:contentKeyID: 49290625
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Merge-CsLegacyTopology

 

_**上次修改主題的時間：** 2015-03-09_

**Merge-CsLegacyTopology** Cmdlet 可讓您將拓撲資訊從 Microsoft Office Communications Server 2007 R2 或 Microsoft Office Communications Server 2007 移轉至 Lync Server。此可讓 Lync Server 與舊版軟體能夠互通。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Merge-CsLegacyTopology -TopologyXmlFileName <String> <COMMON PARAMETERS>

    Merge-CsLegacyTopology -Reserved <PSObject> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Report <String>] [-UserInputFileName <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會將拓樸資訊與來自 Communications Server 2007 R2 或 Communications Server 2007 之信任的服務項目合併，並另外安裝 Lync Server。必要參數 TopologyXmlFileName 用於指出您在執行 **Merge-CsLegacyTopology** Cmdlet 時產生的輸出檔路徑。

    Merge-CsLegacyTopology -TopologyXmlFileName C:\New_Topology.xml

## 範例 2

範例 2 是範例 1 中使用的命令變化。但是，在範例 2 中包含了 UserInputFileName 參數，藉此將 Edge Server 資訊合併至拓樸中。參數值 C:\\EdgeServers.xml 會指向自訂的 XML 檔案，該 XML 檔案包含 Office Communications Server 的 Edge Server 資訊。

    Merge-CsLegacyTopology -TopologyXmlFileName C:\New_Topology.xml -UserInputFileName C:\EdgeServers.xml

## 詳細描述

從舊版的 Office Communications Server ( Office Communications Server 2007 R2 或 Office Communications Server 2007) 移轉至 Lync Server 時， **Merge-CsLegacyTopology** Cmdlet 是首先要使用的工具。 **Merge-CsLegacyTopology** Cmdlet 用於移轉下列元件之信任的服務項目與拓樸資訊：網域、User Services、登錄器、 中繼伺服器 及 Edge Server。此外，Cmdlet 會移轉 會議服務員應用程式、Communicator Web Access 與會議目錄之信任的服務項目 (信任的服務項目是指代表受 Lync Server 信任之伺服器的 Active Directory 項目)。合併拓樸資訊能讓 Lync Server 所屬之使用者與 Communications Server 2007 或 Communications Server 2007 R2 所屬之使用者通訊。

您必須先安裝 Windows Management Instrumentation (WMI) 回溯相容性介面套件，才能執行 **Merge-CsLegacyTopology** Cmdlet；執行 OCSWMIBC.msi 就能安裝這套應用程式 (OCSWMIBC.msi 位於安裝 DVD 的安裝程式中)。安裝相容性介面套件後，接著就能呼叫 **Merge-CsLegacyTopology** Cmdlet。 **Merge-CsLegacyTopology** Cmdlet 會使用 WMI 讀取舊版 Office Communications Server 的舊有資料，接著會取得已擷取的資料並在 Lync Server 中建立對應的物件。例如，系統會針對您 Office Communications Server 安裝中的每個 SIP 網域，在 Lync Server 的新安裝中建立對應的 SIP 網域。

在執行 **Merge-CsLegacyTopology** Cmdlet 後，您接下來應執行 **Import-CsLegacyConfiguration** Cmdlet 與 **Import-CsLegacyConferenceDirectory** Cmdlet。

**Merge-CsLegacyTopology** Cmdlet 必須至少執行兩次：一次是在移轉開始時 (為了引介 Communications Server 2007 或 Communications Server 2007 R2 拓撲)，另一次則是移轉結束、當之前的 Office Communications Server 環境被淘汰時。每次您想變更舊版 Office Communications Server 環境時，也必須執行該 Cmdlet。例如，如果您將 中繼伺服器 新增至 Office Communications Server 拓樸，或淘汰該拓樸中的某個集區，則必須重新執行 **Merge-CsLegacyTopology** Cmdlet，才能匯入已修改的拓樸。

**Import-CsLegacyConfiguration** Cmdlet 與 **Import-CsLegacyConferenceDirectory** Cmdlet 會視 **Merge-CsLegacyTopology** Cmdlet 設定的值而定。這代表您可能收到來自 **Import-CsLegacyConfiguration** Cmdlet 或 **Import-CsLegacyConferenceDirectory** Cmdlet 的錯誤訊息，要您執行 **Merge-CsLegacyTopology** Cmdlet 做為可能的解決方案，解決剛剛發生的問題。如果您不重新執行 **Merge-CsLegacyTopology** Cmdlet，就會發生其他錯誤，尤其是當 Lync Server 仍在使用某個項目時，若要從 Office Communications Server 環境中移除該項目，更可能會發生其他問題。

如果您需要從之前安裝的 Office Communications Server 合併 Edge Server，則必須先建立包含 Edge Server 的自訂 XML 檔案；您必須自行建立該檔案，因為 Edge Server 設定並非儲存在 Active Directory 中，因此， **Merge-CsLegacyTopology** Cmdlet 無法擷取相關設定。在您建立此 XML 檔案後 (請參閱《 Lync Server 部署指南》了解如何建立此檔案的資訊)，執行 **Merge-CsLegacyTopology** Cmdlet 時，您必須包含該檔案的路徑及 UserInputFileName 參數。如果沒有這麼做，合併的拓樸中不會包含 Edge Server。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Merge-CsLegacyTopology** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Merge-CsLegacyTopology"}

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
<td><p><em>Reserved</em></p></td>
<td><p>必要</p></td>
<td><p>PS topology object</p></td>
<td><p>可讓您使用拓撲物件而非 XML 拓撲檔案來合併拓撲。</p></td>
</tr>
<tr class="even">
<td><p><em>TopologyXmlFileName</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>當 <strong>Merge-CsLegacyTopology</strong> Cmdlet 執行時所建立之輸出檔的路徑。請注意，此檔案與使用 Report 參數指定的檔案不同，後者用於記錄錯誤資訊，而 Topology XML 檔案則會包含您新建立的 Lync Server 拓樸。這個檔案稍後會欲於新的拓樸。</p>
<p>如果指定的檔案已存在，則當您執行 <strong>Merge-CsLegacyTopology</strong> Cmdlet 時，會覆寫該檔案。</p></td>
</tr>
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
<td><p>可讓您指定在 Cmdlet 執行時所建立記錄檔的檔案路徑。例如：-Report &quot;C:\Logs\MergeTopology.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>UserInputFileName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>XML 檔案的路徑，用於從舊版 Office Communications Server 匯入 Edge Server 資料。這個 XML 檔案 (您必須依照《 Lync Server 部署指南》詳述的指導方針建立此 XML 檔案) 是必要檔案，因為 Edge Server 設定未儲存在 Active Directory 網域服務 中。如果您不必匯入 Edge Server 資訊，則可略過此參數。</p>
<p>若未使用此參數，遠端及外部存取功能 (包括同盟) 可能無法如預期般在同時執行 Communications Server 2007 R2 或 Communications Server 2007 R2 及 Lync Server 的環境中運作。</p></td>
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

無。 **Merge-CsLegacyTopology** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Merge-CsLegacyTopology** Cmdlet 不會傳回任何物件或值。

## 請參閱

#### 其他資源

[Import-CsLegacyConfiguration](import-cslegacyconfiguration.md)  
[Import-CsLegacyConferenceDirectory](import-cslegacyconferencedirectory.md)  
[Move-CsLegacyUser](move-cslegacyuser.md)

