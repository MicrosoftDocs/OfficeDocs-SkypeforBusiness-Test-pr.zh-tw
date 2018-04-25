---
title: Get-CsWindowsService
TOCTitle: Get-CsWindowsService
ms:assetid: 9b119dac-c3e6-4031-8ae4-972fca1ef728
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398803(v=OCS.15)
ms:contentKeyID: 49291779
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsWindowsService

 

_**上次修改主題的時間：** 2015-03-09_

**Get-CsWindowsService** 會傳回以 Windows 服務形式執行之 Lync Server 元件的詳細資訊。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsWindowsService [-ComputerName <String>] [-ExcludeActivityLevel <SwitchParameter>] [-Name <String>] [-Report <String>]

## 範例

## 範例 1

範例 1 所示的命令會傳回本機電腦上安裝之所有 Lync Server 服務的資訊。作法是呼叫不含任何參數的 **Get-CsWindowsService** Cmdlet。

    Get-CsWindowsService

## 範例 2

範例 2 也會傳回本機電腦上關於 Lync Server 服務的資訊；但在此範例中，資料會以清單格式顯示 (這可讓您檢視每個服務的所有屬性值。在預設的表格式檢視中，只會顯示屬性值的子集)。為了執行此工作，會先呼叫 **Get-CsWindowsService** Cmdlet，然後會將產生的資訊管線傳送到 **Format-List** Cmdlet。

    Get-CsWindowsService | Format-List

## 範例 3

範例 3 會傳回單一 Lync Server 服務的資訊：名稱為 RTCSrv 的服務。

    Get-CsWindowsService -Name "RTCSrv"

## 範例 4

範例 4 會顯示 RTCSrv 服務所處理之所有服務角色的詳細資訊。為了執行此工作，會先使用 **Get-CsWindowsService** Cmdlet 傳回關於 RTCSrv 服務的資訊。然後再將該資訊管線傳送至 **Select-Object** Cmdlet，以使用 ExpandProperty 參數顯示 RTCSrv 服務所處理的所有角色。請注意，如果服務沒有角色名稱，此命令將會傳回錯誤訊息。

    Get-CsWindowsService -Name "RTCSrv" | Select-Object -ExpandProperty RoleName

## 範例 5

範例 5 所示的命令會傳回遠端電腦 atl-cs-001.litwareinc.com 上已安裝 Lync Server 服務的資訊。您可以加入 ComputerName 參數加上遠端電腦的 FQDN。

    Get-CsWindowsService -Computer atl-cs-001.litwareinc.com

## 範例 6

範例 6 會傳回安裝於本機電腦上所有 Lync Server 服務的資訊。此外，加入 Report 參數的目的，是為了將錯誤資訊儲存到名為 C:\\Logs\\Services.html 的檔案。如果 **Get-CsWindowsService** Cmdlet 在擷取服務資料時碰到任何問題，將會在 Services.html 中記錄該問題的資訊。

    Get-CsWindowsService -Report C:\Logs\Services.html

## 範例 7

範例 7 會僅針對本機電腦上目前正在執行的 Lync Server 服務傳回相關資訊。為達成此目的，命令會先呼叫 **Get-CsWindowsService** Cmdlet，以傳回所有 Lync Server 服務 (無論是否正在執行) 的集合。然後，此集合會以管線傳送到 **Where-Object** Cmdlet，這會只挑出 Status 屬性等於 Running 的服務。

    Get-CsWindowsService | Where-Object {$_.Status -eq "Running"}

## 範例 8

範例 8 示範如何在您不知道服務的實際名稱時，擷取特定服務的資訊 (在此範例中為 RTCASMCU)。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsWindowsService** Cmdlet，以傳回本機電腦上所有 Lync Server 服務的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，以選取 DisplayName 屬性包含 (-like) 字串值 "Application Sharing" 的服務。最後的結果會顯示 Lync Server  應用程式共用會議服務的資訊。

    Get-CsWindowsService | Where-Object {$_.DisplayName -like "*Application Sharing*"}

