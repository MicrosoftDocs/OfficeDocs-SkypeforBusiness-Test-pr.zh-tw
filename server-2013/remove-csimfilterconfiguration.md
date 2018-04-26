---
title: Remove-CsImFilterConfiguration
TOCTitle: Remove-CsImFilterConfiguration
ms:assetid: 0c6f5f69-ae41-46d6-b817-fa1c6751c615
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398171(v=OCS.15)
ms:contentKeyID: 49290062
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsImFilterConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

移除指定的立即訊息 (IM) 篩選組態 (IM 篩選設定可用於禁止使用者傳送包含超連結的立即訊息)。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsImFilterConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

在範例 1 中，**Remove-CsImFilterConfiguration** Cmdlet 用來移除 Identity 為 site:Redmond 的 IM 篩選組態。從網站移除 IM 篩選組態時，該網站會自動開始使用在其位置的全域設定。

    Remove-CsImFilterConfiguration -Identity site:Redmond

## 範例 2

在範例 2 中，移除網站範圍內的所有 IM 篩選組態。為了執行此工作，命令會先使用 **Get-CsImFilterConfiguration** Cmdlet 搭配 Filter 參數，以傳回網站範圍內的所有組態；萬用字元字串 site:\* 可指示 **Get-CsImFilterConfiguration** Cmdlet 只傳回 Identity 開頭為字串值 site: 的組態。然後再將篩選後的原則集合管線傳送到 **Remove-CsImFilterConfiguration** Cmdlet，以刪除集合中的每一個組態。

    Get-CsImFilterConfiguration -Filter site:* | Remove-CsImFilterConfiguration

## 詳細描述

傳送立即訊息時，使用者可以在該訊息的文字中內嵌一個統一資源識別元 (URI)，讓交談中的其他參與者參考特定的網站或共用。您可以設定 Lync Server，以封鎖或停用具有特定首碼的超連結 (換句話說，參與者無法只是按一下連結，就被帶往 URI 所指的任何地方；他們必須手動將連結複製並貼入瀏覽器)。

**Remove-CsImFilterConfiguration** Cmdlet 會移除指定之身分識別 (例如特定網站) 的 IM 篩選組態。針對 Global Identity 執行此 Cmdlet 只會將全域組態重設為預設設定。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsImFilterConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsImFilterConfiguration"}

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
<td><p>要移除之組態的唯一識別身分。這將是 Global 或 Site:&lt;網站名稱&gt; (其中 &lt;網站名稱&gt; 表示要套用設定之網站的名稱)。</p>
<p>完整資料類型：Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration 物件。接受管線傳送的 IM 篩選組態物件輸入。

## 傳回類型

移除 Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration 類型的物件。

## 請參閱

#### 其他資源

[New-CsImFilterConfiguration](new-csimfilterconfiguration.md)  
[Set-CsImFilterConfiguration](set-csimfilterconfiguration.md)  
[Get-CsImFilterConfiguration](get-csimfilterconfiguration.md)

