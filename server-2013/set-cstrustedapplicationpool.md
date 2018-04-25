---
title: Set-CsTrustedApplicationPool
TOCTitle: Set-CsTrustedApplicationPool
ms:assetid: 0f42d12b-d09a-41fd-892f-2b7515a35344
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398187(v=OCS.15)
ms:contentKeyID: 49290107
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTrustedApplicationPool

 

_**上次修改主題的時間：** 2015-03-09_

修改包含代管信任之應用程式的電腦的集區。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsTrustedApplicationPool [-Identity <XdsGlobalRelativeIdentity>] [-AppSharingPortCount <UInt16>] [-AppSharingPortStart <UInt16>] [-AudioPortCount <UInt16>] [-AudioPortStart <UInt16>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-OutboundOnly <$true | $false>] [-Registrar <String>] [-RequiresReplication <$true | $false>] [-ThrottleAsServer <$true | $false>] [-TreatAsAuthenticated <$true | $false>] [-VideoPortCount <UInt16>] [-VideoPortStart <UInt16>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會修改 FQDN 為 TrustPool.litwareinc.com 的集區。我們使用 Identity 參數來指定要修改之集區的 FQDN。此範例會透過針對 OutboundOnly 參數指定 True ($True) 的值，修改集區的 OutboundOnly 屬性 (預設值為 False)。

    Set-CsTrustedApplicationPool -Identity TrustPool.litwareinc.com -OutboundOnly $True

## 詳細描述

我們建議您應該將 Lync Server 部署內執行信任的應用程式的電腦，新增至信任的應用程式專用的集區。不過，您也可以將信任的應用程式電腦新增至用於其他用途的現有集區。**Set-CsTrustedApplicationPool** Cmdlet 會修改現有信任的應用程式集區的設定。請注意，您無法使用這個 Cmdlet 修改與集區相關聯的電腦，您必須使用 CsTrustedApplicationComputer Cmdlet 來執行此工作。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsTrustedApplicationPool** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsTrustedApplicationPool"}

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
<td><p><em>AppSharingPortCount</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>應用程式共用連線的連接埠範圍中可用的連接埠號碼。</p></td>
</tr>
<tr class="even">
<td><p><em>AppSharingPortStart</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>應用程式共用連線可用之連接埠範圍中的第一個連接埠號碼。</p></td>
</tr>
<tr class="odd">
<td><p><em>AudioPortCount</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>音訊連線的連接埠範圍中可用的連接埠號碼。</p></td>
</tr>
<tr class="even">
<td><p><em>AudioPortStart</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>音訊連線可用之連接埠範圍中的第一個連接埠號碼。</p></td>
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
<td><p>隱藏變更前所顯示的確認提示。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要修改其設定之集區的完整網域名稱 (FQDN) 或服務 ID。</p></td>
</tr>
<tr class="even">
<td><p><em>OutboundOnly</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指定信任的應用程式是否可以起始與集區中伺服器的連線。如果您希望所有連線都是由伺服器 (而非應用程式) 起始，請將此值設為 True。</p></td>
</tr>
<tr class="odd">
<td><p><em>Registrar</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>集區之登錄程式服務的服務 ID 或 FQDN。請注意，變更登錄器會造成附加至應用程式的任何連絡人變成孤立。必須呼叫 <strong>Move-CsApplicationEndpoint</strong> Cmdlet 來移動這些連絡人。</p></td>
</tr>
<tr class="even">
<td><p><em>RequiresReplication</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>決定此集區是否需要複寫。如果不需要複寫，請將此值設為 False。若是 Microsoft Outlook Web Access 和手動佈建的應用程式，通常會將此參數設為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>ThrottleAsServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>將此參數設為 False 可針對集區中的伺服器以及當做用戶端之信任的應用程式之間的連線進行節流。這比預設的 True 對連線使用更大的限制；若值為 True，則會以伺服器方式對連線進行節流。連線節流只是限制可同時發生的異動數目。</p></td>
</tr>
<tr class="even">
<td><p><em>TreatAsAuthenticated</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>針對連線到集區中伺服器的信任的應用程式，決定是否需要驗證。如果您需要驗證信任的應用程式，請將此參數設為 False。預設值 True 可讓信任的應用程式在已獲得驗證的假設情況下進行連線。</p></td>
</tr>
<tr class="odd">
<td><p><em>VideoPortCount</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>視訊連線的連接埠範圍中可用的連接埠號碼。</p></td>
</tr>
<tr class="even">
<td><p><em>VideoPortStart</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>視訊連線可用之連接埠範圍中的第一個連接埠號碼。</p></td>
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

Microsoft.Rtc.Management.Xds.DisplayExternalServer 物件。接受管線傳送的受信任應用程式集區物件輸入。

## 傳回類型

此 Cmdlet 不會傳回值，而會修改 Microsoft.Rtc.Management.Xds.DisplayExternalServer 類型的物件。

## 請參閱

#### 其他資源

[New-CsTrustedApplicationPool](new-cstrustedapplicationpool.md)  
[Remove-CsTrustedApplicationPool](remove-cstrustedapplicationpool.md)  
[Get-CsTrustedApplicationPool](get-cstrustedapplicationpool.md)  
[New-CsTrustedApplicationComputer](new-cstrustedapplicationcomputer.md)

