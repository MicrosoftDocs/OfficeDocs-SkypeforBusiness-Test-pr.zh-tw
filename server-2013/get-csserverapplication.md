---
title: Get-CsServerApplication
TOCTitle: Get-CsServerApplication
ms:assetid: 46769cc2-9e61-4437-b74a-24f3cf118f39
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425948(v=OCS.15)
ms:contentKeyID: 49290787
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsServerApplication

 

_**上次修改主題的時間：** 2015-03-09_

傳回組織所使用之伺服器應用程式的資訊。伺服器應用程式是 Lync Server 代管的應用程式。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsServerApplication [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsServerApplication [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回組織目前所使用之所有伺服器應用程式的資訊。作法是呼叫不含任何參數的 **Get-CsServerApplication** Cmdlet。

    Get-CsServerApplication

## 範例 2

範例 2 會傳回所有在 EdgeServer:atl-edge-001.litwareinc.com 服務上執行的伺服器應用程式資訊。

    Get-CsServerApplication -Identity "service:EdgeServer:atl-edge-001.litwareinc.com"

## 範例 3

範例 3 會傳回單一伺服器應用程式的資訊：Identity 為 Registrar:atl-cs-001.litwareinc.com/ExumRouting" 的應用程式。

    Get-CsServerApplication -Identity "service:Registrar:atl-cs-001.litwareinc.com/ExumRouting"

## 範例 4

範例 4 會傳回設定用於 atl-cs-001.litwareinc.com 集區的所有伺服器應用程式。作法是使用 Filter 參數和篩選值 "service:\*:atl-cs-001.litwareinc.com\*"。此篩選值可將傳回的資料限制在 Identity 開頭為字元 "service:" 並包含字元 ":atl-cs-001.litwareinc.com" 的應用程式。

    Get-CsServerApplication -Filter "service:*:atl-cs-001.litwareinc.com*"

## 範例 5

範例 5 會傳回目前已停用的所有伺服器應用程式資訊。為達成此目的，命令會先呼叫 **Get-CsServerApplication** Cmdlet 傳回設定供組織使用之所有伺服器應用程式的集合。然後再將該集合管線傳送給 **Where-Object** Cmdlet，這會只選取 Enabled 屬性等於 False 的應用程式。

    Get-CsServerApplication | Where-Object {$_.Enabled -eq $False}

## 範例 6

範例 6 是範例 5 所示命令的變化。範例 6 會傳回標記為重要且目前已停用的所有伺服器應用程式資訊。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsServerApplication** Cmdlet，以傳回設定供使用的所有伺服器應用程式集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出符合下列兩個條件的應用程式：Critical 內容等於 True 且 Enabled 內容等於 False。-and 運算子確保只傳回同時兩個符合準則的物件。

    Get-CsServerApplication | Where-Object {$_.Critical -eq $True -and $_.Enabled -eq $False}

## 範例 7

範例 7 會傳回 Uri 中具有字串值 "routing" 的所有伺服器應用程式資訊。為達成此目的，會先使用 **Get-CsServerApplication** Cmdlet 擷取目前所使用的所有伺服器應用程式。然後再將產生的集合管線傳送到 **Where-Object** Cmdlet，這會只選取 UI 屬性包含字串值 "routing" 的應用程式。

    Get-CsServerApplication | Where-Object {$_.Uri -like "*routing*"}

## 範例 8

範例 8 會傳回已指派指令碼的所有伺服器應用程式資訊。為達成此目的，命令會先擷取目前所使用的所有伺服器應用程式集合；作法是呼叫不含任何參數的 **Get-CsServerApplication** Cmdlet。然後再將伺服器應用程式的完整集合管線傳送到 **Where-Object** Cmdlet，這會只選取 ScriptName 屬性不等於 Null 值的應用程式。如果 ScriptName 屬性不等於 Null 值，表示指令碼已指派給該應用程式。

    Get-CsServerApplication | Where-Object {$_.ScriptName -ne $Null}

## 詳細描述

伺服器應用程式是指在 Lync Server 下執行的個別程式。**Get-CsServerApplication** Cmdlet 提供一種方法，讓系統管理員可以傳回做為 Lync Server 組件執行的任何 (或所有) 應用程式資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsServerApplication** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsServerApplication"}

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
<td><p>讓您可以在做為伺服器應用程式或伺服器應用程式集合傳回時，使用萬用字元。例如，若要傳回 Identity 中具有字串值 &quot;IIMFilter&quot; 的所有伺服器應用程式，請使用下列語法：-Filter &quot;*IIMFilter*&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要擷取之伺服器應用程式的唯一識別碼。伺服器應用程式 Identity 由託管應用程式的服務和應用程式名稱組成。例如，名為 QoEAgent 的伺服器應用程式可能會有如下的 Identity：service:Registrar:atl-cs-001.litwareinc.com/QoEAgent。</p>
<p>若要擷取在指定服務上執行的所有應用程式集合，只要略過以下應用程式名稱：</p>
<p>-Identity &quot;Registrar:atl-cs-001.litwareinc.com &quot;</p>
<p>如果省略此參數，當您呼叫 <strong>Get-CsServerApplication</strong> Cmdlet 時，會傳回所有伺服器應用程式。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區本機複本擷取伺服器應用程式資料，而不從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsServerApplication** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsServerApplication** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.ServerApplication.Application 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsServerApplication](new-csserverapplication.md)  
[Remove-CsServerApplication](remove-csserverapplication.md)  
[Set-CsServerApplication](set-csserverapplication.md)

