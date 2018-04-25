---
title: Debug-CsLisConfiguration
TOCTitle: Debug-CsLisConfiguration
ms:assetid: 8cc718d6-52ec-4ff3-a77e-8d6df1725fb0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398710(v=OCS.15)
ms:contentKeyID: 49291616
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Debug-CsLisConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

以 XML 格式顯示增強型 9-1-1 (E9-1-1) 位置資訊伺服器 (LIS) 組態。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Debug-CsLisConfiguration [-Force <SwitchParameter>] [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

執行此命令將會在 Lync Server 管理命令介面視窗中，以 XML 格式顯示整個 LIS 組態。根據預設，**Debug-CsLisConfiguration** Cmdlet 的輸出會顯示為一行，其中該行結尾的省略符號 (…) 表示有一行以上的資料。因此在此範例中，我們將輸出管線傳送到 **Format-Table** Cmdlet，並指定 Wrap 參數，讓完整輸出可以換行以符合顯示視窗。

    Debug-CsLisConfiguration | Format-Table -Wrap

## 詳細描述

Enterprise Voice E9-1-1 實作的 LIS 組態會以壓縮格式儲存。此 Cmdlet 會解壓縮該組態，並將其以 XML 格式顯示。此功能可以更快速地偵錯組態問題。

此 Cmdlet 會從中央管理存放區擷取位置資訊。建立此資訊時，此資訊會儲存在位置資料庫中；在使用 **Publish-CsLisConfiguration** Cmdlet 發佈該資訊之前，它不會移至中央管理存放區。如果尚未發佈位置資訊 (或已使用 **Unpublish-CsLisConfiguration** Cmdlet 解除發佈)，**Debug-CsLisConfiguration** Cmdlet 就不會傳回任何結果。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Debug-CsLisConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Debug-CsLisConfiguration"}

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
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="even">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>可讓您指定網域控制站。若未指定網域控制站，則會使用第一個可用的網域控制站。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

傳回 System.Management.Automation.PSCustomObject 類型的物件。

## 請參閱

#### 其他資源

[Publish-CsLisConfiguration](publish-cslisconfiguration.md)  
[Unpublish-CsLisConfiguration](unpublish-cslisconfiguration.md)  
[Import-CsLisConfiguration](import-cslisconfiguration.md)  
[Export-CsLisConfiguration](export-cslisconfiguration.md)  
[Test-CsLisConfiguration](test-cslisconfiguration.md)

