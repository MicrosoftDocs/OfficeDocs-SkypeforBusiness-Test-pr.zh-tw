---
title: Disable-CsHostingProvider
TOCTitle: Disable-CsHostingProvider
ms:assetid: 67d67111-aa04-4241-8f41-e8059fd1649c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398481(v=OCS.15)
ms:contentKeyID: 49291179
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Disable-CsHostingProvider

 

_**上次修改主題的時間：** 2015-03-09_

停用組織目前所使用的主機供應商。主機供應商是第三方組織，可提供立即訊息、目前狀態，以及您要結為同盟之網域相關的服務。主機供應商 (例如 Microsoft Lync Online 2010) 不同於公用提供者 (例如 Yahoo\!、MSN 和 AOL)，其服務對象不是一般大眾。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Disable-CsHostingProvider [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Disable-CsHostingProvider [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會停用主機供應商 Fabrikam.com。請注意，如果已經停用 Fabrikam.com，此命令將會傳回錯誤訊息。

    Disable-CsHostingProvider -Identity "Fabrikam.com"

## 範例 2

範例 2 會停用目前已啟用的所有主機供應商。為達成此目的，命令會先呼叫 **Get-CsHostingProvider** Cmdlet 傳回設定供組織使用之所有主機供應商的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 Enabled 屬性等於 True 的供應商。接著將篩選後的集合管線傳送到 **Disable-CsHostingProvider** Cmdlet，以停用集合中的每個供應商。

    Get-CsHostingProvider | Where-Object {$_.Enabled -eq $True} | Disable-CsHostingProvider

## 範例 3

範例 3 會停用所有已啟用且驗證層級不等於 AlwaysVerifiable 的主機供應商。為了執行此工作，命令會先使用 **Get-CsHostingProvider** Cmdlet 傳回設定供組織使用之所有主機供應商的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取符合下列兩個條件的供應商：1) VerificationLevel 屬性不等於 AlwaysVerifiable；且 2) Enabled 屬性等於 True。接著將篩選後的集合管線傳送到 **Disable-CsHostingProvider** Cmdlet，以停用集合中的每個供應商。

    Get-CsHostingProvider | Where-Object {$_.VerificationLevel -ne "AlwaysVerifiable" -and $_.Enabled -eq $True} | Disable-CsHostingProvider

## 詳細描述

「同盟」是兩個組織可建立信任關係的一種方法，此信任關係會簡化兩個團體之間的通訊。建立同盟後，兩個組織的使用者便可互相傳送立即訊息、訂閱目前狀態通知，並使用如 Lync 2013 等 SIP 應用程式互相通訊。Lync Server 允許三種同盟：1) 您的組織與其他組織之間的直接同盟；2) 您的組織與公用提供者之間的同盟；以及 3) 您的組織與第三方主機供應商之間的同盟。

主機供應商是為其他組織提供 SIP 通訊服務的組織；例如 Fabrikam, Inc. 可能為 Contoso、Northwind Traders、Wingtip Toys 的使用者提供主機服務。當您與主機供應商建立同盟關係時，實際上是與由該供應商提供主機服務的任何組織建立同盟。例如，如果您與 Fabrikam Hosting 同盟，您的使用者便能夠與 Contoso、Northwind Traders 及 Wingtip Toys 的使用者交換立即訊息和目前狀態的資訊。

主機供應商也可以用於分割網域案例。在分割網域案例中，您的部分 Lync Server 使用者擁有內部部署之主機上的帳戶 (也就是主機位於您的 Lync Server 本機實作上)。其他使用者的帳戶由第三方主機供應商在外部部署維護。與主機供應商同盟可讓內部部署使用者與外部部署使用者互相通訊。

若要與第三方主機供應商同盟，您必須建立並啟用新的主機供應商 (此外，該第三方供應商也必須與您建立同盟關係)。您可以在建立主機供應商時啟用該供應商；或者，也可以事後使用 **Enable-CsHostingProvider** Cmdlet 來啟用該供應商。此外，您隨時可以使用 **Disable-CsHostingProvider** Cmdlet 停用關係。當您停用主機供應商時，該供應商仍保留有效的同盟協力廠商；不過，您組織與該供應商之間的所有通訊活動將會擱置，直到重新啟用供應商為止。

請注意，如果您的 Edge Server 設定為使用預設路由，而非網域名稱系統 (DNS) 伺服器路由，則您無法與主機供應商同盟。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Disable-CsHostingProvider** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Disable-CsHostingProvider"}

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
<td><p>要停用之主機供應商的唯一識別碼。Identity 可能是主機供應商的完整網域 (FQDN) 名稱 (例如 fabrikam.com)，或者可能是提供服務的公司名稱 (Fabrikam, Inc.)。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>DisplayHostingProvider 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayHostingProvider 物件。**Disable-CsHostingProvider** Cmdlet 會接受管線傳送的主機供應商物件執行個體。

## 傳回類型

無。反之，此 Cmdlet 會停用 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayHostingProvider 物件的執行個體。

## 請參閱

#### 其他資源

[Enable-CsHostingProvider](enable-cshostingprovider.md)  
[Get-CsHostingProvider](get-cshostingprovider.md)  
[New-CsHostingProvider](new-cshostingprovider.md)  
[Remove-CsHostingProvider](remove-cshostingprovider.md)  
[Set-CsHostingProvider](set-cshostingprovider.md)

