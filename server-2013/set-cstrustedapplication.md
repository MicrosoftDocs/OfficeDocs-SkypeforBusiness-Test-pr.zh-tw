---
title: Set-CsTrustedApplication
TOCTitle: Set-CsTrustedApplication
ms:assetid: 35b2812b-43da-4a0a-88dc-960f3cab0dfc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425840(v=OCS.15)
ms:contentKeyID: 49290561
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTrustedApplication

 

_**上次修改主題的時間：** 2015-03-09_

修改信任之應用程式的設定。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsTrustedApplication [-Identity <ExternalApplicationIdentity>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Port <Int32>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會將 Identity 為 TrustPool.litwareinc.com/tapp2 之信任的應用程式的連接埠修改為連接埠 6200。這可以透過將 Identity TrustPool.litwareinc.com/tapp2 傳遞給 **Set-CsTrustedApplication** Cmdlet 完成。此 Identity 是由應用程式所在之集區的名稱，後面緊接著應用程式名稱 (或識別碼) 所組成。接著，我們會加上 Port 參數，將其值指定為 6200 以修改該值。

    Set-CsTrustedApplication -Identity TrustPool.litwareinc.com/tapp2 -Port 6200

## 詳細描述

信任的應用程式是由第三方開發的應用程式，具備做為 Lync Server 之一部分來執行的信任狀態，但不是產品的內建部分。此 Cmdlet 可讓您修改執行應用程式之外部服務所使用的連接埠號碼。

當您使用此 Cmdlet 修改信任的應用程式時，必須提供 Identity 參數的值。Identity 是應用程式所在之集區的完整網域名稱 (FQDN)，後面緊接著正斜線 (/) 和應用程式識別碼。例如 TrustPool.litwareinc.com/tapp2，其中 TrustPool.litwareinc.com 是集區 FQDN，而 tapp2 是應用程式識別碼。請注意，如果您透過呼叫 **Get-CsTrustedApplication** Cmdlet 來檢視現有的應用程式，您看到的識別碼會類似如下：TrustPool.litwareinc.com/urn:application:tapp2。請注意應用程式名稱 (tapp2) 之前的首碼 urn:application:。由於此首碼是 Identity 的一部分，因此當您指定 Identity 參數的值時，不需要此首碼。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsTrustedApplication** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –matches "Set-CsTrustedApplication\\b"}

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
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.ExternalApplicationIdentity</p></td>
<td><p>您要修改之信任的應用程式的唯一識別碼。Identity 值必須以 &lt;集區 FQDN&gt;/&lt;應用程式識別碼&gt; 格式輸入，其中「集區 FQDN」是應用程式所在之集區的 FQDN，而「應用程式識別碼」是應用程式的名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>Port</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int32</p></td>
<td><p>將會執行應用程式的連接埠號碼。</p></td>
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

Microsoft.Rtc.Management.Xds.DisplayTrustedApplication 物件。接受管線傳送的受信任應用程式物件輸入。

## 傳回類型

這個 Cmdlet 不會傳回值，而會修改 Microsoft.Rtc.Management.Xds.DisplayTrustedApplication 類型的物件。

## 請參閱

#### 其他資源

[New-CsTrustedApplication](new-cstrustedapplication.md)  
[Remove-CsTrustedApplication](remove-cstrustedapplication.md)  
[Get-CsTrustedApplication](get-cstrustedapplication.md)

