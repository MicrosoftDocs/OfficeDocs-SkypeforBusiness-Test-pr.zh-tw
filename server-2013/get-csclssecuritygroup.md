---
title: Get-CsClsSecurityGroup
TOCTitle: Get-CsClsSecurityGroup
ms:assetid: ce7aa87a-2355-4025-bba8-d4debf2137d2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205285(v=OCS.15)
ms:contentKeyID: 49292355
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsClsSecurityGroup

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織使用之集中式記錄組態安全性群組的資訊。集中式記錄讓系統管理員可以同時啟用或停用多部電腦上的事件追蹤。安全性群組主要會在 商務用 Skype Online 上使用。

Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Get-CsClsSecurityGroup [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsClsSecurityGroup [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回設定供組織使用之所有集中式記錄安全性群組的資訊。

    Get-CsClsSecurityGroup

## 範例 2

範例 2 會傳回單一集中式記錄安全性群組 (即 Identity 為 global/helpdesk 的群組) 的資訊。

    Get-CsClsSecurityGroup -Identity "global/HelpDesk"

## 範例 3

範例 3 會傳回在全域範圍設定之所有集中式記錄安全性群組的資訊。為達此目的，會加入 Filter 參數搭配篩選值 "global/\*" (此篩選值會將傳回的資料限制在全域範圍設定的群組)。

    Get-CsClsSecurityGroup -Filter "global/*"

## 範例 4

範例 4 所示的命令會傳回存取層級設為 RedmondSupport 的所有集中式記錄安全性群組。為了執行此工作，命令會先呼叫不含任何參數的 **Get-CsClsSecurityGroup** Cmdlet，以傳回所有可用的集中式記錄安全性群組集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 AccessLevel 屬性等於 RedmondSupport 的群組。

    Get-CsClsSecurityGroup | Where-Object {$_.AccessLevel -eq "RedmondSupport"}

## 詳細描述

集中式記錄服務 (取代 Microsoft Lync Server 2010 中使用的 OCSLogger 與 OCSTracer 工具) 提供一種方法，讓管理員管理所有執行 Lync Server 2013 之電腦與集區的記錄和追蹤。集中式記錄可讓管理員利用單一命令，來停止、啟動及設定一或多個集區與電腦的記錄；例如，您可以使用一個命令，在所有 Address Book Server 上啟用通訊錄服務記錄功能。這和必須在每部伺服器上個別管理 (包括個別停止和啟動) 的 OCSLogger 與 OCSTracer 工具不同。此外，集中式記錄服務也提供一種方法，讓系統管理員可以使用 Windows PowerShell 命令列介面與 [Search-CsClsLogging](search-csclslogging.md) Cmdlet，從命令中搜尋追蹤記錄。

在 商務用 Skype Online 中，安全性群組可用於判斷有權存取要寫入記錄檔之個人識別資訊的使用者。在使用 [New-CsClsSecurityGroup](new-csclssecuritygroup.md) Cmdlet 建立安全性群組後，會將其新增至集中式記錄組態設定集合。您可以使用 **Get-CsClsSecurityGroup** Cmdlet，以傳回集中式記錄安全性群組的資訊。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsClsSecurityGroup"}

**Lync Server 控制台：** **Get-CsClsSecurityGroup** Cmdlet 的執行功能並未提供於 Lync Server 控制台。

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
<td><p>可讓您使用萬用字元傳回一或多個集中式記錄安全性群組。例如，若要傳回在全域範圍設定的所有群組集合，請使用下列語法：</p>
<p>-Filter &quot;global/*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要傳回之集中式記錄安全性群組的唯一識別碼。安全性群組識別由建立群組的範圍與群組名稱組成。例如，若要傳回在全域範圍建立的群組 HelpDesk，請使用下列語法：</p>
<p>-Identity &quot;global/HelpDesk&quot;</p>
<p>如果未指定此參數， <strong>Get-CsClsSecurityGroup</strong> Cmdlet 會傳回所有集中式記錄安全性群組的資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區的本機複本擷取集中式記錄組態資料，而非從 中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Get-CsClsSecurityGroup** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsClsSecurityGroup** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.SecurityGroup\#Decorated 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsClsSecurityGroup](new-csclssecuritygroup.md)  
[Remove-CsClsSecurityGroup](remove-csclssecuritygroup.md)  
[Set-CsClsSecurityGroup](set-csclssecuritygroup.md)

