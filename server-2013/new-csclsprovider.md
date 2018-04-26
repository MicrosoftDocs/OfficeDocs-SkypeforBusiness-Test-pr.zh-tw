---
title: New-CsClsProvider
TOCTitle: New-CsClsProvider
ms:assetid: 9b0a90c1-27ab-49c8-88f2-a381cf14625e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ619187(v=OCS.15)
ms:contentKeyID: 49291777
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsClsProvider

 

_**上次修改主題的時間：** 2015-03-09_

建立新的集中式記錄追蹤提供者。追蹤提供者是應用程式元件，所產生的追蹤訊息或追蹤事件在疑難排解 Lync Server 的問題時很有用。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    New-CsClsProvider -Flags <String> -Level <All | Fatal | Error | Warning | Info | Verbose | Debug> -Name <String> -Type <WPP | EventLog | IISLog> [-Guid <String>] [-Role <String>]

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

每個集中式記錄案例需要有一或多個追蹤提供者，才會產生記錄在追蹤記錄的訊息與事件。 Lync Server 2013 隨附大量為您預先定義的提供者。 **New-CsClsProvider** Cmdlet 可讓正在擴充 Lync Server 的開發人員針對自訂的新應用程式/元件利用集中式記錄。

您也可以使用 [New-CsClsScenario](new-csclsscenario.md) Cmdlet，定義自訂的案例。

若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsClsProvider"}

Lync Server 控制台： Lync Server 控制台不提供 **New-CsClsProvider** Cmdlet 所執行的功能。

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
<td><p><em>Flags</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>指定與追蹤相關的各個通訊協定與子元件。例如，SipStack 提供者包含下列旗標：TF_COMPONENT、TF_RTCHTTP、TF_CONNECTION、TF_DIAG。</p>
<p>大部分提供者已設為使用所有可用的旗標。</p></td>
</tr>
<tr class="even">
<td><p><em>Level</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLoggingConfig.ProviderLevel</p></td>
<td><p>提供者所記錄事件的追蹤等級。允許的值為：</p>
<p>* Fatal</p>
<p>* Error</p>
<p>* Warning</p>
<p>* Info</p>
<p>* Verbose</p>
<p>* Debug</p></td>
</tr>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>新提供者的唯一名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>Type</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLoggingConfig.ProviderType</p></td>
<td><p>提供者使用的追蹤類型。允許的值為：</p>
<p>* WPP (Windows software trace preprocessor)</p>
<p>* EventLog</p>
<p>* IISLog</p></td>
</tr>
<tr class="odd">
<td><p><em>Guid</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>指派給提供者的全域唯一識別碼。</p></td>
</tr>
<tr class="even">
<td><p><em>Role</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>提供者的 Lync Server 伺服器角色。例如，前端伺服器為 FE，或者 Edge Server 為 Edge。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。New-CsClsProvider Cmdlet 不接受管線傳送的輸入。

## 傳回類型

New-CsClsProvider Cmdlet 會建立新的 Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.Provider 物件執行個體。

## 請參閱

#### 其他資源

[New-CsClsScenario](new-csclsscenario.md)  
[Set-CsClsScenario](set-csclsscenario.md)

