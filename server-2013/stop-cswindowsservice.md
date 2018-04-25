---
title: Stop-CsWindowsService
TOCTitle: Stop-CsWindowsService
ms:assetid: 60318b9f-2291-4b99-a271-d206e4074b70
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398426(v=OCS.15)
ms:contentKeyID: 49291076
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Stop-CsWindowsService

 

_**上次修改主題的時間：** 2015-03-09_

**Stop-CsWindowsService** 可讓您停止 Lync Server 服務。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Stop-CsWindowsService [-ComputerName <String>] [-Name <String>] <COMMON PARAMETERS>

    Stop-CsWindowsService [-InputObject <NTService>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Graceful <SwitchParameter>] [-LeaveClsAgentRunning <SwitchParameter>] [-LeaveWebServerRunning <SwitchParameter>] [-NoWait <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會停止本機電腦上的 回應群組應用程式 服務。回應群組應用程式 服務是透過包含 Name 參數與以下服務的名稱來識別：RTCRGS。

    Stop-CsWindowsService -Name "RTCRGS"

## 範例 2

範例 2 也會停止 回應群組應用程式 服務；但在此範例中，該服務位在 atl-cs-001.litwareinc.com 遠端電腦上。若要停止遠端電腦上的服務，請包含 ComputerName 參數，後面加上遠端電腦的 FQDN。

    Stop-CsWindowsService -Name "RTCRGS" -ComputerName atl-cs-001.litwareinc.com

## 範例 3

範例 3 示範要如何停止服務，即使您不知道服務名稱 (在本範例為 RTCCPS)。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsWindowsService** Cmdlet，以傳回本機電腦上所有 Lync Server 服務的集合。然後再將此完整的集合管線傳送到 **Where-Object** Cmdlet，這會只選取 DisplayName 屬性包含 "Call Park" 字串值的服務。接著將篩選後的集合管線傳送到 **Stop-CsWindowsService** Cmdlet，以停止通話駐留應用程式服務。

    Get-CsWindowsService | Where-Object {$_.DisplayName -like "*Call Park*"} | Stop-CsWindowsService

## 詳細描述

有許多 Lync Server 元件都是以標準 Windows 服務的形式運作。例如，會議服務員應用程式實際上是名稱為 RTCCAA 的服務。如果您需要停止 Lync Server 服務，可以使用 **Stop-CsWindowsService** Cmdlet 加以停止。

請記住，**Stop-CsWindowsService** Cmdlet 只能停止 Lync Server 服務，如果您嘗試使用此 Cmdlet 停止非 Lync Server 的服務 (例如列印多工緩衝處理器)，便會發生錯誤。

**Stop-CsWindowsService** Cmdlet 在功能上和一般 Windows PowerShell**Stop-Service** Cmdlet 相當類似。如果您想要的話，可以使用 **Stop-Service** Cmdlet 來停止 Lync Server 服務。但是 **Stop-CsWindowsService** Cmdlet 中包含了 ComputerName 參數，使得停止遠端電腦上的服務變得很容易：您只要包含 ComputerName 參數，後面再加上遠端電腦的完整網域名稱 (FQDN) 即可。**Stop-Service** Cmdlet 並沒有相對的參數。此外，**Stop-CsWindowsService** Cmdlet 的 Report 參數可讓您保留呼叫該 Cmdlet 時可能發生之任何錯誤的記錄。

**Stop-CsWindowsService** Cmdlet 的功能就和它的名稱所代表的意思一樣：它會停止任何您要求停止的服務。包括具有相依服務 (僅在您嘗試停止的服務正在執行時才能執行的服務) 的服務。根據預設，如果您嘗試停止的服務有相依服務，則 **Stop-CsWindowsService** Cmdlet 不只會停止所要求的服務，也會停止所有相依服務。因為這可能會導致無法預期的後果，所以您在呼叫 **Stop-CsWindowsService** Cmdlet 時可以包含 Graceful 參數。當您包含 Graceful 參數時，**Stop-CsWindowsService** Cmdlet 會阻止服務接受任何新的要求。所有現有的服務要求會保留，不過新的要求將遭到拒絕。當現有的要求完成時，並不會取代這些要求。最終，等到滿足所有現有的要求後，服務便會關閉。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Stop-CsWindowsService** Cmdlet：RTCUniversalServerAdmins。此外，您必須具有目的地電腦的本機系統管理員權限才能執行此 Cmdlet。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Stop-CsWindowsService"}

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
<td><p><em>ComputerName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>執行要停止之服務的遠端電腦名稱；如果未包含此參數，則 <strong>Stop-CsWindowsService</strong> Cmdlet 會停止本機電腦上的指定服務。您應該使用遠端電腦的 FQDN 來加以指定；例如 atl-mcs-001.litwareinc.com。</p></td>
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
<td><p><em>Graceful</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>等候所有現有的服務要求實現，而非立即關閉服務 (不過所有新的服務要求都將遭到拒絕)。所有現有的要求必須完成，該服務才會完全關閉。</p></td>
</tr>
<tr class="odd">
<td><p><em>InputObject</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.Core.NTService</p></td>
<td><p>可讓您使用物件參考來停止服務，而非使用服務名稱。例如，如果使用 <strong>Get-CsWindowsService</strong> Cmdlet 傳回服務的資訊，且將傳回的物件儲存在名為 $x 的變數中，則可以使用此命令停止服務：</p>
<p>$x = Get-CsWindowsService –Name &quot;RTCCPS&quot;</p>
<p>Stop-CsWindowsService -InputObject $x.Name</p></td>
</tr>
<tr class="even">
<td><p><em>LeaveClsAgentRunning</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>指定此項目時，會停止所有 Lync Server 服務 (除了集中式記錄代理程式服務之外)。</p></td>
</tr>
<tr class="odd">
<td><p><em>LeaveWebServerRunning</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有指定此參數，除了指定電腦上的 Web 伺服器服務之外，會關閉所有服務。</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>要停止之 Lync Server 服務的名稱。請注意，您必須使用服務名稱 (例如 RTCCAA)，而非服務顯示名稱。您只能將單一服務名稱傳遞到 Name 參數，且無法在服務名稱中使用萬用字元。您可以使用 <strong>Get-CsWindowsService</strong> Cmdlet 來擷取服務名稱。</p>
<p>請注意，<strong>Stop-CsWindowsService</strong> Cmdlet 只能停止 Lync Server 服務，您無法使用此 Cmdlet 停止其他 Windows 服務。對於那些服務，您可以使用 Windows PowerShell  <strong>Stop-Service</strong> Cmdlet。</p></td>
</tr>
<tr class="odd">
<td><p><em>NoWait</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>當存在時，會導致命令執行，並立即傳回控制到 Windows PowerShell 提示。如果不存在，則必須等到命令完成，且狀態報表已寫入畫面時，才會傳回控制。</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可寫入錯誤資訊的 HTML 檔案路徑。如有加入此參數，執行此 Cmdlet 期間所發生的任何錯誤都會記錄到指定的檔案 (如 C:\Logs\Service_report.html) 中。</p></td>
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

Microsoft.Rtc.Management.Deployment.Core.NTService 物件。**Stop-CsWindowsService** Cmdlet 接受管線傳送的 Windows 服務物件執行個體。

## 傳回類型

無。反之，**Stop-CsWindowsService** Cmdlet 會停止 Microsoft.Rtc.Management.Deployment.Core.NTService 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsWindowsService](get-cswindowsservice.md)  
[Start-CsWindowsService](start-cswindowsservice.md)

