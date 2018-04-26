---
title: Remove-CsClsConfiguration
TOCTitle: Remove-CsClsConfiguration
ms:assetid: f10005f4-ae5c-4d9e-800f-48183b5182be
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ619191(v=OCS.15)
ms:contentKeyID: 49292761
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsClsConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除一或多個集中式記錄組態設定的集合。集中式記錄提供一種方法，讓管理員同時啟用或停用多部電腦上的事件追蹤功能。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Remove-CsClsConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會移除套用到 Redmond 網站的集中式記錄組態設定。

    Remove-CsClsConfiguration -Identity "site:Redmond"

## 範例 2

在範例 2 中，會移除套用到網站範圍的所有集中式記錄組態設定。若要這樣做，此命令會先呼叫 **Get-CsClsConfiguration** Cmdlet 搭配 Filter 參數；篩選值 "site:\*" 會將傳回的資料限制為在網站範圍設定的設定。接著那些設定會管道傳送至 **Remove-CsClsConfiguration** Cmdlet，並由其移除。

    Get-CsClsConfiguration -Filter "site:*" | Remove-CsClsConfiguration

## 範例 3

範例 3 會刪除允許 ETL 檔案超過 20 MB 的所有集中式記錄組態設定。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsClsConfiguration** Cmdlet；如此會傳回組織使用中的所有集中式記錄組態設定集合。接著，那些設定會管道傳送到 **Where-Object** Cmdlet，這會只挑出 EtlFileRollverSizeMB 屬性大於 (-gt) 20 MB 的設定。然後將符合該準則的設定管道傳送到 **Remove-CsClsConfiguration** Cmdlet，並由其刪除。

    Get-CsClsConfiguration | Where-Object {$_.EtlFileRolloverSizeMB -gt 20} | Remove-CsClsConfiguration

## 詳細描述

集中式記錄服務 (取代 Microsoft Lync Server 2010 中使用的 OCSLogger 與 OCSTracer 工具) 提供一種方法，讓管理員管理所有執行 Lync Server 2013 之電腦與集區的記錄和追蹤。集中式記錄可讓管理員利用單一命令，來停止、啟動及設定一或多個集區與電腦的記錄；例如，您可以使用一個命令，在所有 Address Book Server 上啟用通訊錄服務記錄功能。這和必須在每部伺服器上個別管理 (包括個別停止和啟動) 的 OCSLogger 與 OCSTracer 工具不同。此外，集中式記錄服務也提供一種方法，讓管理員使用 Windows PowerShell 命令列介面與 [Search-CsClsLogging](search-csclslogging.md) Cmdlet，從命令中搜尋追蹤記錄。

集中式記錄是以一系列預先定義的案例為主來建立，可提供比舊版 Lync Server 更精確的記錄方法。這些案例可為您預先決定伺服器元件與記錄功能；因此，啟用 RGS 案例的管理員確信將只會記錄與「回應群組」服務有關的資訊，而非不相關的服務，例如音訊會議提供者服務。

您也可以使用 [New-CsClsScenario](new-csclsscenario.md) Cmdlet，定義自訂的案例。

您可以使用集中式記錄服務組態設定的集合來管理集中式記錄。當您安裝 Lync Server 2013 時，就會安裝一組這類的全域組態設定；此外，管理員可以在網站範圍新增自訂的設定集合。稍後，您可以使用 **Remove-CsClsConfiguration** Cmdlet 來移除這些網站範圍設定。請注意，您也可以對全域設定集合執行此 Cmdlet。不過，在該情況下，將不會移除集合。而是將該集合中的所有屬性重設為預設值。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsClsConfiguration"}

**Lync Server 控制台：** **Remove-CsClsConfiguration** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p>您要移除之集中式記錄組態設定集合的唯一識別碼。若要移除全域設定，請使用此語法：</p>
<p>-Identity &quot;global&quot;</p>
<p>請注意，這樣做實際上不會移除全域原則，而是將所有原則屬性重設為其預設值。</p>
<p>若要修改在網站範圍設定的集合，請使用類似如下的語法：</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>請注意，指定 Identity 時，無法使用萬用字元。</p></td>
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
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

**Remove-CsClsConfiguration** Cmdlet 接受 Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.CentralizedLoggingConfiguration 物件的管道傳送執行個體。

## 傳回類型

無。 而是 **Remove-CsClsConfiguration** Cmdlet 會刪除現有的 Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.CentralizedLoggingConfiguration 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsClsConfiguration](get-csclsconfiguration.md)  
[New-CsClsConfiguration](new-csclsconfiguration.md)  
[Set-CsClsConfiguration](set-csclsconfiguration.md)

