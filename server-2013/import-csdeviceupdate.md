---
title: Import-CsDeviceUpdate
TOCTitle: Import-CsDeviceUpdate
ms:assetid: cc2e5fab-d978-4e7e-8fc6-d12a0172c07c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398861(v=OCS.15)
ms:contentKeyID: 49292339
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Import-CsDeviceUpdate

 

_**上次修改主題的時間：** 2015-03-09_

匯入下載自 Microsoft 網站的裝置更新規則集合。裝置更新規則可用於關聯韌體版本更新與執行 Lync Phone Edition 的硬體裝置。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Import-CsDeviceUpdate -FileName <String> -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令可從 C:\\Updates\\UCUpdates.cab 檔案匯入裝置更新規則。

    Import-CsDeviceUpdate -Identity "service:WebServer:atl-cs-001.litwareinc.com" -FileName C:\Updates\UCUpdates.cab

## 範例 2

範例 2 所示的命令可從 UNC 路徑 \\\\atl-fs-001\\Updates\\UCUpdates.cab 匯入裝置更新規則。

    Import-CsDeviceUpdate -Identity "service:WebServer:atl-cs-001.litwareinc.com" -FileName \\atl-fs-001\Updates\UCUpdates.cab

## 範例 3

範例 3 示範如何使用單一命令，將裝置更新規則匯入所有執行 Web 服務的伺服器中。為達成此目的，命令會先呼叫 **Get-CsService** Cmdlet 搭配 WebServer 參數，以傳回所有執行 Web 服務服務之伺服器的集合。然後，此集合會管線傳送到 **ForEach-Object** Cmdlet，以循序處理集合中的每一部伺服器，並使用 **Import-CsDeviceUpdate** Cmdlet，將這些伺服器的裝置更新規則更新為最新版本。請注意，必須先將 UCUpdates.cab 複製到所有伺服器的同一個位置 (C:\\Updates)，此命令才可發揮作用。

    Get-CsService -WebServer | ForEach-Object {Import-CsDeviceUpdate -Identity $_.Identity -FileName C:\Updates\UCUpdates.cab}

## 詳細描述

Microsoft 會定期發行新的 Lync Phone Edition 裝置更新規則組合。這些規則代表執行 Lync Phone Edition 之裝置的韌體更新。在匯入這些規則後，系統管理員能測試韌體更新，測試成功的話，可以將更新提供給所有在組織中使用的相關裝置。

建立新更新規則唯一的方法是從 Microsoft 下載更新套件，您不能自行建立專屬的裝置更新規則。若要取得最新的裝置更新規則組合，請前往 Microsoft 網站的 \[說明及支援\] 頁面並搜尋 "Phone Edition"。下載更新套件後，將檔案解壓縮至要上載之更新所在的電腦資料夾內。解壓縮檔案後，接著可以使用 **Import-CsDeviceUpdate** Cmdlet 匯入解壓縮後之 .CAB 檔案 (其名稱為 UCUpdates.cab) 中的裝置更新規則。

如上所述，只能本機載入更新；您需要將 UCUpdates.cab 複製到執行 Web 服務服務且需要裝載裝置更新規則的電腦上。另請記住，裝置更新規則不會在伺服器之間進行複寫。如果您想讓整個組織的所有裝置更新規則都維持同步，則需要在每部主控這些規則的伺服器上執行相同作業。例如，如果您從某部 Web 服務伺服器移除規則，則需要從其他的 Web 服務伺服器移除這個相同的規則。否則，裝置更新規則將無法同步。

您只能將更新規則匯入服務，這些規則並不適合在全域、網站或個別使用者範圍內使用。但請注意，**Import-CsDeviceUpdate** Cmdlet 不會將規則和更新自動新增至網站中的每一個服務；而是只會將這些規則和更新載入特定的服務。例如，若您在執行 Web 服務的網站中有三部伺服器，將需要執行三次 **Import-CsDeviceUpdate** Cmdlet，針對每一個 Web 服務執行個體各執行一次。或者，您可以使用如範例 3 所示的命令：這一個命令會擷取所有伺服器 Web 服務的 Identity，然後在這每一部伺服器上執行 **Import-CsDeviceUpdate** Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Import-CsDeviceUpdate** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Import-CsDeviceUpdate"}

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
<td><p>更新檔案的路徑 (如 C:\Updates\UCUpdates.cab)。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>表示要套用新更新規則的服務執行個體。例如：-Identity &quot;service:WebServer:atl-cs-001.litwareinc.com&quot;。</p>
<p>Identity 應該是安裝 Web 伺服器之 Front End 集區的完整網域名稱。</p></td>
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
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Import-CsDeviceUpdate** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Import-CsDeviceUpdate** Cmdlet 會匯入 Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.Rule 類別的執行個體。

## 請參閱

#### 其他資源

[Get-CsDeviceUpdateRule](get-csdeviceupdaterule.md)

