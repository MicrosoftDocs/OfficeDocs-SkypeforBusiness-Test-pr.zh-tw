---
title: Set-CsHostingProvider
TOCTitle: Set-CsHostingProvider
ms:assetid: 709567e3-1af6-4829-b9ce-5f488f9db372
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398532(v=OCS.15)
ms:contentKeyID: 49291271
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsHostingProvider

 

_**上次修改主題的時間：** 2015-03-09_

修改組織目前所使用的主機供應商。主機供應商是第三方組織，可提供立即訊息、目前狀態，以及您要結為同盟之網域相關的服務。主機供應商 (例如 Microsoft Lync Online 2010) 不同於公用提供者 (例如 Yahoo\!、MSN 和 AOL)，其服務對象不是一般大眾。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsHostingProvider [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsHostingProvider [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AutodiscoverUrl <String>] [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-EnabledSharedAddressSpace <$true | $false>] [-Force <SwitchParameter>] [-HostsOCSUsers <$true | $false>] [-IsLocal <$true | $false>] [-SipClientPort <UInt64>] [-VerificationLevel <AlwaysVerifiable | AlwaysUnverifiable | UseSourceVerification>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會修改包含 Identity 為 Fabrikam.com 的主機供應商。在此範例中，VerificationLevel 屬性會設為 AlwaysUnverifiable。

    Set-CsHostingProvider -Identity "Fabrikam.com" -VerificationLevel "AlwaysUnverifiable"

## 範例 2

範例 2 是範例 1 所示之命令的變化；不過，在此範例中所有主機供應商的驗證層級都設為 AlwaysUnverifiable。為達此目的，會先使用 **Get-CsHostingProvider** 傳回設定供組織使用之所有主機供應商的集合。然後再將該集合管線傳送到 **Set-CsHostingProvider**，以修改集合中每一個供應商的 VerificationLevel 屬性。

    Get-CsHostingProvider | Set-CsHostingProvider -VerificationLevel "AlwaysUnverifiable"

## 範例 3

範例 3 會修改分隔網域設定中目前設定供使用的所有主機供應商，使之不再提供分隔網域同盟使用。此範例會先呼叫 **Get-CsHostingProvider**，以傳回所有可用之主機供應商的集合。然後再將該集合管線傳送到 **Where-Object** Cmdlet，以選取符合兩個準則的供應商：1) HostsOCSUsers 屬性等於 True；且 2) EnabledSharedAddressSpace 屬性等於 True。接著將篩選後的集合管線傳送到 **Set-CsHostingProvider**，以將 EnabledSharedAddressSpace 和 HostsOCSUsers 內容設為 False。完成之後，集合內的主機供應商仍會啟用同盟，但無法再用於分隔網域案例中。

    Get-CsHostingProvider | Where-Object {$_.EnabledSharedAddressSpace -eq $True -and $_.HostsOCSUsers -eq $True} | Set-CsHostingProvider -EnabledSharedAddressSpace $False -HostsOCSUsers $False

## 詳細描述

同盟是兩個組織用來建立信任關係的方法，以促進兩個群組之間的溝通。建立同盟後，兩個組織的使用者便可互相傳送立即訊息、訂閱目前狀態通知，並使用如 Microsoft Lync 2013 等 SIP 應用程式互相通訊。Lync Server 允許三種同盟：1) 您組織與其他組織之間的直接同盟；2) 您組織與公用提供者之間的同盟；3) 您組織與第三方主機供應商之間的同盟。

主機供應商是為其他組織提供 SIP 通訊服務的組織；例如 Fabrikam，Inc. 可能為 Contoso、Northwind Traders、Wingtip Toys 的使用者提供主機服務。當您與主機供應商建立同盟關係時，便能夠有效率地與該供應商所託管的任何組織建立同盟關係。例如，如果您與 Fabrikam Hosting 同盟，您的使用者便能夠與 Contoso、Northwind Traders 及 Wingtip Toys 的使用者交換立即訊息和目前狀態的資訊。

