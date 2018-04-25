---
title: Set-CsPublicProvider
TOCTitle: Set-CsPublicProvider
ms:assetid: ff7c1a5a-823c-41f7-80dc-1f5842609ccb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413087(v=OCS.15)
ms:contentKeyID: 49292934
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPublicProvider

 

_**上次修改主題的時間：** 2015-03-09_

修改目前已設定為供組織使用的公用提供者。公用提供者是一家提供立即訊息 (IM)、目前狀態和相關服務給一般大眾的組織。Lync Server 隨附三個已設定但尚未啟用的公用提供者：Yahoo\!、AOL 和 MSN。

## 語法

    Set-CsPublicProvider [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsPublicProvider [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-VerificationLevel <AlwaysVerifiable | AlwaysUnverifiable | UseSourceVerification>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 會針對 Identity 為 Messenger 的公用提供者設定 VerificationLevel。這可藉由包含 VerificationLevel 參數與參數值 AlwaysVerifiable 來完成。

    Set-CsPublicProvider -Identity "Messenger" -VerificationLevel "AlwaysVerifiable"

## 範例 2

範例 2 會修改組織目前所使用之所有公用提供者的驗證層級。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsPublicProvider** Cmdlet，以傳回目前設定為可供使用之所有公用提供者的集合。然後，此集合會管線傳送到 **Set-CsPublicProvider** Cmdlet，以取得集合中的每個提供者，並將 VerificationLevel 屬性值變更為 AlwaysVerifiable。

    Get-CsPublicProvider | Set-CsPublicProvider -VerificationLevel "AlwaysVerifiable"

## 範例 3

範例 3 所示的命令會針對任何驗證層級目前設定為 AlwaysUnverifiable 的公用提供者修改該層級。為達成此目的，命令會先呼叫 **Get-CsPublicProvider** Cmdlet 傳回目前設定供組織使用之所有公用提供者的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 VerificationLevel 屬性等於 AlwaysUnverifiable 的提供者。接著將篩選後的集合管線傳送到 **Set-CsPublicProvider** Cmdlet，以將集合中每個提供者的 VerificationLevel 變更為 AlwaysVerifiable。

    Get-CsPublicProvider | Where-Object {$_.VerificationLevel -eq "AlwaysUnverifiable"} | Set-CsPublicProvider -VerificationLevel "AlwaysVerifiable"

## 詳細描述

同盟是兩個組織用來建立信任關係的方法，以促進兩個群組之間的溝通。建立同盟後，兩個組織的使用者便可互相傳送立即訊息、訂閱目前狀態通知，並使用如 Microsoft Lync 2010 等 SIP 應用程式互相通訊。Lync Server 允許三種同盟：1) 您組織與其他組織之間的直接同盟；2) 您組織與公用提供者之間的同盟；3) 您組織與第三方主機供應商之間的同盟。

公用提供者是一家提供 SIP 通訊服務給一般大眾的組織。當您與公用提供者建立同盟關係時，實際上就等於和任何具有該提供者所提供帳戶的使用者建立同盟。例如，如果您與 Messenger (MSN) 同盟，則 (視您設定系統的方式而定) 您的使用者將能夠與其他具備 Messenger 立即訊息帳戶的人員交換立即訊息和目前狀態資訊。

為了與公用提供者同盟，您需要建立並啟用新的公用提供者 (此外，公用提供者也將需要與您建立同盟關係)。Lync Server 包括三個預先設定的公用提供者 (Yahoo\!、AOL 及 MSN)。當有其他公用提供者可供使用時，您可以使用 **New-CsPublicProvider** Cmdlet 建立與這些新提供者的同盟關係。建立同盟關係後，接著您可以使用 **Set-CsPublicProvider** Cmdlet，修改這些關係的兩個重要屬性值，分別是 Enabled 和 VerificationLevel。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsPublicProvider** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPublicProvider"}

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
<td><p><em>Enabled</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出您的組織與公用提供者之間是否仍存在同盟關係。若設定為 True，組織內的使用者將能夠與具備已在公用提供者上主控之帳戶的使用者交換立即訊息和目前狀態資訊。若設定為 False，組織內的使用者將無法與具備已在公用提供者上主控之帳戶的使用者交換立即訊息和目前狀態資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏當您執行 Cmdlet 時可能發生的任何確認提示字元或非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要修改之公用提供者的唯一識別碼。Identity 通常是提供服務的網站名稱 (例如，Yahoo!、AOL、MSN 等)。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>DisplayPublicProvider 物件</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="even">
<td><p><em>VerificationLevel</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Edge.VerificationLevelType</p></td>
<td><p>表示如何驗證 (或是否驗證) 從公用提供者傳送的訊息，以確認它們確實是傳送自該提供者。驗證層級必須設為下列其中一個值：</p>
<p>AlwaysVerifiable。會接受由此提供者所傳送的所有訊息。如果訊息中找不到驗證標頭，則 Lync Server 將會新增驗證標頭。此為預設值。</p>
<p>AlwaysUnverifiable。所有宣稱從公用提供者傳送而來的訊息皆會被視為未驗證。只有來自收件者連絡人清單上之人員所傳送的訊息才會加以傳遞。例如，如果 Ken Myer 在您的連絡人清單上，您便能接收其訊息。如果 Pilar Ackerman 不在您的連絡人清單上，您便無法接收其訊息。請注意，Lync 2013 使用者可以手動覆寫此設定，讓自己可以接收未列名其連絡人清單上之人員的訊息。</p>
<p>UseSourceVerification。使用公用提供者加在訊息中的驗證標頭。若無這項驗證資訊，將會拒絕該訊息。此 Cmdlet 已被淘汰，無法再於 Lync Server 2013中使用。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider 物件。**Set-CsPublicProvider** Cmdlet 會接受公用提供者物件的管線執行個體。

## 傳回類型

**Set-CsPublicProvider** Cmdlet 不會傳回值或物件，而是會設定 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider 物件的執行個體。

## 請參閱

#### 其他資源

[Disable-CsPublicProvider](disable-cspublicprovider.md)  
[Enable-CsPublicProvider](enable-cspublicprovider.md)  
[Get-CsPublicProvider](get-cspublicprovider.md)  
[New-CsPublicProvider](new-cspublicprovider.md)  
[Remove-CsPublicProvider](remove-cspublicprovider.md)

