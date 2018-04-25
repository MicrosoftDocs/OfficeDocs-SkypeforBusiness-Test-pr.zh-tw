---
title: New-CsHostingProvider
TOCTitle: New-CsHostingProvider
ms:assetid: 6874cc14-d250-43d4-8868-43cd8d202e9c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398490(v=OCS.15)
ms:contentKeyID: 49291181
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsHostingProvider

 

_**上次修改主題的時間：** 2015-03-09_

建立供組織使用的新主機供應商。主機供應商是第三方組織，可提供立即訊息、目前狀態，以及您要結為同盟之網域相關的服務。主機供應商 (例如 Microsoft Lync Online 2010) 不同於公用提供者 (例如 Yahoo\!、MSN 和 AOL)，其服務對象不是一般大眾。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsHostingProvider -Enabled <$true | $false> -Identity <XdsGlobalRelativeIdentity> -ProxyFqdn <String> [-AutodiscoverUrl <String>] [-IsLocal <$true | $false>] [-SipClientPort <UInt64>] [-VerificationLevel <AlwaysVerifiable | AlwaysUnverifiable | UseSourceVerification>] <COMMON PARAMETERS>

    New-CsHostingProvider -Enabled <$true | $false> -EnabledSharedAddressSpace <$true | $false> -HostsOCSUsers <$true | $false> -Identity <XdsGlobalRelativeIdentity> -ProxyFqdn <String> [-AutodiscoverUrl <String>] [-IsLocal <$true | $false>] [-SipClientPort <UInt64>] [-VerificationLevel <AlwaysVerifiable | AlwaysUnverifiable | UseSourceVerification>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會建立 Identity 為 Fabrikam.com 的新主機供應商。除了指定 Identity，命令還包含了其他兩個必要參數：ProxyFqdn (指定 Fabrikam.com 使用的 Proxy 伺服器) 和 Enabled (指出是否啟用新主機供應商以供使用)。如果您省略任何必要參數，**New-CsHostingProvider** Cmdlet 在繼續進行前會提示您輸入那些值。

    New-CsHostingProvider -Identity Fabrikam.com -ProxyFqdn "proxyserver.fabrikam.com" -Enabled $True

## 範例 2

範例 2 示範如何建立用於分隔網域案例的新主機供應商(分隔網域表示您的某些 Lync Server 帳戶為內部維護，而其他帳戶則是由主機供應商維護)。若要建立這種類型的主機供應商，您必須包含三種必要參數 (Identity、ProxyFQDN 和 Enabled)。此外，您必須同時包含 HostsOCSUsers 和 EnabledSharedAddressSpace 參數，並將它們都設為 True。若要建立主控非 Lync Server 服務 (例如 Microsoft Exchange) 的分隔網域供應商，請同樣包含這兩個參數，但將 HostsOCSUsers 設為 False。

    New-CsHostingProvider -Identity Fabrikam.com -ProxyFqdn "proxyserver.fabrikam.com" -Enabled $True -HostsOCSUsers $True -EnabledSharedAddressSpace $True

## 詳細描述

「同盟」是兩個組織可建立信任關係的一種方法，此信任關係會簡化兩個團體之間的通訊。建立同盟後，兩個組織的使用者便可互相傳送立即訊息、訂閱目前狀態通知，並使用如 Lync 2013 等 SIP 應用程式互相通訊。Lync Server 允許三種同盟：1) 您的組織與其他組織之間的直接同盟；2) 您的組織與公用提供者之間的同盟；以及 3) 您的組織與第三方主機供應商之間的同盟。

主機供應商是為其他組織提供 SIP 通訊服務的組織；例如 Fabrikam, Inc. 可能託管 Contoso、Northwind Traders、Wingtip Toys 等組織的使用者。當您與主機供應商建立同盟關係時，便能夠有效率地與該供應商所託管的任何組織建立同盟關係。例如，如果您與 Fabrikam Hosting 同盟，您的使用者便能夠與 Contoso、Northwind Traders 及 Wingtip Toys 的使用者交換立即訊息和目前狀態的資訊。

主機供應商也可以用於分割網域案例。在分割網域案例中，您的部分 Lync Server 使用者擁有內部部署之主機上的帳戶 (也就是主機位於您的 Lync Server 本機實作上)。其他使用者的帳戶由第三方主機供應商在外部部署維護。與主機供應商同盟可讓內部部署使用者與外部部署使用者互相通訊。

為了與第三方主機供應商同盟，您必須建立並啟用新的主機供應商。(此外，第三方供應商必須與您建立同盟關係)。**New-CsHostingProvider** Cmdlet 可讓您設定三種類型的主機供應商關係：

直接與主機供應商同盟。若要建立這種類型的關係，您必須包含三個必要參數：Identity、ProxyFQDN 和 Enabled。