## 範例 9

範例 9 會傳回主控應用程式伺服器角色之任何服務的資訊。為達成此目的，命令會先呼叫 **Get-CsWindowsService** Cmdlet，以傳回本機電腦上所有 Lync Server 服務的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，以選取 RoleName 屬性包含 (-contains) ApplicationServer 的服務。

    Get-CsWindowsService | Where-Object {$_.RoleName -contains "ApplicationServer"}

## 詳細描述

許多 Lync Server 元件都會當做標準 Windows 服務執行；例如， Lync Server  會議服務員應用程式實際上是名稱為 RTCCAA 的服務。 **Get-CsWindowsService** Cmdlet 可讓您擷取關於這些 Lync Server 服務 (而且僅關於這些服務) 的詳細資訊。這是因為此 Cmdlet 是針對忽略不屬於 Lync Server 的所有服務而設計。

**Get-CsWindowsService** Cmdlet 會自動篩除非 Lync Server 服務，這是此 Cmdlet 優於 Windows PowerShell 隨附之一般 **Get-Service** Cmdlet 的優點之一。除此之外，如果您需要擷取 Lync Server 服務的資訊，這是另一個使用 **Get-CsWindowsService** Cmdlet 的理由： **Get-CsWindowsService** Cmdlet 會傳回 **Get-Service** Cmdlet 不會傳回的有用資料。例如，傳回關於 Lync Server 會議服務員服務的資訊時， **Get-CsWindowsService** Cmdlet 會回報此服務正在處理的同時通話數 (服務活動層級) 。 **Get-Service** Cmdlet 則不會。

根據預設， **Get-CsWindowsService** Cmdlet 會針對本機電腦執行。不過，您可以透過加入 -ComputerName 參數，以傳回在遠端電腦上執行之 Lync Server 服務的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsWindowsService** Cmdlet：RTCUniversalServerAdmins。此外，您也必須是目的地電腦上 Performance Monitor Users 群組的成員，才能執行這個 Cmdlet。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsWindowsService"}

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
<td><p>要擷取其服務資訊之遠端電腦的名稱；若未加入此參數，則 <strong>Get-CsWindowsService</strong> Cmdlet 將會傳回關於本機電腦上執行之 Lync Server 服務的資訊。您應該使用遠端電腦的完整網域名稱 (FQDN) 來參考它，例如 atl-mcs-001.litwareinc.com。</p></td>
</tr>
<tr class="even">
<td><p><em>ExcludeActivityLevel</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如果加入此參數，此參數會使 <strong>Get-CsWindowsService</strong> Cmdlet 僅傳回服務狀態，而不傳回服務活動層級。</p></td>
</tr>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>您想傳回其資訊的服務名稱。請注意，您必須使用服務名稱 (例如 RTCCAA)，而非服務顯示名稱。您僅能將單一服務名稱傳遞給 Name 參數；此外，您無法在服務名稱中使用萬用字元。</p>
<p>也請注意， <strong>Get-CsWindowsService</strong> Cmdlet 僅能傳回 Lync Server 服務的資訊；您無法使用這個 Cmdlet 傳回其他 Windows 服務的資訊。針對那些服務，您或許可以使用 Windows PowerShell  <strong>Get-Service</strong> Cmdlet。</p>
<p>若未加入此參數， <strong>Get-CsWindowsService</strong> Cmdlet 將會傳回所有 Lync Server 服務的資訊。</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可儲存錯誤資訊的 HTML 檔案路徑。如果有加入此參數，執行此 Cmdlet 期間所發生的任何錯誤都會記錄到指定的檔案 (如 C:\Logs\Service_report.html) 中。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Get-CsWindowsService** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsWindowsService** Cmdlet 會傳回 Microsoft.Rtc.Management.Deployment.Core.NTService 物件的執行個體。

## 請參閱

#### 其他資源

[Start-CsWindowsService](start-cswindowsservice.md)  
[Stop-CsWindowsService](stop-cswindowsservice.md)

