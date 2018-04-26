---
title: Get-CsClsConfiguration
TOCTitle: Get-CsClsConfiguration
ms:assetid: 5fef2e35-e23c-453d-97e5-cb9c4e7bfef7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ619179(v=OCS.15)
ms:contentKeyID: 49291073
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsClsConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織正在使用的集中式記錄組態設定相關資訊。集中式記錄提供一種方法，讓管理員同時啟用或停用多部電腦上的事件追蹤功能。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsClsConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsClsConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回組織目前使用中的所有集中式記錄組態設定資訊。

    Get-CsClsConfiguration

## 範例 2

在範例 2 中，會傳回單一集中式記錄組態設定集合的資訊：套用到 Redmond 網站的集合。

    Get-CsClsConfiguration -Identity "site:Redmond"

## 範例 3

範例 3 會顯示 Redmond 網站可用的集中式記錄案例詳細資訊。為達成此目的，命令會先擷取 Redmond 網站的所有集中式記錄屬性值。這些屬性值會管道傳送到 Select-Object Cmdlet，以使用 ExpandProperty 參數來「展開」在 Scenarios 屬性找到的值。當您展開屬性時，只會以易讀的方式顯示該屬性中儲存的所有資訊。

    Get-CsClsConfiguration -Identity "site:Redmond" | Select-Object -ExpandProperty Scenarios

## 範例 4

範例 4 傳回的資訊是 ETL 檔案變換間隔大於 1 小時的所有集中式記錄組態設定。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsClsConfiguration** Cmdlet；這會傳回組織中所有集中式記錄組態設定的集合。接著將此集合管道傳送到 **Where-Object** Cmdlet，這會只挑出 EtlFileRolloverMinutes 屬性大於 (-gt) 60 分鐘的設定。

    Get-CsClsConfiguration | Where-Object {$_.EtlFileRolloverMinutes -gt 60}

## 範例 5

範例 5 所示的命令和範例 4 所示的命令類似；不過，此案例中傳回的資訊只有包含 "HybridVoice" 案例的集中式記錄組態設定。為達成此目的，此命令會先使用 **Get-CsClsConfiguration** Cmdlet，以傳回所有集中式記錄組態設定的集合。接著將該集合管道傳送到 **Where-Object** Cmdlet，這會只選取至少有一個案例的 Name 屬性包含 (-match) 字串值 "HybridVoice" 的設定。

    Get-CsClsConfiguration | Where-Object {$_.Scenarios.Name -match "HybridVoice"}

## 詳細描述

集中式記錄服務 (取代 Microsoft Lync Server 2010 中使用的 OCSLogger 與 OCSTracer 工具) 提供一種方法，讓管理員管理所有執行 Lync Server 2013 之電腦與集區的記錄和追蹤。集中式記錄可讓管理員利用單一命令，來停止、啟動及設定一或多個集區與電腦的記錄；例如，您可以使用一個命令，在所有 Address Book Server 上啟用通訊錄服務記錄功能。這和必須在每部伺服器上個別管理 (包括個別停止和啟動) 的 OCSLogger 與 OCSTracer 工具不同。此外，集中式記錄服務也提供一種方法，讓管理員使用 Windows PowerShell 命令列介面與 [Search-CsClsLogging](search-csclslogging.md) Cmdlet，從命令中搜尋追蹤記錄。

集中式記錄是以一系列預先定義的案例為主來建立，可提供比舊版 Lync Server 更精確的記錄方法。這些案例可為您預先決定伺服器元件與記錄功能；因此，啟用 RGS 案例的管理員確信將只會記錄與「回應群組」服務有關的資訊，而非不相關的服務，例如音訊會議提供者服務。

您也可以使用 [New-CsClsScenario](new-csclsscenario.md) Cmdlet，定義自訂的案例。

您可以使用集中式記錄服務組態設定的集合來管理集中式記錄。當您安裝 Microsoft Lync Server 2013 時，就會安裝一組這類的全域組態設定；此外，管理員可以在網站範圍新增自訂的設定集合。 **Get-CsClsConfiguration** Cmdlet 可讓管理員傳回組織目前使用中之所有集中式記錄組態設定的資訊。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsClsConfiguration"}

**Lync Server 控制台：** **Get-CsClsConfiguration** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p>可讓您使用萬用字元，以傳回一或多個集中式記錄組態設定集合。例如，若要傳回在此網站範圍所設定之所有設定集合，請使用此語法：</p>
<p>-Filter &quot;site:*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>表示您要傳回之集中式記錄組態設定集合的唯一識別碼。若要參照全域設定，請使用此語法：</p>
<p>-Identity &quot;global&quot;</p>
<p>若要參照在此網站範圍設定的集合，請使用類似下列的語法：</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>請注意，如有指定 Identity，即無法使用萬用字元。如果您必須使用萬用字元，請改為包含 Filter 參數。</p>
<p>如果未指定此參數，則 <strong>Get-CsClsConfiguration</strong> Cmdlet 會傳回組織使用中之所有集中式記錄組態設定的集合。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取集中式記錄組態資料，而不是從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Get-CsClsConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsClsConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.CentralizedLoggingConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsClsConfiguration](new-csclsconfiguration.md)  
[Remove-CsClsConfiguration](remove-csclsconfiguration.md)  
[Set-CsClsConfiguration](set-csclsconfiguration.md)

