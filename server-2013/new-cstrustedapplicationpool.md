---
title: New-CsTrustedApplicationPool
TOCTitle: New-CsTrustedApplicationPool
ms:assetid: 30117225-d82b-494b-8bc2-da5d539bdd6b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425804(v=OCS.15)
ms:contentKeyID: 49290486
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsTrustedApplicationPool

 

_**上次修改主題的時間：** 2015-03-09_

建立新集區，以容納代管信任之應用程式的電腦。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsTrustedApplicationPool -Identity <XdsGlobalRelativeIdentity> [-AppSharingPortCount <UInt16>] [-AppSharingPortStart <UInt16>] [-AudioPortCount <UInt16>] [-AudioPortStart <UInt16>] [-ComputerFqdn <Fqdn>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-OutboundOnly <$true | $false>] [-Registrar <String>] [-RequiresReplication <$true | $false>] [-Site <String>] [-ThrottleAsServer <$true | $false>] [-TreatAsAuthenticated <$true | $false>] [-VideoPortCount <UInt16>] [-VideoPortStart <UInt16>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會建立含有 FQDN TrustPool.litwareinc.com 的新集區。我們使用 Identity 參數來指定新 FQDN。我們使用含有 pool0.litwareinc.com 值的 Registrar 參數，在該 FQDN 上使新集區與登錄器服務產生關聯。最後，我們使用含有 Redmond 值的 Site 參數來指定該集區為 Redmond 網站的一部份。

請注意，儘管 Site 值是 SiteId (可藉由呼叫 **Get-CsSite** Cmdlet 來加以擷取)，不過網站 Identity 將隨著新受信任應用程式集區一併儲存。例如，如果網站的 Identity 為 site:Redmond1 而 SiteId 為 NA，您必須在呼叫 **New-CsTrustedApplicationPool** Cmdlet 時將 NA 當做 Site 參數的值。然而，如果您想要在稍後再尋找 NA 網站的所有受信任應用程式集區，您可以在 Where 子句中使用 Identity 值，如下所示：

Get-CsTrustedApplicationPool | Where-Object {$\_.SiteId –eq "site:Redmond1"}

    New-CsTrustedApplicationPool -Identity TrustPool.litwareinc.com -Registrar pool0.litwareinc.com -Site Redmond

## 範例 2

範例 2 與範例 1 相同，除了它不指定登錄器服務的 FQDN，而是使用服務識別碼 Registrar:redmond.litwareinc.com。此外，我們已為 ComputerFqdn 參數指定了值。建立集區之後，電腦也會建立在該集區內。根據預設，電腦的 FQDN 與集區的 FQDN 相同。我們已為該集區內的電腦指定不同的 FQDN，即 AppServer.litwareinc.com。

    New-CsTrustedApplicationPool -Identity TrustPool.litwareinc.com -Registrar Registrar:redmond.litwareinc.com -Site Redmond -ComputerFqdn AppServer.litwareinc.com

## 詳細描述

建議您應該將 Lync Server 部署內執行信任的應用程式之電腦，新增至信任的應用程式專用的集區。不過，您也可以將信任的應用程式電腦新增至用於其他用途的現有集區。如果集區已經是拓撲的一部分，此 Cmdlet 會建立與該集區相關聯的外部服務 (含 ExternalServer 的服務角色)。如果集區不存在，此 Cmdlet 會建立集區和對應的服務 (您可以透過呼叫 **Get-CsPool** Cmdlet，找到現有集區的清單)。

建立新的信任的應用程式集區 (新外部服務) 還會建立指派給該集區之新的信任的應用程式電腦。根據預設，會指派與集區相同的完整網域名稱 (FQDN) 給電腦。不過，您可以使用這個 Cmdlet 的 ComputerFqdn 參數，指定您自己的 FQDN 值。如果您計畫新增更多電腦至集區，則必須指定與集區 FQDN 不同的 ComputerFqdn 值。若要新增更多電腦至集區，請呼叫 **New-CsTrustedApplicationComputer** Cmdlet。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsTrustedApplicationPool** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsTrustedApplicationPool"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>新集區的 FQDN。請注意，用於建立集區的 Identity 值是集區 FQDN，做為 Identity 與新集區一起儲存的值實際上是集區自動產生的服務 ID。此處輸入的 Identity 會儲存為 PoolFqdn。</p></td>
</tr>
<tr class="even">
<td><p><em>AppSharingPortCount</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>連接埠範圍中可用於應用程式共用連線的連接埠數目。</p>
<p>預設值：0</p></td>
</tr>
<tr class="odd">
<td><p><em>AppSharingPortStart</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>連接埠範圍中可用於應用程式共用連線的第一個連接埠號碼。</p></td>
</tr>
<tr class="even">
<td><p><em>AudioPortCount</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>連接埠範圍中可用於音訊連線的連接埠數目。</p>
<p>預設值：0</p></td>
</tr>
<tr class="odd">
<td><p><em>AudioPortStart</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>連接埠範圍中可用於音訊連線的第一個連接埠號碼。</p></td>
</tr>
<tr class="even">
<td><p><em>ComputerFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>建立信任的應用程式集區會自動建立屬於該集區之信任的應用程式電腦。根據預設，電腦會接收與集區相同的 FQDN。在此參數中輸入值，以指定與集區 FQDN 不同之電腦的 FQDN。如果您計畫新增更多電腦至集區，您必須輸入與集區 FQDN 不同的參數值。</p></td>
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
<td><p><em>OutboundOnly</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指定信任的應用程式是否可以起始連線至集區內的伺服器如果您希望由伺服器而非由應用程式起始所有連線，請將這個值設為 True。</p>
<p>預設值：False</p></td>
</tr>
<tr class="even">
<td><p><em>Registrar</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>集區之登錄器服務的服務 ID 或 FQDN。</p>
<p>請注意，雖然這是選用選項，但如果您嘗試建立新的信任的應用程式端點 (使用 <strong>New-CsTrustedApplicationEndpoint</strong> Cmdlet)，並指派端點至沒有登錄器相依性的集區，則您會收到錯誤，且無法建立端點。此外，您無法移除與登錄器無關之信任的應用程式集區。</p></td>
</tr>
<tr class="odd">
<td><p><em>RequiresReplication</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>決定此集區是否需要複寫。如果不需要複寫，請將這個值設為 False。若是 Microsoft Outlook Web Access 和手動佈建的應用程式，通常會將此參數設為 False。</p>
<p>預設值：True</p></td>
</tr>
<tr class="even">
<td><p><em>Site</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此集區所在之網站的網站識別碼。呼叫 <strong>Get-CsSite</strong> Cmdlet 以擷取網站的 SiteId 內容。請記住，您必須使用 SiteId 內容，而不是網站的 Identity。另外，請勿在 SiteId 前加上“site:”字串，只要輸入 SiteId 即可。除此之外，雖然您已經輸入從 <strong>Get-CsSite</strong> Cmdlet 擷取的 SiteId，不過新受信任應用程式集區的 SiteId 內容將含有網站 Identity。例如，如果網站的 SiteId 為 Main 而網站 Identity 為 site:Redmond1，您必須在呼叫 <strong>New-CsTrustedApplicationPool</strong> Cmdlet 時輸入 -Site Main，不過後續的 <strong>Get-CsTrustedApplicationPool</strong> Cmdlet 呼叫會將 SiteId 顯示為 site:Redmond1。</p>
<p>如果在 Identity 中指定的集區已存在，則您不需要指定網站。如果集區不存在，則需要此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>ThrottleAsServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設定此參數為 False，將集區內的伺服器和信任的應用程式之間的連線節流為用戶端。相較於將連線節流為伺服器的預設值 True，這樣的連線限制更多。連線節流會限制可同時發生的交易數目。</p>
<p>預設值：True</p></td>
</tr>
<tr class="even">
<td><p><em>TreatAsAuthenticated</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>決定集區內連線至伺服器之信任的應用程式是否需要驗證。如果信任的應用程式需要驗證，請將此參數設為 False。預設值 True 允許信任的應用程式在已驗證的假設下連線。</p>
<p>預設值：True</p></td>
</tr>
<tr class="odd">
<td><p><em>VideoPortCount</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>連接埠範圍中可用於視訊連線的連接埠數目。</p>
<p>預設值：0</p></td>
</tr>
<tr class="even">
<td><p><em>VideoPortStart</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>連接埠範圍中可用於視訊連線的第一個連接埠號碼。</p></td>
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

建立 Microsoft.Rtc.Management.Xds.DisplayExternalServer 類型的物件。

## 請參閱

#### 其他資源

[Remove-CsTrustedApplicationPool](remove-cstrustedapplicationpool.md)  
[Set-CsTrustedApplicationPool](set-cstrustedapplicationpool.md)  
[Get-CsTrustedApplicationPool](get-cstrustedapplicationpool.md)  
[New-CsTrustedApplicationComputer](new-cstrustedapplicationcomputer.md)  
[Get-CsSite](get-cssite.md)

