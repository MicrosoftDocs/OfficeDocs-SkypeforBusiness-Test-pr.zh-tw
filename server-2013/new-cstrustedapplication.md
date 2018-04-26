---
title: New-CsTrustedApplication
TOCTitle: New-CsTrustedApplication
ms:assetid: 1c804a97-f9b5-4c3e-adc6-a120b26c1f51
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398259(v=OCS.15)
ms:contentKeyID: 49290264
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsTrustedApplication

 

_**上次修改主題的時間：** 2015-03-09_

新增信任的應用程式到集區。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsTrustedApplication -ApplicationId <String> -TrustedApplicationPoolFqdn <String> <COMMON PARAMETERS>

    New-CsTrustedApplication [-Identity <ExternalApplicationIdentity>] <COMMON PARAMETERS>

    COMMON PARAMETERS: -Port <Int32> [-Confirm [<SwitchParameter>]] [-EnableTcp <SwitchParameter>] [-Force <SwitchParameter>] [-LegacyApplicationName <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會建立應用程式識別碼為 tapp1 之信任的應用程式。我們使用 TrustedApplicationPoolFqdn 參數指定此應用程式所在之信任的應用程式集區，在此範例中，是 FQDN 為 TrustPool.litwareinc.com 的集區。我們也必須指定應用程式的連接埠；在此範例中，我們使用連接埠 6000。請注意，透過指定 ApplicationId 和 TrustedApplicationPoolFqdn 來執行此 Cmdlet 將會自動產生 Identity，此 Identity 稍後可用來擷取、修改或移除此應用程式。

    New-CsTrustedApplication -ApplicationId tapp1 -TrustedApplicationPoolFqdn TrustPool.litwareinc.com -Port 6000

## 範例 2

此範例會在連接埠 6100 上建立 Identity 為 TrustPool.litwareinc.com/tapp2 的信任的應用程式。請注意 Identity 的格式。此值的格式必須為 \<信任的集區 FQDN\>/\<應用程式識別碼\>。

    New-CsTrustedApplication -Identity TrustPool.litwareinc.com/tapp2 -Port 6100

## 詳細描述

信任的應用程式是由第三方開發的應用程式，只可在執行 Lync Server 時提供信任狀態，但不是內建於產品之中。此 Cmdlet 會將信任的應用程式新增到信任的應用程式集區，並將連接埠指派給執行該應用程式的外部服務。

信任的應用程式必須與可全域路由傳送使用者代理 URI (GRUU) 產生關聯，包括服務 GRUU 及電腦 GRUU。此 Cmdlet 會根據與此應用程式所在位置之集區相關聯的電腦及服務，自動產生這些值。

當您使用此 Cmdlet 建立信任的應用程式時，必須提供 Identity 參數的值或 ApplicationID 及 TrustedApplicationPoolFqdn 參數的值。Identity 就是 TrustedApplicationPoolFqdn 後面緊接著正斜線 (/) 和 ApplicationID。例如 TrustPool.litwareinc.com/tapp2，其中的 TrustPool.litwareinc.com 是 TrustedApplicationPoolFqdn，而 tapp2 則是 ApplicationID。

請注意，當您輸入應用程式識別碼(不論是做為 Identity 參數的一部分或在 ApplicationID 參數中) 時，必須只輸入應用程式名稱。不過，完整的應用程式識別碼將會自動加上字串 urn:application: 做為首碼。例如，如果您輸入值 tapp2 做為 ApplicationID，該 ID 將會儲存為 urn:application:tapp2。同樣地，如果您輸入的 Identity 為 TrustPool.litwareinc.com/tapp2，該 Identity 在系統中將會儲存為 TrustPool.litwareinc.com/urn:application:tapp2。

當您使用此 Cmdlet 指定 Port 值時，此 Cmdlet 不會開啟該連接埠。您必須在 Windows 防火牆和任何公司防火牆中開啟連接埠，才能讓信任的應用程式與防火牆外的網路取得聯繫。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsTrustedApplication** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsTrustedApplication\\b"}

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
<td><p><em>ApplicationId</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>應用程式的名稱。這必須是在 TrustedApplicationPoolFqdn 參數中指定，並且在集區中是唯一的字串。該字串中不能包含空格。如果您提供 ApplicationId 的值，也必須提供 TrustedApplicationPoolFqdn 參數的值。您無法指定 ApplicationId 及 Identity。</p></td>
</tr>
<tr class="even">
<td><p><em>Port</em></p></td>
<td><p>必要</p></td>
<td><p>System.Int32</p></td>
<td><p>將會執行應用程式的連接埠號碼。該連接埠在指定集區中必須是唯一的。換句話說，在指定的集區上無法定義使用這個相同連接埠的其他應用程式。</p></td>
</tr>
<tr class="odd">
<td><p><em>TrustedApplicationPoolFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>應用程式所在之信任應用程式集區的 FQDN。如果您提供 TrustedApplicationPoolFqdn 的值，也必須提供 ApplicationId 的值，但是您無法提供 Identity 參數的值。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableTcp</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>指定信任的應用程式將使用傳輸控制通訊協定 (TCP)。只有在信任的應用程式不是 Microsoft Unified Communications Managed API (UCMA) 應用程式時，才使用此參數。這是因為 UCMA 應用程式僅支援相互傳輸層安全性 (MTLS) 通訊協定。如果您不指定 Force 參數搭配 EnableTcp 參數，將在建立新信任的應用程式之前收到確認提示。</p></td>
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
<td><p>集區中信任之應用程式的唯一識別碼。Identity 值的輸入格式必須為 &lt;集區 FQDN&gt;/&lt;應用程式識別碼&gt;，其中的集區 FQDN 是應用程式所在之集區的完整網域名稱 (FQDN)，而應用程式識別碼則是應用程式名稱。應用程式識別碼在指定集區中必須是唯一的。</p>
<p>如果您輸入 Identity，則無法指定 ApplicationId 或 TrustedApplicationPoolFqdn 參數的值。</p></td>
</tr>
<tr class="even">
<td><p><em>LegacyApplicationName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>只有當應用程式從 Microsoft Office Communications Server 2007 R2 部署遷移時，才使用此參數。此值必須與應用程式 Office Communications Server 2007 R2 版本的 GRUU 類型相同，兩者才能共同運作。</p>
<p>請注意，在大多數情況下，將 ApplicationId 參數設為等於 GRUU 類型，就足以讓應用程式共同運作。不過，如果來自 Office Communications Server 2007 R2 應用程式的 GRUU 類型包含 ApplicationId 中無效的字元，則必須在 LegacyApplicationName 參數中提供該值。</p>
<p>如果您未指定此參數的值，將會自動插入應用程式識別碼的值 (不含 urn:application:首碼)。</p></td>
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

無。

## 傳回類型

建立 Microsoft.Rtc.Management.Xds.DisplayTrustedApplication 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsTrustedApplication](remove-cstrustedapplication.md)  
[Set-CsTrustedApplication](set-cstrustedapplication.md)  
[Get-CsTrustedApplication](get-cstrustedapplication.md)

