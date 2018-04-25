---
title: Get-CsCdrConfiguration
TOCTitle: Get-CsCdrConfiguration
ms:assetid: 4af8ffa2-63d3-4873-8dac-5afede090d4f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398298(v=OCS.15)
ms:contentKeyID: 49290838
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsCdrConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回通話詳細記錄 (CDR) 設定的資訊。CDR 可讓您追蹤對等立即訊息工作階段、Voice over Internet Protocol (VoIP) 電話及會議電話的使用方式。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsCdrConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsCdrConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

此範例會使用 **Get-CsCdrConfiguration** Cmdlet 傳回設定為在組織中使用之所有 CDR 設定的集合。

    Get-CsCdrConfiguration

## 範例 2

範例 2 會使用 Identity 參數，傳回單一 CDR 設定集合：Identity 為 site:Redmond 的設定。

    Get-CsCdrConfiguration -Identity site:Redmond

## 範例 3

範例 3 會使用 Filter 參數傳回網站範圍所設定的所有 CDR 設定。篩選值 "site:\*" 可傳回 Identity 開頭為字串值 "site:" 的所有 CDR 設定。根據定義，這些是在網站範圍設定的設定。

    Get-CsCdrConfiguration -Filter site:*

## 範例 4

範例 4 會傳回 KeepCallDetailForDays 屬性少於 30 天的所有 CDR 設定集合。為達成此目的，命令會先使用 **Get-CsCdrConfiguration** Cmdlet 傳回組織中所設定之所有 CDR 設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 KeepCallDetailForDays 值小於 30 天的設定。

    Get-CsCdrConfiguration | Where-Object {$_.KeepCallDetailForDays -lt 30}

## 詳細描述

通話詳細記錄 (CDR) 讓您能夠追蹤 Lync Server 功能的使用狀況，這些功能包括 Voice over IP (VoIP) 通話、立即訊息、檔案傳輸、音訊/視訊 (A/V) 會議，以及應用程式分享工作階段。CDR (只有在您部署了監控服務後才可使用) 會保留使用資訊：它會記錄通話方、通話長度、是否傳輸任何檔案等資訊 (但 CDR 不會記錄通話本身)。

CDR 也會追蹤通話錯誤資訊：點對點工作階段與會議電話的詳細診斷資料。

做為系統管理員，您可以決定是否要在組織中使用 CDR。假設已部署監控服務，就可以啟用或停用 CDR。此外，您還可以依全域 (在整個組織啟用或停用 CDR) 或個別網站的基礎來進行此決策；例如，您可以在 Redmond 網站使用 CDR，但在 Paris 網站不使用 CDR。

**Get-CsCdrConfiguration** Cmdlet 可讓您傳回關於 CDR 在組織中的使用方式。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsCdrConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsCdrConfiguration"}

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
<td><p>可讓您使用萬用字元傳回 CDR 組態設定集合。例如，若要傳回在此網站範圍所設定之所有設定集合，請使用下列語法：-Filter site:*。若要傳回在 Identity 中任何位置出現字串值 &quot;Western&quot; 的所有設定集合，請使用下列語法：-Filter *Western*。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>表示您要傳回之 CDR 組態設定集合的唯一識別碼。若要參考全域設定，請使用下列語法：-Identity global。若要參考在網站範圍設定的集合，請使用類似下列的語法：-Identity site:Redmond。請注意，如有指定 Identity，即無法使用萬用字元。如果您需要使用萬用字元，請改用 Filter 參數。</p>
<p>若未指定此參數，則 <strong>Get-CsCdrConfiguration</strong> Cmdlet 會傳回組織中目前使用之所有 CDR 組態設定的集合。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取 CDR 組態資料，而非從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsCdrConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsCdrConfiguration** Cmdlet 傳回 Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CdrSettings 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsCdrConfiguration](new-cscdrconfiguration.md)  
[Remove-CsCdrConfiguration](remove-cscdrconfiguration.md)  
[Set-CsCdrConfiguration](set-cscdrconfiguration.md)

