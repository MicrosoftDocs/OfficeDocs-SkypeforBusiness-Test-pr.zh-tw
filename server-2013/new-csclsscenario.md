---
title: New-CsClsScenario
TOCTitle: New-CsClsScenario
ms:assetid: 79ff443f-82ff-4b49-bde5-98e51e8b1ed2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205022(v=OCS.15)
ms:contentKeyID: 49291399
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsClsScenario

 

_**上次修改主題的時間：** 2015-03-09_

建立新的集中式記錄組態案例。案例代表系統管理員可啟用或停用追蹤的特定 Lync Server 2013 元件或狀況 (例如 IM 和目前狀態)。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    New-CsClsScenario -Identity <XdsIdentity> <COMMON PARAMETERS>

    New-CsClsScenario -Name <String> -Parent <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Provider <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會建立 Identity 為 global/RedmondHybridVoice 的新集中式記錄案例。為了執行此工作，範例中的第一個命令會先使用 **New-CsClsProvider** Cmdlet 建立要指派給案例的提供者，並將此新提供者儲存在名為 $provider 的變數中。

建立描述和提供者之後，範例的最後一個命令會呼叫 **New-CsClsScenario** Cmdlet 建立案例，並使用儲存在 $provider 中的資料指派 Provider 屬性的值。

    $provider = New-CsClsProvider -Name "RedmondHybridVoice" -Type "WPP" -Level "Info" -Flags "All"
    
    New-CsClsScenario -Identity "global/RedmondHybridVoice"-Provider $provider

## 詳細描述

集中式記錄服務 (取代 Microsoft Lync Server 2010 中使用的 OCSLogger 與 OCSTracer 工具) 提供一種方法，讓管理員管理所有執行 Lync Server 2013 之電腦與集區的記錄和追蹤。集中式記錄可讓管理員利用單一命令，來停止、啟動及設定一或多個集區與電腦的記錄；例如，您可以使用一個命令，在所有 Address Book Server 上啟用通訊錄服務記錄功能。這和必須在每部伺服器上個別管理 (包括個別停止和啟動) 的 OCSLogger 與 OCSTracer 工具不同。此外，集中式記錄服務也提供一種方法，讓管理員使用 Windows PowerShell 命令列介面與 [Search-CsClsLogging](search-csclslogging.md) Cmdlet，從命令中搜尋追蹤記錄。

集中式記錄是以一系列預先定義的案例為主來建立，可提供比舊版 Lync Server 更精確的記錄方法。這些案例可為您預先決定伺服器元件與記錄功能；因此，啟用 RGS 案例的管理員確信將只會記錄與「回應群組」服務有關的資訊，而非不相關的服務，例如音訊會議提供者服務。

可使用 New-CsClsScenario Cmdlet 建立自訂案例，然後將新案例加入集中式記錄組態設定的集合。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsClsScenario"}

**Lync Server 控制台：** **New-CsClsScenario** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>新案例的唯一識別碼。案例包含兩個部分：案例設定所在的範圍 (亦即，可以找到該案例的集中式記錄組態設定集合) 及案例名稱。例如：</p>
<p>-Identity &quot;site:Redmond/AddressBook&quot;</p>
<p>如有使用 Identity 參數，即不可再使用 name 參數或 Parent 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>新案例的唯一名稱。例如：</p>
<p>-Name &quot;RedmondHybridVoice&quot;</p>
<p>如有使用 Name 參數，也必須使用 Parent 參數。但請勿在使用 Name 及 Parent 參數的命令中使用 Identity 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>Parent</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>新案例所在之集中式記錄組態設定的範圍。例如，若要將新案例加入全域設定，請使用下列語法：</p>
<p>-Parent &quot;global&quot;</p>
<p>您可以使用此命令傳回所有集中式記錄「父系」的識別：</p>
<p>Get-CsClsConfiguration | Select-Object Identity</p>
<p>如有使用 Name 參數，也必須使用 Parent 參數。但請勿在使用 Name 及 Parent 參數的命令中使用 Identity 參數。</p></td>
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
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="odd">
<td><p><em>Provider</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>案例的記錄提供者。新提供者必須使用 New-CsCentralizedLoggingProvider Cmdlet 加以建立。例如：</p>
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

無。 **New-CsClsScenario** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsClsScenario** Cmdlet 會建立新的 Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.Scenario\#Decorated 物件執行個體。

