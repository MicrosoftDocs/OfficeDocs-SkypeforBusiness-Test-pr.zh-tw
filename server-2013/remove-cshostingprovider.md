---
title: Remove-CsHostingProvider
TOCTitle: Remove-CsHostingProvider
ms:assetid: 309e472b-683c-47ed-9536-3b7aa50119d2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425809(v=OCS.15)
ms:contentKeyID: 49290495
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsHostingProvider

 

_**上次修改主題的時間：** 2015-03-09_

移除組織目前所使用的一或多個主機供應商。主機供應商是第三方組織，可提供立即訊息、目前狀態，以及您要結為同盟之網域相關的服務。主機供應商 (如 Microsoft Lync Online 2010) 與公用提供者 (例如 Yahoo\!、MSN 與 AOL) 不同，其服務對象不是一般大眾。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsHostingProvider -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會顯示 Identity 為 Fabrikam.com 的主機供應商。在刪除該主機供應商後，與 Fabrikam.com (以及任何與 Fabrikam.com 關聯的網域) 之間的同盟將會終止。

    Remove-CsHostingProvider -Identity "Fabrikam.com"

## 範例 2

範例 2 會刪除所有設定供組織使用的主機供應商。為達成此目的，命令會先使用 **Get-CsHostingProvider** Cmdlet 傳回目前所使用之所有主機供應商的集合。然後，此集合會管線傳送到 **Remove-CsHostingProvider** Cmdlet，以刪除集合中的每一個項目。當此命令完成時，便不再有任何設定使用的主機供應商。

    Get-CsHostingProvider | Remove-CsHostingProvider

## 範例 3

範例 3 會刪除任何在提供者 Identity 的某處有出現 "Fabrikam" 字串值的主機供應商。為了執行此工作，命令會先呼叫 **Get-CsHostingProvider** Cmdlet 搭配 Filter 參數；篩選值 "\*Fabrikam\*" 可將傳回的資料限制在 Identity 包含 "Fabrikam" 的主機供應商，例如 Fabrikam.com、Fabrikam.net 與 FabrikamUsers.com 等等。然後再將篩選後的集合管線傳送到 **Remove-CsHostingProvider** Cmdlet，以刪除集合中的每個項目。

    Get-CsHostingProvider -Filter "*Fabrikam*" | Remove-CsHostingProvider

## 範例 4

在範例 4 中，會刪除所有驗證層級不是設為 AlwaysVerifiable 的主機供應商。作法是先呼叫不含任何額外參數的 **Get-CsHostingProvider** Cmdlet，以傳回所有設定供組織使用之所有主機供應商的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 VerificationLevel 屬性不等於 AlwaysVerifiable 的供應商。接著將篩選後的集合管線傳送到 **Remove-CsHostingProvider** Cmdlet，以移除該篩選過之集合中的每個供應商。

    Get-CsHostingProvider | Where-Object {$_.VerificationLevel -ne "AlwaysVerifiable"} | Remove-CsHostingProvider

## 範例 5

範例 5 會移除所有目前停用的主機供應商。為達成此目的，命令會先使用 **Get-CsHostingProvider** Cmdlet 傳回設定供組織使用之所有主機供應商的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出停用的供應商，亦即選取 Enabled 屬性等於 False 的供應商。然後再將篩選後的集合管線傳送到 **Remove-CsHostingProvider** Cmdlet，以刪除每個停用的主機供應商。

    Get-CsHostingProvider | Where-Object {$_.Enabled -eq $False} | Remove-CsHostingProvider

## 詳細描述

同盟是兩個組織用來建立信任關係的方法，以促進兩個群組之間的溝通。建立同盟後，兩個組織的使用者便可互相傳送立即訊息、訂閱目前狀態通知，並使用如 Lync 2013 等 SIP 應用程式互相通訊。Lync Server 允許三種同盟：1) 您組織與其他組織之間的直接同盟；2) 您組織與公用提供者之間的同盟；3) 您組織與協力廠商主機供應商之間的同盟。

主機供應商是為其他組織提供 SIP 通訊服務的組織；例如 Fabrikam, Inc. 可能託管 Contoso、Northwind Traders、Wingtip Toys 等組織的使用者。當您與主機供應商建立同盟關係時，便能夠有效率地與該供應商所託管的任何組織建立同盟關係。例如，如果您與 Fabrikam Hosting 同盟，您的使用者便能夠與 Contoso、Northwind Traders 及 Wingtip Toys 的使用者交換立即訊息和目前狀態的資訊。

主機供應商也用於分割網域案例。在分割網域案例中，您有部分使用者的帳戶被託管在內部部署中 (亦即被託管在您的 Lync Server 本端實作)。其他使用者的帳戶由第三方主機供應商在外部部署維護。與主機供應商同盟可讓內部部署使用者與外部部署使用者互相通訊。

為了與協力廠商主機供應商同盟，您必須建立並啟用新的主機供應商。(此外，協力廠商供應商必須與您建立同盟關係)。如果您日後決定終止此關係，可以使用 **Remove-CsHostingProvider** Cmdlet 刪除主機供應商。當您刪除主機供應商後，會自同盟協力廠商清單中移除該供應商；到時候重新建立關係的唯一方法就是重新建立供應商。如果您要暫時中止關係，請改用 **Disable-CsHostingProvider** Cmdlet。當主機供應商為停用時，不會自同盟協力廠商清單中刪除該供應商；而是標記為已停用，同時也會停用您組織與該供應商之間的通訊。若要重新建立關係，您可以使用 **Enable-CsHostingProvider** Cmdlet 重新啟用供應商。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsHostingProvider** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsHostingProvider"}

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
<td><p>要移除之主機供應商的唯一識別碼。Identity 是字串值；Identity 可能是主機供應商的完整網域 (FQDN) 名稱 (例如 fabrikam.com)，或者可能是提供服務的公司名稱 (Fabrikam, Inc.)。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayHostingProvider 物件。**Remove-CsHostingProvider** Cmdlet 接受主機供應商物件的管線傳送執行個體。

## 傳回類型

無。反之，此 Cmdlet 會刪除 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayHostingProvider 物件的執行個體。

## 請參閱

#### 其他資源

[Disable-CsHostingProvider](disable-cshostingprovider.md)  
[Enable-CsHostingProvider](enable-cshostingprovider.md)  
[Get-CsHostingProvider](get-cshostingprovider.md)  
[New-CsHostingProvider](new-cshostingprovider.md)  
[Set-CsHostingProvider](set-cshostingprovider.md)

