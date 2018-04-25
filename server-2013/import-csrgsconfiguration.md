---
title: Import-CsRgsConfiguration
TOCTitle: Import-CsRgsConfiguration
ms:assetid: c4977e34-7a62-4cb7-b8ec-bacb471b3de4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205245(v=OCS.15)
ms:contentKeyID: 49292250
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Import-CsRgsConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

匯入之前使用 **Export-CsRgsConfiguration** Cmdlet 匯出的回應群組組態資料。在災害復原案例中，匯出及匯入回應群組組態資料的功能特別實用。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Import-CsRgsConfiguration -Destination <RgsIdentity> -FileName <String> [-Force <SwitchParameter>] [-OverwriteOwner <SwitchParameter>] [-ReplaceExistingRgsSettings <SwitchParameter>] [-ResolveNameConflicts <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會匯入先前匯出的回應群組應用程式設定集合，然後將那些設定套用至 atl-cs-001.litwareinc.com 上由應用程式伺服器主控的回應群組安裝。

    Import-CsRgsConfiguration -FileName "C:\Export\RgsExport.zip" -Destination "ApplicationServer:atl-cs-001.litwareinc.com"

## 詳細描述

[Export-CsRgsConfiguration](export-csrgsconfiguration.md) Cmdlet 與 **Import-CsRgsConfiguration** Cmdlet 可讓您匯出現有回應群組應用程式實作 (包括工作流程、佇列、代理群組、假日集與營業時間，以及音訊檔與服務組態設定) 的資料，然後再匯入 (或重新匯入) 該資訊。這對災害復原 (例如代管回應群組應用程式的伺服器失效) 或單純要將回應群組應用程式移轉到不同集區時十分實用。

請注意，**Export-CsRgsConfiguration** Cmdlet 與 **Import-CsRgsConfiguration** Cmdlet 只可搭配 Lync Server 2013 一起使用。若要將回應群組資料從 Microsoft Lync Server 2010 移轉至 Lync Server 2013，請改用 [Move-CsRgsConfiguration](move-csrgsconfiguration.md) Cmdlet。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Import-CsRgsConfiguration"}

**Lync Server 控制台:**Lync Server 控制台不提供 **Import-CsRgsConfiguration** Cmdlet 所執行的功能。

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
<td><p><em>Destination</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>要匯入組態設定之回應群組執行個體的識別。例如：</p>
<p>-Destination &quot;ApplicationServer:atl-rgs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>FileName</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p><strong>Export-CsRgsConfiguration</strong> Cmdlet 建立之 .ZIP 檔案的路徑。例如：</p>
<p>-FileName &quot;C:\Exports\RgsConfig.zip&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏顯示當執行命令時可能發生的任何非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>OverwriteOwner</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>目前若已有回應群組物件擁有者，將會以新回應群組集區的服務識別取代。</p></td>
</tr>
<tr class="odd">
<td><p><em>ReplaceExistingRgsSettings</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>指定此參數時，目的地集區的所有現存服務設定都會取代成匯入的設定。如果不指定此參數，服務設定就會維持原狀，只會匯入回應群組物件 (例如工作流程和代理群組)。</p></td>
</tr>
<tr class="even">
<td><p><em>ResolveNameConflicts</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>如有設定，當名稱重複時，將會在名稱後附加唯一的識別號碼。例如，若有兩個工作流程的名稱均是 Help Desk Workflow，便會將其中一個工作流程名稱變更為 Help Desk Workflow (2)。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Import-CsRgsConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。

## 請參閱

#### 其他資源

[Export-CsRgsConfiguration](export-csrgsconfiguration.md)

