---
title: Get-CsClsScenario
TOCTitle: Get-CsClsScenario
ms:assetid: 8f0c5f52-c000-4e27-82a2-534a50b11a98
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205091(v=OCS.15)
ms:contentKeyID: 49291640
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsClsScenario

 

_**上次修改主題的時間：** 2015-03-09_

傳回一或多個集中式記錄組態案例的資訊。案例代表系統管理員可啟用或停用追蹤的特定 Lync Server 2013 元件或狀況 (例如 IM 和目前狀態)。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsClsScenario [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsClsScenario [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回目前組織正在使用的所有集中式記錄案例相關資訊。

    Get-CsClsScenario

## 範例 2

範例 2 會傳回單一集中式記錄案例的資訊：包含在全域設定集合中的 VoiceMail 案例。

    Get-CsClsScenario -Identity "global/VoiceMail"

## 範例 3

範例 3 會傳回目前使用的所有預設案例相關資訊。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsClsScenario** Cmdlet，以傳回所有可用案例的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 Provider 名稱包含 (-match) "AsMcu" 的案例。

    Get-CsClsScenario | Where-Object {$_.Provider.Name -match "AsMcu"}

## 範例 4

範例 4 會傳回全域 VoiceMail 案例之 Provider 屬性的詳細資訊。為了執行此工作，命令會先使用 **Get-CsClsScenario** Cmdlet，以傳回全域 VoiceMail 案例的所有屬性值。然後再將該資訊管線傳送到 Select-Object Cmdlet，以使用 ExpandProperty 參數「展開」Provider 屬性的值，進而將儲存在 Provider 屬性中的所有資料，以易於閱讀的格式顯示在畫面上。

    Get-CsClsScenario -Identity "global/VoiceMail" | Select-Object -ExpandProperty Provider

## 詳細描述

集中式記錄服務 (取代 Microsoft Lync Server 2010 中使用的 OCSLogger 與 OCSTracer 工具) 提供一種方法，讓管理員管理所有執行 Lync Server 2013 之電腦與集區的記錄和追蹤。集中式記錄可讓管理員利用單一命令，來停止、啟動及設定一或多個集區與電腦的記錄；例如，您可以使用一個命令，在所有 Address Book Server 上啟用通訊錄服務記錄功能。這和必須在每部伺服器上個別管理 (包括個別停止和啟動) 的 OCSLogger 與 OCSTracer 工具不同。此外，集中式記錄服務也提供一種方法，讓管理員使用 Windows PowerShell 命令列介面與 [Search-CsClsLogging](search-csclslogging.md) Cmdlet，從命令中搜尋追蹤記錄。

集中式記錄是以一系列預先定義的案例為主來建立，可提供比舊版 Lync Server 更精確的記錄方法。這些案例可為您預先決定伺服器元件與記錄功能；因此，啟用 RGS 案例的管理員確信將只會記錄與「回應群組」服務有關的資訊，而非不相關的服務，例如音訊會議提供者服務。

使用 **Get-CsClsScenario** Cmdlet 可以傳回組織中可供使用之所有集中式記錄案例的資訊。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsClsScenario"}

Lync Server 控制台： Lync Server 控制台不提供 **Get-CsClsScenario** Cmdlet 所執行的功能。

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
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可讓您使用萬用字元來傳回一或多個案例。例如，若要傳回所有 HybridVoice 案例，無論設定這些案例所在的範圍為何，請使用下列語法：</p>
<p>-Filter &quot;*HybridVoice*&quot;</p>
<p>同一個命令中不可同時使用 Identity 參數與 Filter 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>所要傳回之案例的唯一識別碼。案例包含兩個部分：案例設定所在的範圍 (亦即，可以找到該案例的集中式記錄組態設定集合) 及案例名稱。例如：</p>
<p>-Identity &quot;site:Redmond/AddressBook&quot;</p>
<p>您也可以只指定案例範圍；例如：</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>在該情況下，將會傳回設定用於 Redmond 網站的所有案例。</p>
<p>若未指定此參數， <strong>Get-CsClsScenario</strong> Cmdlet 將會傳回所有集中式記錄案例的資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取案例資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Get-CsScenario** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsScenario** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.Scenario\#Decorated 物件的執行個體。

