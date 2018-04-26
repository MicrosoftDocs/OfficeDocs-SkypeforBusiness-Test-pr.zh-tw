---
title: Start-CsWindowsService
TOCTitle: Start-CsWindowsService
ms:assetid: 7491b91f-d342-4f9a-878b-d20b35294a9c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398561(v=OCS.15)
ms:contentKeyID: 49291319
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Start-CsWindowsService

 

_**上次修改主題的時間：** 2015-03-09_

**Start-CsWindowsService** Cmdlet 可讓您啟動 Lync Server 服務。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Start-CsWindowsService [-ComputerName <String>] [-Name <String>] <COMMON PARAMETERS>

    Start-CsWindowsService [-InputObject <NTService>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-NoWait <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會在本機電腦上啟動所有 Lync Server 服務。作法是呼叫不含任何參數的 **Start-CsWindowsService** Cmdlet。請注意，如果嘗試啟動已啟動的服務，您不會收到錯誤訊息。

    Start-CsWindowsService

## 範例 2

範例 2 會啟動本機電腦上的 回應群組應用程式服務。為達此目的，命令會使用 Name 參數加上服務名稱：RTCRGS。

    Start-CsWindowsService -Name "RTCRGS"

## 範例 3

範例 3 所示的命令也會啟動 回應群組應用程式 服務；但此範例中服務是在遠端電腦 atl-cs-001.litwareinc.com 上啟動。若要在遠端電腦上啟動服務，請加上 ComputerName 參數，後面加上遠端電腦的 FQDN。

    Start-CsWindowsService -Name "RTCRGS" -ComputerName atl-cs-001.litwareinc.com

## 範例 4

在範例 4 中，命令會搜尋本機電腦目前未執行的所有 Lync Server 服務，然後啟動每個非使用中服務。為達成此目的，命令會先呼叫 **Get-CsWindowsService** Cmdlet 傳回所有 Lync Server 服務的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 Status 屬性不等於 Running 的服務。接著將篩選後的集合管線傳送到 **Start-CsWindowsService** Cmdlet，以啟動集合中的每個服務。

    Get-CsWindowsService | Where-Object {$_.Status -ne "Running"} | Start-CsWindowsService

## 詳細描述

有許多 Lync Server 元件都是以標準 Windows 服務的形式來運作。例如， 會議服務員應用程式實際上是名稱為 RTCCAA 的服務。如果您的其中一個 Lync Server 服務目前已經停止，便可使用 **Start-CsWindowsService** Cmdlet 重新啟動該服務。

不過，請注意， **Start-CsWindowsService** Cmdlet 只能啟動 Lync Server 服務；如果您嘗試以這個 Cmdlet 來啟動非 Lync Server 服務 (例如，列印多工緩衝處理器)，則會發生錯誤。

**Start-CsWindowsService** Cmdlet 在功能上與一般的 Windows PowerShell**Start-Service** Cmdlet 很類似；如有必要，您也可以使用 **Start-Service** Cmdlet 來啟動 Lync Server 服務。另一方面，**Start-CsWindowsService** Cmdlet 包含 ComputerName 參數，讓啟動遠端電腦的服務更加方便；只要加入 ComputerName 參數，後面再加上遠端電腦的完整網域名稱 (FQDN) 即可。**Start-Service** Cmdlet 沒有相對的參數。此外，Cmdlet 的 Report 參數可讓您保留呼叫 **Start-CsWindowsService** 時可能發生的任何錯誤記錄。

就像其他 Windows 服務，某些 Lync Server 服務對其他服務具有相依性；舉例來說，除非已在執行 應用程式服務，否則無法執行 Lync Server 會議服務員服務。如果您嘗試啟動相依於另一個服務的服務， **Start-CsWindowsService** Cmdlet 會同時啟動這兩個服務。這表示，如果您嘗試啟動會議服務員服務，Cmdlet 會先啟動 應用程式服務，然後再啟動會議服務員服務。不過， **Start-CsWindowsService** Cmdlet 不會自動啟動服務的任何相依服務：如果您啟動 應用程式服務，命令也不會自動啟動會議服務員服務。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Start-CsWindows** Cmdlet：RTCUniversalServerAdmins。此外，您必須具有目的地電腦的本機系統管理員權限才能執行此 Cmdlet。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Start-CsWindowsService"}

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
<td><p>主控要啟動之服務的遠端電腦名稱；如果未包含此參數， <strong>Start-CsWindowsService</strong> Cmdlet 便會啟動本機電腦上指定的服務。您應該使用遠端電腦的 FQDN 加以參照；例如 atl-cs-001.litwareinc.com。</p></td>
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
<td><p><em>InputObject</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.Core.NTService</p></td>
<td><p>可讓您使用物件參考來啟動服務，而非使用服務名稱。例如，如果使用 <strong>Get-CsWindowsService</strong> Cmdlet 傳回服務的資訊，且將傳回的物件儲存在名為 $x 的變數中，則可以使用此命令啟動服務：</p>
<p>$x = Get-CsWindowsService -Name &quot;RTCCPS&quot;</p>
<p>Start-CsWindowsService -InputObject $x.Name</p></td>
</tr>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>您要啟動的 Lync Server 服務名稱。請注意，您必須使用服務名稱 (例如 RTCCAA)，而非服務顯示名稱。您只能將單一服務名稱傳遞到 Name 參數，且無法在服務名稱中使用萬用字元。服務名稱可以使用 <strong>Get-CsWindowsService</strong> Cmdlet 來擷取。</p>
<p>請注意， <strong>Start-CsWindowsService</strong> Cmdlet 只能啟動 Lync Server 服務，您無法使用此 Cmdlet 啟動其他 Windows 服務。對於那些服務，您可以使用 Windows PowerShell  <strong>Start-Service</strong> Cmdlet。</p></td>
</tr>
<tr class="even">
<td><p><em>NoWait</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>當存在時，會導致命令執行，並立即傳回控制到 Windows PowerShell 提示。如果不存在，則必須等到命令完成，且狀態報表已寫入畫面時，才會傳回控制。</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可儲存錯誤資訊的 HTML 檔案路徑。如果有加入此參數，執行此 Cmdlet 期間所發生的任何錯誤都會記錄到指定的檔案 (如 C:\Logs\Service_report.html) 中。</p></td>
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

Microsoft.Rtc.Management.Deployment.Core.NTService 物件。 **Start-CsWindowsService** Cmdlet 接受管線傳送的 Windows 服務物件執行個體。

## 傳回類型

無。**Start-CsWindowsService** Cmdlet 會啟動 Microsoft.Rtc.Management.Deployment.Core.NTService 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsWindowsService](get-cswindowsservice.md)  
[Stop-CsWindowsService](stop-cswindowsservice.md)

