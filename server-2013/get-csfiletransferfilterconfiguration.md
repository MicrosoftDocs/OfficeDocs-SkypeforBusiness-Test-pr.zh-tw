---
title: Get-CsFileTransferFilterConfiguration
TOCTitle: Get-CsFileTransferFilterConfiguration
ms:assetid: 6f43c203-acd6-4dbf-a071-752bf0c1727c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398527(v=OCS.15)
ms:contentKeyID: 49291274
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsFileTransferFilterConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織的檔案傳輸篩選組態。這些組態的用途，在禁止使用者使用 Lync Server 用戶端傳輸特定檔案類型 (例如副檔名為 .vbs 或 .ps1 的檔案)。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsFileTransferFilterConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsFileTransferFilterConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回設為在組織中使用之所有檔案傳輸篩選組態的集合。每當您呼叫不含其他任何參數的 **Get-CsFileTransferFilterConfiguration** Cmdlet 時，此為預設行為。

    Get-CsFileTransferFilterConfiguration

## 範例 2

範例 2 會傳回單一檔案傳輸篩選組態：組態的 Identity 為 site:Redmond。由於識別身分必須是唯一的，因此此命令絕對不會傳回一個以上的組態。

    Get-CsFileTransferFilterConfiguration -Identity site:Redmond

## 範例 3

範例 3 使用 Filter 參數傳回在網站層級上所有檔案傳輸篩選組態的集合。Filter 值 "site:\*" 會指示 **Get-CsFileTransferFilterConfiguration** Cmdlet 僅傳回 Identity 開頭為字串值 "site:" 的組態。

    Get-CsFileTransferFilterConfiguration -Filter site:*

## 範例 4

範例 4 所示的命令只會傳回在禁止副檔名清單中包含 .xls 的檔案傳輸篩選組態。為達成此目的，會先使用 **Get-CsFileTransferFilterConfiguration** Cmdlet 傳回組織所使用之所有組態的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet 套用篩選，將傳回的資料限制在 Extensions 屬性包含 (-contains) 字串值 ".xls" 的組態。

    Get-CsFileTransferFilterConfiguration | Where-Object {$_.Extensions -contains ".xls"}

## 範例 5

範例 5 會傳回目前停用的所有檔案傳輸篩選組態。為達此目的，會使用 **Get-CsFileTransferFilterConfiguration** Cmdlet 傳回設定供組織使用之所有組態的集合。然後將此集合以管線傳送到 **Where-Object** Cmdlet，接著此 Cmdlet 只會選取 Enabled 屬性等於 (-eq) False ($False) 的組態。

    Get-CsFileTransferFilterConfiguration | Where-Object {$_.Enabled -eq $False}

## 範例 6

範例 6 會顯示全域檔案傳輸篩選組態所禁止的完整副檔名清單。此命令的開頭是呼叫 **Get-CsFileTransferFilterConfiguration** Cmdlet，以指定 Global 組態集合。然後，傳回的資訊會傳送到 **Select-Object** Cmdlet，以使用 ExpandProperty 參數來「展開」Extensions 屬性的值。如此會產生完整副檔名清單，顯示於畫面上，每行一個副檔名。

    Get-CsFileTransferFilterConfiguration -Identity Global | Select-Object -ExpandProperty Extensions

## 詳細描述

傳送立即訊息時，使用者可以在交談中附加及傳送檔案給其他參與者。 Lync Server 可以設定為不允許使用 Lync 用戶端傳送具有特定副檔名的檔案 (通常是可能證明有害的檔案類型副檔名)。

**Get-CsFileTransferFilterConfiguration** Cmdlet 提供一種方法，讓您擷取特定設定集合 (這些設定可在全域範圍或網站範圍設定) 的設定。檔案傳輸篩選組態包括封鎖傳輸的副檔名清單、啟用篩選的程度 (封鎖所有檔案傳輸或僅封鎖具特定副檔名的檔案)，以及是否啟用檔案傳輸篩選。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsFileTransferFilterConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsFileTransferFilterConfiguration"}

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
<td><p>System.String</p></td>
<td><p>可讓您在指定要傳回的檔案傳輸篩選組態時，使用萬用字元。例如，若要傳回在網站範圍的所有檔案傳輸篩選組態，請使用下列語法：-Filter &quot;site:*&quot;。根據設計，具有 Identity (唯一可以當做篩選依據的屬性) 開頭字串值為 &quot;site&quot; 的檔案傳輸篩選組態：都是在網站範圍設定的設定。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要擷取之檔案傳輸篩選組態的唯一識別碼。若要參考全域設定，請使用下列語法：-Identity global。若要參照已設定於網站範圍上的設定，請使用類似下列的語法：-Identity site:Redmond。請注意，如有指定 Identity，即無法使用萬用字元值。如果要使用萬用字元，請改用 Filter 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區的本機複本擷取檔案傳輸篩選組態，而非從 中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

**Get-CsFileTransferFilterConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.FileTransferFilterConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsFileTransferFilterConfiguration](new-csfiletransferfilterconfiguration.md)  
[Remove-CsFileTransferFilterConfiguration](remove-csfiletransferfilterconfiguration.md)  
[Set-CsFileTransferFilterConfiguration](set-csfiletransferfilterconfiguration.md)

