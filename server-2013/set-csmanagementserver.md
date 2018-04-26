---
title: Set-CsManagementServer
TOCTitle: Set-CsManagementServer
ms:assetid: 6607580d-f111-4dff-961a-71525bf2e482
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398465(v=OCS.15)
ms:contentKeyID: 49291142
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsManagementServer

 

_**上次修改主題的時間：** 2015-03-09_

修改 Lync Server中央管理服務所使用的複寫連接埠。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsManagementServer [-Identity <XdsGlobalRelativeIdentity>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-ReplicationServicePort <UInt16>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會連線到 Identity 為 ManagementServer:atl-cs-001.litwareinc.com 的 中央管理服務，並將複寫服務連接埠設定為連接埠 5076。

    Set-CsManagementServer -Identity "ManagementServer:atl-cs-001.litwareinc.com" -ReplicationServicePort 5076

## 詳細描述

中央管理服務負責複寫 中央管理存放區和執行 Lync Server 服務或擔任伺服器角色之電腦間的資料。 中央管理服務會在一個 前端集區 (或一個 Standard Edition 伺服器) 中運作，以加速整個 Lync Server 基礎結構的複寫作業。

**Set-CsManagementServer** Cmdlet 可讓您指定 中央管理服務 用來複寫的連接埠。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsManagementServer** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsManagementServer"}

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
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>中央管理服務 的唯一識別碼。例如：-Identity &quot;ManagementServer:atl-cs-001.litwareinc.com&quot;。</p>
<p>請注意，您可以省略前置詞 &quot;ManagementServer:&quot;指定 中央管理伺服器時，您可以省略首碼 &quot;MediationServer:&quot;。例如：-Identity &quot;atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>ReplicationServicePort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>中央管理服務 所使用之複寫連接埠的連接埠號碼。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Set-CsManagementServer** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Set-CsManagementServer** Cmdlet 不會傳回任何物件或值，而會修改現有的 Microsoft.Rtc.Management.Xds.DisplayManagementServer 物件執行個體。

## 請參閱

#### 其他資源

[Get-CsService](get-csservice.md)  
[Move-CsManagementServer](move-csmanagementserver.md)

