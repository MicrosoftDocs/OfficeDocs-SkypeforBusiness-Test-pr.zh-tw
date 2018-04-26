---
title: Set-CsClsScenario
TOCTitle: Set-CsClsScenario
ms:assetid: 00de6571-a1ad-4f69-a21e-8a9ae115882f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204622(v=OCS.15)
ms:contentKeyID: 49289893
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsClsScenario

 

_**上次修改主題的時間：** 2015-03-09_

可讓您修改集中式記錄組態案例。案例代表系統管理員可啟用或停用追蹤的特定 Lync Server 2013 元件或狀況 (例如 IM 和目前狀態)。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Set-CsClsScenario [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsClsScenario [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Provider <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會建立新的集中式記錄案例提供者，然後將該提供者新增至為 Redmond 網站設定的 WAC 案例。為達成此目的，範例中的第一個命令會使用 **New-CsClsProvider** Cmdlet，建立名為 WebInfrastructure 的新提供者；這個新提供者會以名稱為 $provider 的變數儲存。接著，範例中的第二個命令會將這個新提供者新增至案例 site:Redmond/WAC。因為命令使用的語法是 @{Add=$provider}，所以除了已經針對該設定的其他提供者之外，也會將新的提供者新增到 WAC 案例。

    $provider = New-CsClsProvider -Name "WebInfrastructure" -Type "WPP" -Level "Warning" -Flags "All"
    
    Set-CsClsScenario -Identity "site:Redmond/WAC" -Provider @{Add=$provider}

## 範例 2

範例 2 所示的命令是範例 1 顯示的命令變化。不過，在範例2 中，新提供者將取代針對 WAC 案例設定的任何 (及所有) 現有提供者。若要這樣做，請使用 @{Replace=$provider} 的語法。

    $provider = New-CsClsProvider -Name "WebInfrastructure" -Type "WPP" -Level "Warning" -Flags "All"
    
    Set-CsClsScenario -Identity "site:Redmond/WAC" -Provider @{Replace=$provider}

## 詳細描述

集中式記錄服務 (取代 Microsoft Lync Server 2010 中使用的 OCSLogger 與 OCSTracer 工具) 提供一種方法，讓管理員管理所有執行 Lync Server 2013 之電腦與集區的記錄和追蹤。集中式記錄可讓管理員利用單一命令，來停止、啟動及設定一或多個集區與電腦的記錄；例如，您可以使用一個命令，在所有 Address Book Server 上啟用通訊錄服務記錄功能。這和必須在每部伺服器上個別管理 (包括個別停止和啟動) 的 OCSLogger 與 OCSTracer 工具不同。此外，集中式記錄服務也提供一種方法，讓管理員使用 Windows PowerShell 命令列介面與 [Search-CsClsLogging](search-csclslogging.md) Cmdlet，從命令中搜尋追蹤記錄。

集中式記錄是以一系列預先定義的案例為主來建立，可提供比舊版 Lync Server 更精確的記錄方法。這些案例可為您預先決定伺服器元件與記錄功能；因此，啟用 RGS 案例的管理員確信將只會記錄與「回應群組」服務有關的資訊，而非不相關的服務，例如音訊會議提供者服務。

使用 [New-CsClsScenario](new-csclsscenario.md) Cmdlet 自訂案例，然後將新案例加入集中式記錄組態設定。所有案例都可以透過 **Set-CsClsScenario** Cmdlet 加以修改。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsClsScenario"}

Lync Server 控制台：**Set-CsClsScenario** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要修改之案例的唯一識別碼。案例包含兩個部分：案例設定所在的範圍 (亦即，可以找到案例的集中式記錄組態設定集合) 及案例名稱。例如：</p>
<p>-Identity &quot;site:Redmond/AddressBook&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>允許您傳遞物件參考，而不設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>Provider</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>案例的記錄提供者。新提供者必須使用 <strong>New-CsClsProvider</strong> Cmdlet 加以建立。例如：</p>
<p>$provider = New-CsClsProvider –Name &quot;UserServices&quot; –Type &quot;WPP&quot; –Level &quot;Info&quot; –Flags &quot;All&quot;</p></td>
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

**Set-CsClsScenario** Cmdlet 接受管線傳送的 Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.Scenario\#Decorated 物件執行個體。

## 傳回類型

無。反之， **Set-CsClsScenario** Cmdlet 會修改現有的 Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.Scenario\#Decorated 物件執行個體。

