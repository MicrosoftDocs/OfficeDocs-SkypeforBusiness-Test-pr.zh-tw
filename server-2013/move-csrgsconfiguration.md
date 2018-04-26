---
title: Move-CsRgsConfiguration
TOCTitle: Move-CsRgsConfiguration
ms:assetid: 983eadb8-baee-41ba-bba4-2f2b01471250
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398782(v=OCS.15)
ms:contentKeyID: 49291742
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Move-CsRgsConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

可讓您將回應群組組態設定從 Microsoft Office Communications Server 2007 R2 或 Microsoft Lync Server 2010 移轉至 Microsoft Lync Server 2013。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Move-CsRgsConfiguration -Destination <String> -Source <String> [-Force <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會將回應群組應用程式從 atl-ocsrgs-001.litwareinc.com 移轉至 redmond-lyncrgs-001.litwareinc.com。

    Move-CsRgsConfiguration -Source atl-ocsrgs-001.litwareinc.com -Destination redmond-lyncrgs-001.litwareinc.com 

## 詳細描述

回應群組應用程式 能讓您將來電自動路由傳送到如服務台或客戶支援專線等實體。當某人撥打指定的電話號碼，可將該來電自動路由傳送到回應群組代理的適當集。或者，來電可能會路由傳送到互動語音回應 (IVR) 佇列。在該佇列中，系統會詢問來電者一系列問題 (例如「您是否為了現有訂單來電？」)，然後依據這些問題的回答給予要求的資訊，或路由傳送到回應群組代理。

如果您目前在 Office Communications Server 2007 R2 或 Lync Server 2010 上執行回應群組應用程式，**Move-CsRgsConfiguration** Cmdlet 可提供您將此服務移轉至 Lync Server 2013的方法。若要移轉服務，您需要呼叫 **Move-CsRgsConfiguration** Cmdlet，並指定：1) 回應群組應用程式現有版本 (來源) 的完整網域名稱 (FQDN)；以及 2) 新版 Lync Server 2013服務 (目的地) 的 FQDN。然後 **Move-CsRgsConfiguration** 會將所有組態設定、音訊檔和連絡人物件從現有版本 (Office Communications Server 2007 R2 或 Lync Server 2010) 移動到 Lync Server 2013。移轉服務之後，所有對回應群組電話號碼的來電都會由 Lync Server 2013處理。來電將不再由舊版服務處理。

您必須先安裝 Windows Management Instrumentation (WMI) 回溯相容性介面套件，才能執行 **Move-CsRgsConfiguration**；執行 OCSWMIBC.msi 即可安裝此應用程式。您可以在安裝 DVD 的 Setup 資料夾中找到檔案 OCSWMIBC.msi。

如果 Office Communications Server 2007 正在執行 Microsoft SQL Server 2005，則在嘗試遷移回應群組應用程式之前，您必須先在執行 **Move-CsRgsConfiguration** Cmdlet 的電腦上安裝 Microsoft SQL Server 2005 Native Client。如果未安裝 Native Client，當您呼叫 **Move-CsRgsConfiguration** 時，會收到錯誤訊息 \[無法存取 WMI 設定\]。

**Move-CsRgsConfiguration** Cmdlet 只能用來從 Office Communications Server 2007 R2 或 Lync Server 2010 移轉至 Lync Server 2013；您無法使用此 Cmdlet 從某個 Lync Server 2013執行個體移轉至新的 Lync Server 2013執行個體。這種移轉類型只能使用新的 **Import-CsRgsConfiguration** 及 **Export-CsRgsConfiguration** Cmdlet 來執行。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Move-CsRgsConfiguration** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Move-CsRgsConfiguration"}

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
<td><p><em>Destination</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>主控 Lync Server 2013 回應群組應用程式之電腦 (「複製到」位置) 的 FQDN。</p></td>
</tr>
<tr class="even">
<td><p><em>Source</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>目前主控 Office Communications Server 2007 R2 或 Lync Server 2010回應群組應用程式之集區的 FQDN (「複製自」位置)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Move-CsRgsConfiguration** 不接受管線傳送的輸入。

## 傳回類型

**Move-CsRgsConfiguration** 可以在服務之間移動 Microsoft.Rtc.Management.WritableSettings.ServiceSettings 的執行個體。

## 請參閱

#### 其他資源

[Get-CsRgsConfiguration](get-csrgsconfiguration.md)  
[Move-CsRgsConfiguration](move-csrgsconfiguration.md)

