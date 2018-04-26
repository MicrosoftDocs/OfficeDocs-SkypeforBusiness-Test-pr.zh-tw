---
title: Set-CsUserServer
TOCTitle: Set-CsUserServer
ms:assetid: f4dd845a-5c78-4455-93eb-722b603ff154
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413026(v=OCS.15)
ms:contentKeyID: 49292820
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsUserServer

 

_**上次修改主題的時間：** 2015-03-09_

可讓您修改現有的 User Services 集區。User Services 集區可以提供目前狀態資訊及協助管理會議。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsUserServer [-Identity <XdsGlobalRelativeIdentity>] [-ConfDirManagementWcfTcpPort <UInt16>] [-ConferenceServer <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-McuFactorySipPort <UInt16>] [-UserDatabase <String>] [-UserPinManagementWcfHttpPort <UInt16>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會變更單一 User Services 集區的 McuFactorySipPort：Identity 為 UserServer:atl-cs-001.litwareinc.com 的集區。在此範例中，連接埠會變更為 445。

    Set-CsUserServer -Identity "UserServer:atl-cs-001.litwareinc.com" -McuFactorySipPort 445

## 範例 2

範例 2 所示的命令是範例 1 所示命令的變化；不過，在此例中，會針對組織中的所有「使用者服務」集區修改 McuFactorySipPort。為達成此目的，命令會先使用 **Get-CsService** Cmdlet 搭配 UserServer 參數，來傳回目前所使用的所有「使用者服務」集區的集合。然後，此集合會管線傳送到 **ForEach-Object** Cmdlet，它會取得集合中的每個集區，並將 McuFactorySipPort 設定為 445。由於 **Set-CsUserServer** Cmdlet 無法接受本身的管線資料，因此必須將資料管線傳送到 **ForEach-Object** Cmdlet。

    Get-CsService -UserServer | ForEach-Object {Set-CsUserServer -Identity $_.Identity -McuFactorySipPort 445}

## 詳細描述

User Services 是一個全部擷取元件，可執行許多關鍵 Lync Server 角色，例如，User Services 可以提供目前狀態資訊、協助管理會議 (透過「會議狀態」和「會議排程」)、處理使用者授權和使用者層級的路由，以及提供服務以做為後端資料庫的主要介面。User Services 也可協助佈建使用者帳戶。

基於此因素，對於使用者而言，確實瞭解 User Services 集區已設定且可視需要修改這些設定，是非常重要的。您可以利用下列命令擷取 User Services 集區的資訊：

Get-CsService -UserServer

同樣地，也可以使用 **Set-CsUserServer** Cmdlet 進行這其中任何集區的變更。**Set-CsUserServer** Cmdlet 讓系統管理員變更使用者資料庫和/或與集區相關聯的會議伺服器。此 Cmdlet 也可以讓您修改用來與「會議排程」連線的連接埠。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsUserServer** Cmdlet：RTCUniversalServerAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsUserServer"}

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
<td><p><em>ConfDirManagementWcfTcpPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>用於管理會議目錄的 Windows Communication Foundation (WCF) 連接埠。預設值為 9001。</p></td>
</tr>
<tr class="even">
<td><p><em>ConferenceServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>與 User Services 集區相關聯之會議伺服器的服務識別碼。例如：-ConferenceServer &quot;ConferenceServer:atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
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
<td><p>要修改之 User Services 集區的唯一識別碼。例如：-Identity &quot;UserServer:atl-cs-001.litwareinc.com&quot;。</p>
<p>請注意，您可以省略首碼 &quot;UserServer&quot;：指定使用者伺服器時。例如：-Identity &quot;atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>McuFactorySipPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>用來連線至「會議排程」(McuFactory) 的連接埠。「會議排程」會配置媒體控制項單位 (MCU)，以便將特定的媒體類型 (例如音訊) 新增至會議。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserDatabase</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>與 User Services 集區相關聯之使用者資料庫的服務 ID。例如：-UserDatabase &quot;UserDatabase:atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>UserPinManagementWcfHttpPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>Windows Communication Foundation (WCF) 用來管理使用者 PIN 的連接埠。預設值為 443。</p></td>
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

無。**Set-CsUserServer** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Set-CsUserServer** Cmdlet 不會傳回任何物件或值。而是此 Cmdlet 會修改 Microsoft.Rtc.Management.Xds.DisplayUserServer 物件的現有執行個體。

## 請參閱

#### 其他資源

[Get-CsService](get-csservice.md)

