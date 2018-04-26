---
title: Remove-CsCpsConfiguration
TOCTitle: Remove-CsCpsConfiguration
ms:assetid: 546343e1-a2e4-4bc0-bf6d-c8ae9bb3e690
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398358(v=OCS.15)
ms:contentKeyID: 49290938
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsCpsConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除現有的通話駐留服務組態。通話駐留是可以讓使用者「駐留」來電的服務。駐留通話會將來電轉接到指定範圍或軌道內的號碼，然後立即將來電設為保留。任何人 (不只是原來接聽電話的人) 只要輸入正確的號碼，即可從任何電話回復通話。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsCpsConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會使用 **Remove-CsCpsConfiguration** Cmdlet 來刪除 Identity 為 site:Redmond1 的通話駐留服務組態。由於識別是唯一的，因此此命令只會刪除一個組態。

    Remove-CsCpsConfiguration -Identity site:Redmond1

## 範例 2

範例 2 會刪除所有已在網站範圍內定義的通話保留服務組態。為了執行此工作，命令會先使用 **Get-CsCpsConfiguration** Cmdlet 搭配 Filter 參數，以傳回在網站範圍定義的所有通話駐留服務組態 (萬用字元 site:\* 可確保只會傳回 Identity 開頭為字串值 site: 的設定)。然後再將篩選後的集合管線傳送到 **Remove-CsCpsConfiguration** Cmdlet，以繼續刪除集合中每一個項目。請注意，每當您移除網站中的通話保留服務設定時，網站便會自動開始使用於全域範圍內設定的通話保留服務設定。

    Get-CsCpsConfiguration -Filter site:* | Remove-CsCpsConfiguration

## 詳細描述

此 Cmdlet 可用來移除通話駐留服務組態。通話駐留服務組態會指定駐留通話後的動作。例如，如果駐留的通話在一段時間內沒有回應，則可自動轉接其他人 (例如系統管理員) 或回應群組。可以設定來電在一段期間後響鈴，以確保不會忘掉來電。此外，可以設定通話駐留服務在駐留通話時，向等待的來電者播放的等候音樂。

可以使用這個 Cmdlet 移除任何通話駐留組態，包括 Global 組態。但如果是 Global 設定，不會真的移除設定，而是重設為預設值。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsCpsConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsCpsConfiguration"}

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
<td><p>您要移除之通話駐留服務設定的唯一識別碼。這個識別碼將是 Global 或 site:&lt;網站名稱&gt;，其中 &lt;網站名稱&gt; 是設定套用之網站的名稱。</p></td>
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
<td><p>隱藏變更前所顯示的確認提示。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings 物件。接受管線傳送的通話保留服務組態物件輸入。

## 傳回類型

移除 Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings 類型的物件。

## 請參閱

#### 其他資源

[New-CsCpsConfiguration](new-cscpsconfiguration.md)  
[Set-CsCpsConfiguration](set-cscpsconfiguration.md)  
[Get-CsCpsConfiguration](get-cscpsconfiguration.md)  
[Set-CsCallParkServiceMusicOnHoldFile](set-cscallparkservicemusiconholdfile.md)