主機供應商也用於分割網域案例。在分割網域案例中，您有部分 Lync Server 使用者的帳戶被託管在內部部署中 (亦即被託管在您的 Lync Server 本端實作)。其他使用者的帳戶由第三方主機供應商在外部部署維護。與主機供應商同盟可讓內部部署使用者與外部部署使用者互相通訊。

為了與第三方主機供應商同盟，您必須建立並啟用新的主機供應商(此外，第三方供應商必須與您建立同盟關係)。建立主機供應商後，您可以使用 **Set-CsHostingProvider** Cmdlet 修改該供應商的屬性。例如，您可以使用這個 Cmdlet 變更供應商 Proxy 伺服器的完整網域名稱 (FQDN)，或使用 Cmdlet 變更該供應商的驗證層級。

請注意，如果您的 Edge Server 設定為使用預設路由，而非網域名稱系統 (DNS) 伺服器路由，則您無法與主機供應商同盟。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsHostingProvider** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsHostingProvider"}

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
<td><p><em>AutodiscoverUrl</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>託管 Lync Server 帳戶的主機供應商所使用之自動探索服務的 URL。自動探索服務可讓用戶端應用程式 (例如 Microsoft Lync Mobile) 決定如何存取使用者的主集區等資源。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出網域和主機供應商之間的網路連線是否已啟用。只有將此值設為 True，才能在兩個組織之間交換訊息。預設值為 False。</p></td>
</tr>
<tr class="even">
<td><p><em>EnabledSharedAddressSpace</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若為 True，則指出該主機供應商將用於分隔網域案例中。預設值為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏顯示當執行命令時可能發生的任何非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>HostsOCSUsers</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>此參數若為 True，指出該主機供應商用於裝載 Lync Server 帳戶。若為 False，則指出該提供者裝載其他帳戶類型，例如 Microsoft Exchange Server 帳戶。預設值為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要修改之主機供應商的唯一識別碼。Identity 可能是主機供應商的 FQDN (例如 fabrikam.com)，或是提供服務的公司名稱 (Fabrikam，Inc.)。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>DisplayHostingProvider 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>IsLocal</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>若為 True，則指出主機供應商使用的 Proxy 伺服器被包含在您自己的 Lync Server 拓撲內。預設值為 False。</p></td>
</tr>
<tr class="even">
<td><p><em>SipClientPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt64</p></td>
<td><p>提供者用來與 SIP 用戶端通訊的連接埠；預設值為 443。請注意，根據預設，當您執行 Get-CsHostingProvider Cmdlet 時，不會顯示 SipClientPort。若要顯示 SipClientPort，請使用類似下列的命令：</p>
<p>Get-CsHostingProvider | Select-Object *</p></td>
</tr>
<tr class="odd">
<td><p><em>VerificationLevel</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Edge.VerificationLevelType</p></td>
<td><p>指出傳送至主機供應商或從主機供應商發出之訊息的允許驗證層級。驗證層級必須設為下列其中一個值：</p>
<p>AlwaysVerifiable。指出從主機供應商發出的所有訊息都視為可驗證。這表示從主機供應商所發出的所有訊息都不會被拒絕。</p>
<p>AlwaysUnverifiable。指出從主機供應商發出的所有訊息都視為無法驗證。因此，只有在主機供應商上的使用者也在您的連絡人清單上，才會傳遞訊息。</p>
<p>UseSourceVerification。依賴包含在主機供應商發出之訊息內的驗證層級。如果沒有指定這個層級，訊息會視為無法驗證而被拒絕。</p>
<p>預設值為 AlwaysVerifiable。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayHostingProvider 物件。**Set-CsHostingProvider** 接受主機供應商物件管線傳送的執行個體。

## 傳回類型

**Set-CsHostingProvider** 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayHostingProvider 物件的執行個體。

## 請參閱

#### 其他資源

[Disable-CsHostingProvider](disable-cshostingprovider.md)  
[Enable-CsHostingProvider](enable-cshostingprovider.md)  
[Get-CsHostingProvider](get-cshostingprovider.md)  
[New-CsHostingProvider](new-cshostingprovider.md)  
[Remove-CsHostingProvider](remove-cshostingprovider.md)

