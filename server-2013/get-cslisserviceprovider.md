---
title: Get-CsLisServiceProvider
TOCTitle: Get-CsLisServiceProvider
ms:assetid: 060b0b32-5787-487b-b1d9-7a0c7dd44d80
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398116(v=OCS.15)
ms:contentKeyID: 49289972
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsLisServiceProvider

 

_**上次修改主題的時間：** 2015-03-09_

擷取由增強型 9-1-1 (E9-1-1) 網路路由提供者所提供用於驗證位置之 Web 服務的資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsLisServiceProvider

## 範例

## 範例 1

**Get-CsLisServiceProvider** Cmdlet 不接受任何參數 (除非是一般 Windows PowerShell 參數，例如 Verbose)。一個 E9-1-1 實作中絕不會有一個以上的服務提供者，因此，此 Cmdlet 會擷取由該服務提供者所提供之 Web 服務的資訊。

    Get-CsLisServiceProvider

## 詳細描述

在啟用 E9-1-1 的 Enterprise Voice 實作中，系統必須先透過 E9-1-1 網路路由提供者來路由傳送緊急通話，以確保將通話路由傳送至合適的公眾安全回應點 (PSAP) (PSAP 是在美國的一個機構，這個機構會將來電導向至最近的緊急服務，例如警察、消防以及救護車服務)。為了完成這項作業，提供者必須先取得組織周圍的位置清單，然後再比對位置清單和主要街道地址指南中的內容，以確保所有位置的有效性。此 Cmdlet 會擷取提供者的資訊，包括提供者的名稱以及組織將用於傳送位置之 Web 服務的 URL。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsLisServiceProvider** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsLisServiceProvider"}

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
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>此 Cmdlet 只提供一般的 Windows PowerShell 參數。</p></td>
<td><p></p></td>
<td><p></p></td>
<td> </td>
</tr>
</tbody>
</table>


## 輸入類型

無。

## 傳回類型

此 Cmdlet 會擷取 System.Management.Automation.PSCustomObject 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsLisServiceProvider](remove-cslisserviceprovider.md)  
[Set-CsLisServiceProvider](set-cslisserviceprovider.md)

