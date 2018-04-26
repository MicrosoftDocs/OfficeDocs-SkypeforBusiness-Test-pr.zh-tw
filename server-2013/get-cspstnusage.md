---
title: Get-CsPstnUsage
TOCTitle: Get-CsPstnUsage
ms:assetid: 9dc82b88-303b-4678-8298-0dbc769f6781
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412734(v=OCS.15)
ms:contentKeyID: 49291833
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPstnUsage

 

_**上次修改主題的時間：** 2015-03-09_

傳回關於組織所使用之公用交換電話網路 (PSTN) 使用方式記錄的資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsPstnUsage [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsPstnUsage [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

這個命令會傳回組織內可用的全域 PSTN 使用方式清單。

    Get-CsPstnUsage

## 範例 2

此範例中的命令會傳回所有已定義之 PSTN 使用方式的清單，並且在輸出的每一行列出一個使用方式。單獨呼叫 **Get-CsPstnUsage** Cmdlet 會傳回 Identity 及 Usage 清單。如果 Usage 清單包含三個或四個以上的項目，清單將會在輸出中縮短，類似如下所示：

Usage :{Internal, Local, Long Distance, International...}

使用本例中的命令可只顯示使用方式的清單。輸出類似於下列：

Internal

Local

Long Distance

International

Restricted

    (Get-CsPstnUsage).Usage

## 範例 3

這個命令會傳回名稱內出現 "tern" 字串的所有 PSTN 使用方式名稱。例如，這個命令會傳回 "Internal" 和 "International"，但不會傳回 "Local" 或 "Long Distance"。

此命令的第一個部分是括弧內的 **Get-CsPstnUsage** Cmdlet，這表示最先進行的動作是擷取所有的 PSTN 使用方式。.Usage 屬性只會傳回 PSTN 使用方式的使用方式資訊，而不會傳回 Identity。這份使用方式清單接著會傳送至 **ForEach-Object** Cmdlet，它會一次查看一個使用方式字串。If 陳述式會比對目前的使用方式字串以及字串 "\*tern\*" (\* 為萬用字元)，然後顯示符合該模式的任何出現項目。

    (Get-CsPstnUsage).Usage | ForEach-Object {if ($_ -like "*tern*") {$_}}

## 詳細描述

PSTN 使用方式是用於電話授權的字串值。PSTN 使用方式會將語音原則連結至路由。**Get-CsPstnUsage** Cmdlet 會擷取組織內可用的所有 PSTN 使用方式清單。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsPstnUsage** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPstnUsage"}

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
<td><p>Filter 參數允許您只擷取 Identity 符合特定萬用字元字串的 PSTN 使用方式。不過，PSTN 使用方式唯一可用的 Identity 是 Global，因此此參數對此 Cmdlet 沒有作用。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>套用這些設定的層級。唯一可以套用至 PSTN 使用方式的 Identity 是 Global。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從本機資料存放區擷取 PSTN 使用方式資訊，而不從主要的 中央管理存放區 擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

**Get-CsPstnUsage** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.PSTNUsages 物件的執行個體。

## 請參閱

#### 其他資源

[Set-CsPstnUsage](set-cspstnusage.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)

