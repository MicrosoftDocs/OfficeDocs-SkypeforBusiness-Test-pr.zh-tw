---
title: Get-CsVoicemailReroutingConfiguration
TOCTitle: Get-CsVoicemailReroutingConfiguration
ms:assetid: 25e401eb-6a84-468f-b0eb-5b794f20b5bc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425732(v=OCS.15)
ms:contentKeyID: 49290370
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsVoicemailReroutingConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

擷取提供存取 Exchange UM 使用者存取與自動語音應答功能所需之公共交換電話網路 (PSTN) 電話號碼的設定。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsVoicemailReroutingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsVoicemailReroutingConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

此範例會擷取在這個 Lync Server 部署中定義的所有語音信箱重新路由組態設定。例如，如果已部署 Survivable Branch Appliance 的分公司有三個，此命令將會傳回三個語音信箱重新路由組態集。

    Get-CsVoicemailReroutingConfiguration

## 範例 2

此範例會擷取 BranchOffice\_Portland 網站的語音信箱重新路由組態設定。

    Get-CsVoicemailReroutingConfiguration -Identity site:BranchOffice_Portland

## 範例 3

此範例會擷取網站名稱開頭字串為 BranchOffice (例如 BranchOffice\_Portland、BranchOffice\_Sacramento) 之所有網站的所有語音信箱重新路由設定。

    Get-CsVoicemailReroutingConfiguration -Filter *:BranchOffice*

## 範例 4

此範例會擷取所有未啟用的語音信箱重新路由組態。此命令的第一個部分是呼叫 **Get-CsVoicemailReroutingConfiguration** Cmdlet，這會擷取所有語音信箱重新路由組態的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet。**Where-Object** Cmdlet 會縮小集合的範圍，只包含 Enabled 屬性等於 (-eq) False 的組態。

    Get-CsVoicemailReroutingConfiguration | Where-Object {$_.Enabled -eq $False}

## 詳細描述

當分支網站中的 Lync Server 至位於資料中心之 Exchange UM Server 的 IP 連線無法使用時，此 Cmdlet 會擷取決定「自動語音應答」和「使用者存取」通話要重新路由到哪裡的設定。

「自動語音應答」和「使用者存取」是 Exchange UM 的功能。「自動語音應答」功能會提供語音辨識與按鍵觸控 (雙音多頻 (DTMF)) 功能供外部來電者導覽公司的電話系統，以連絡到所需的部門或員工，或在「留言模式」中接受使用者留言 (建議使用「留言模式」的語音重新路由)。「使用者存取」可讓內部使用者透過電話存取其 Microsoft Outlook 信箱。這些設定提供的號碼允許來電者在語音信箱留言，讓 Enterprise Voice 使用者 (AutoAttendantNumber 設定) 和這些使用者能夠擷取語音信箱，即使從遠端網站的 Lync Server 部署到資料中心的 Exchange UM 之間沒有 IP 連線可用 (SubscriberAccessNumber 設定) 也一樣。

不使用任何參數而直接呼叫此 Cmdlet，將會傳回所有語音信箱重新路由組態。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsVoicemailReroutingConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsVoicemailReroutingConfiguration"}

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
<td><p>Filter 參數可讓您依據萬用字元比對，擷取特定一組網站的組態設定。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>您要擷取之組態的唯一識別碼。針對此 Cmdlet，Identity 將是 Global 或 Site:&lt;網站名稱&gt;，其中 &lt;網站名稱&gt; 是要套用設定之網站的名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取語音信箱重新路由組態，而非從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

擷取 Microsoft.Rtc.Management.WritableConfig.Settings.ExumRouting.VoicemailReroutingConfiguration 類型的一或多個物件。

## 請參閱

#### 其他資源

[New-CsVoicemailReroutingConfiguration](new-csvoicemailreroutingconfiguration.md)  
[Remove-CsVoicemailReroutingConfiguration](remove-csvoicemailreroutingconfiguration.md)  
[Set-CsVoicemailReroutingConfiguration](set-csvoicemailreroutingconfiguration.md)