分割網域，包含託管的 Lync Server 服務。若要建立這種類型的關係，您必須包含三個必要參數。此外，您必須同時將 EnabledSharedAddressSpace 和 HostsOCSUsers 屬性設為 True。

分隔網域，包含受主控的非 Lync Server 服務 (例如 Microsoft Exchange)。若要建立這種類型的關係，您必須包含三個必要參數。此外，您必須將 EnabledSharedAddressSpace 設為 True，HostsOCSUsers 設為 False。

建立新的主機供應商時，用於該供應商之 Identity 和 Proxy 完整網域名稱 (FQDN) 必須是唯一的：您無法擁有兩個共用 Identity 和/或 Proxy FQDN 的主機供應商 (或即使是一個主機供應商和一個公用供應商)。

另請注意，如果您的 Edge Server 設定為使用預設路由，而非網域名稱系統 (DNS) 伺服器路由，則您無法與主機供應商同盟。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsHostingProvider** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsHostingProvider"}

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
<td><p><em>Enabled</em></p></td>
<td><p>必要</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出網域和主機供應商之間的網路連線是否已啟用。只有將此值設為 True，才能在兩個組織之間交換訊息。預設值為 False。</p></td>
</tr>
<tr class="even">
<td><p><em>EnabledSharedAddressSpace</em></p></td>
<td><p>必要</p></td>
<td><p>System.Boolean</p></td>
<td><p>若為 True，則指出該主機供應商將用於分隔網域案例中。預設值為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>HostsOCSUsers</em></p></td>
<td><p>必要</p></td>
<td><p>System.Boolean</p></td>
<td><p>若為 True，則指出該主機供應商用於託管 Lync Server 帳戶。若為 False，則指出該供應商託管其他帳戶類型，例如 Microsoft Exchange 帳戶。預設值為 False。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要建立之主機供應商的唯一識別碼。Identity 是字串值，它可以是主機供應商的 FQDN (例如 fabrikam.com)，或是提供服務的公司名稱 (Fabrikam, Inc.)。</p>
<p>主機供應商的 Identity 必須是唯一的。如果您嘗試建立的新主機供應商和現有供應商擁有相同的 Identity，則命令會失敗。</p></td>
</tr>
<tr class="odd">
<td><p><em>ProxyFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>主機供應商使用之 Proxy 伺服器的 FQDN。請注意，這個值無法修改。如果主機供應商於稍後變更其 Proxy 伺服器，或是當您在指定 Proxy FQDN 時發生錯誤，則必須刪除該供應商的項目並重新建立。</p></td>
</tr>
<tr class="even">
<td><p><em>AutodiscoverUrl</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>主控 Lync Server 帳戶之主機供應商所使用的自動探索服務 URL。自動探索服務可讓用戶端應用程式決定如何存取資源，如使用者的主集區。</p></td>
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
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="even">
<td><p><em>IsLocal</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若為 True，則指出主機供應商使用的 Proxy 伺服器已包含在您自己的 Lync Server 拓撲內。預設值為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>SipClientPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt64</p></td>
<td><p>供應商用來與 SIP 用戶端通訊的連接埠；預設值為 443。請注意，根據預設，當您執行 <strong>Get-CsHostingProvider</strong> Cmdlet 時，不會顯示 SipClientPort。若要顯示 SipClientPort，請使用類似下列的命令：</p>
<p>Get-CsHostingProvider | Select-Object *</p></td>
</tr>
<tr class="even">
<td><p><em>VerificationLevel</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Edge.VerificationLevelType</p></td>
<td><p>指出傳送至主機供應商或從主機供應商發出之訊息的允許驗證層級。驗證層級必須設為下列其中一個值：</p>
<p>AlwaysVerifiable。指出從主機供應商發出的所有訊息都視為可驗證。這表示從主機供應商所發出的所有訊息都不會被拒絕。</p>
<p>AlwaysUnverifiable。指出從主機供應商發出的所有訊息都視為無法驗證。因此，只有在主機供應商上的使用者也在您的連絡人清單上，才會傳遞訊息。</p>
<p>UseSourceVerification。依賴包含在主機供應商發出之訊息內的驗證層級。如果沒有指定這個層級，訊息會視為無法驗證而被拒絕。</p>
<p>預設值為 AlwayVerifiable。</p></td>
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

無。**New-CsHostingProvider** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

建立 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayHostingProvider 物件的新執行個體。

## 請參閱

#### 其他資源

[Disable-CsHostingProvider](disable-cshostingprovider.md)  
[Enable-CsHostingProvider](enable-cshostingprovider.md)  
[Get-CsHostingProvider](get-cshostingprovider.md)  
[Remove-CsHostingProvider](remove-cshostingprovider.md)  
[Set-CsHostingProvider](set-cshostingprovider.md)

