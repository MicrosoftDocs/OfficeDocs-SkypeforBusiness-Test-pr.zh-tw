---
title: Export-CsRgsConfiguration
TOCTitle: Export-CsRgsConfiguration
ms:assetid: 754513a4-0b46-44b7-8910-f865b1e0f037
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205011(v=OCS.15)
ms:contentKeyID: 49291330
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Export-CsRgsConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

從現有的回應群組應用程式組態匯出資料。此資料儲存成 .ZIP 檔，稍後可使用 **Import-CsRgsConfiguration** Cmdlet 來匯入。在災害復原案例中，匯出及匯入回應群組組態資料的功能特別實用。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Export-CsRgsConfiguration -FileName <String> -Source <RgsIdentity> [-Force <SwitchParameter>] [-Owner <RgsIdentity>] [-RemoveExportedConfiguration <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會將回應群組組態設定從集區 atl-rgs-001.litwareinc.com 匯出至路徑為 C:\\Exports\\Rgs.zip 的檔案。

    Export-CsRgsConfiguration -Source "ApplicationServer:atl-rgs-001.litwareinc.com" -FileName "C:\Exports\Rgs.zip"

## 詳細描述

**Export-CsRgsConfiguration** Cmdlet 與 [Import-CsRgsConfiguration](import-csrgsconfiguration.md) Cmdlet 可讓您匯出現有回應群組應用程式實作 (包括工作流程、佇列、代理群組、假日集與營業時間，以及音訊檔與服務組態設定) 的資料，然後再匯入 (或重新匯入) 該資訊。這對災害復原 (例如代管回應群組應用程式的伺服器失效) 或單純要將回應群組應用程式移轉到不同集區時十分實用。

請注意，**Export-CsRgsConfiguration** Cmdlet 與 **Import-CsRgsConfiguration** Cmdlet 只可搭配 Lync Server 2013 一起使用。若要將回應群組資料從 Microsoft Lync Server 2010 移轉至 Lync Server 2013，請改用 [Move-CsRgsConfiguration](move-csrgsconfiguration.md) Cmdlet。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Export-CsRgsConfiguration"}

**Lync Server 控制台：**Lync Server 控制台不提供 **Export-CsRgsConfiguration** Cmdlet 所執行的功能。

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
<td><p>當您執行 <strong>Export-CsRgsConfiguration</strong> Cmdlet 時所要建立之 .ZIP 檔案的路徑。例如：</p>
<p>-FileName &quot;C:\Exports\RgsConfig.zip&quot;</p>
<p>請注意，如果此檔案已經存在，您的命令就會失敗。</p></td>
</tr>
<tr class="even">
<td><p><em>Source</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>要匯出組態設定之回應群組執行個體的識別。例如：</p>
<p>-Source &quot;ApplicationServer:atl-rgs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Owner</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>如果指定此參數，將會匯出在指定集區上找到之所有回應群組執行個體的組態資訊。例如：</p>
<p>-Owner &quot;atl-rgs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>RemoveExportedConfiguration</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>指定此參數時，在匯出組態資訊之後，將會刪除回應群組執行個體。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Export-CsRgsConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Export-CsRgsConfiguration** Cmdlet 會建立副檔名為 .ZIP 的壓縮檔。

## 請參閱

#### 其他資源

[Import-CsRgsConfiguration](import-csrgsconfiguration.md)

