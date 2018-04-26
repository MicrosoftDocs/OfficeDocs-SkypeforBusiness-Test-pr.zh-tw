---
title: New-CsPublicProvider
TOCTitle: New-CsPublicProvider
ms:assetid: 0b2dcb40-13f8-4ce6-b537-527d34895ceb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398161(v=OCS.15)
ms:contentKeyID: 49290059
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPublicProvider

 

_**上次修改主題的時間：** 2015-03-09_

建立與新公用提供者的同盟關係。公用提供者是可以為大眾提供立即訊息、目前狀態及相關服務的組織。 Lync Server 的出貨版本中設有 Yahoo、AIM (AOL) 及 Messenger (MSN) 三家公用提供者，但未加以啟用。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsPublicProvider -Identity <XdsGlobalRelativeIdentity> -Enabled <$true | $false> -ProxyFqdn <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-IconUrl <String>] [-InMemory <SwitchParameter>] [-VerificationLevel <AlwaysVerifiable | AlwaysUnverifiable | UseSourceVerification>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會與 Identity 為 Fabrikam 的公用提供者建立新的同盟關係。除了指定 Identity 之外，也必須設定以下其他兩個屬性值 (及其對應參數)：ProxyFqdn (設為 proxyserver.fabrikam.com) 及 Enabled (在此範例中設為 True)。

    New-CsPublicProvider -Identity "Fabrikam" -ProxyFqdn "proxyserver.fabrikam.com" -Enabled $True

## 範例 2

範例 2 會示範如何僅在記憶體中建立新的公用提供者、修改該提供者的屬性，然後將該虛擬提供者轉變成組織中可使用的實際提供者。為達此目的，範例中的第一個命令會建立 Identity 為 Fabrikam 的公用提供者。除了加入必要參數 (Identity、ProxyFQDN 及 Enabled) 之外，該命令還會加入 InMemory 參數，以建立僅存於記憶體中的提供者執行個體，並將其儲存在名為 $x 的變數中。

建立提供者的記憶體內執行個體之後，範例中的第二個命令會修改虛擬提供者的 VerificationLevel。然後，最後一個命令會使用 **Set-CsPublicProvider** Cmdlet，將虛擬提供者 (以 $x 儲存) 轉變成實際的公用提供者。如果您沒有呼叫 **Set-CsPublicProvider** Cmdlet，將不會建立實際提供者。接著，當您結束 Windows PowerShell 工作階段或刪除變數 $x 時，虛擬提供者將會消失。

    $x = New-CsPublicProvider -Identity "Fabrikam" -ProxyFqdn "proxyserver.fabrikam.com" -Enabled $True -InMemory
    $x.VerificationLevel = "AlwaysUnverifiable"
    Set-CsPublicProvider -Instance $x

## 詳細描述

同盟是兩個組織用來建立信任關係的方法，以促進兩個群組之間的溝通。如果建立了同盟，兩個組織中的使用者就可以互相傳送立即訊息、訂閱目前狀態通知，以及使用 SIP 應用程式 (例如 Lync 2013) 相互進行通訊。 Lync Server 允許下列三種同盟類型：1) 您的組織與其他組織之間的直接同盟；2) 您的組織與公用提供者之間的同盟；以及 3) 您的組織與協力廠商主機供應商之間的同盟。

公用提供者是為大眾提供 SIP 通訊服務的組織。當您與公用提供者建立同盟關係時，實際上是與擁有該提供者所提供帳戶的所有使用者建立同盟。例如，如果您與 Messenger (MSN) 結盟，您的使用者便能夠與任何具有 Messenger (MSN) 立即訊息帳戶的使用者交換立即訊息和目前狀態資訊。

若要與公用提供者同盟，您必須建立並啟用新的公用提供者 (此外，該公用提供者也必須與您建立同盟關係)。 **Set-CsPublicProvider** 可讓您修改已設定為在組織中使用之任何公用提供者的屬性值。

請注意，如果您的 Edge Server 已設為使用預設路由，而非 DNS 伺服器路由，您將無法與公用提供者結盟。

誰可以執行這個 Cmdlet：根據預設，會授權下列群組的成員執行 **New-CsPublicProvider** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsPublicProvider"}

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
<td><p>指出您的組織與公用提供者之間是否仍存在同盟關係。如果設為 True，組織中的使用者將可以與在該公用提供者之主機上擁有帳戶的使用者交換立即訊息和目前狀態資訊。如果設為 False，組織中的使用者將無法與在該公用提供者之主機上擁有帳戶的使用者交換立即訊息和目前狀態資訊。您隨時可以分別使用 <strong>Enable-CsPublicProvider</strong> Cmdlet 與 <strong>Disable-CsPublicProvider</strong> Cmdlet 來啟用及停用同盟關係。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>要建立之公用提供者的唯一識別碼。Identity 通常是提供服務的網站名稱 (例如，Yahoo!、AOL 或 MSN )。</p>
<p>Identity 不只在公用提供者間必須是唯一的，在主機供應商間也必須是唯一的。假設您嘗試建立 Identity 為 Fabrikam 的新公用提供者。如果具有該 Identity 的公用提供者或主機供應商已經存在，則命令將會失敗。</p></td>
</tr>
<tr class="odd">
<td><p><em>ProxyFqdn</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>指定公用提供者所使用之 Proxy 伺服器的完整網域名稱 (FQDN) (例如，proxyserver.fabrikam.com)。</p>
<p>Proxy FQDN 不只在公用提供者間必須是唯一的，在主機供應商間也必須是唯一的。例如，假設您嘗試建立 Proxy FQDN 為 proxyserver.fabrikam.com 的新公用提供者。如果具有該 Proxy FQDN 的公用提供者或主機供應商已存在，則命令將會失敗。</p></td>
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
<td><p><em>IconUrl</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>用來指出 Microsoft Skype 連絡人的圖示 URL。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
</tr>
<tr class="even">
<td><p><em>VerificationLevel</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Edge.VerificationLevelType</p></td>
<td><p>表示如何驗證 (或是否驗證) 從公用提供者傳送的訊息，以確認它們確實是傳送自該提供者。VerificationLevel 必須設為下列其中一個值：</p>
<p>AlwaysVerifiable。會接受由此提供者所傳送的所有訊息。如果訊息中找不到驗證標頭，則 Lync Server 將會新增驗證標頭。此為預設值。</p>
<p>AlwaysUnverifiable。所有宣稱從公用提供者傳送而來的訊息皆會被視為未驗證。只有來自收件者連絡人清單上之人員所傳送的訊息才會加以傳遞。例如，如果 Ken Myer 在您的連絡人清單上，您便能接收其訊息。如果 Pilar Ackerman 不在您的連絡人清單上，您便無法接收其訊息。請注意， Lync 2013 使用者可以手動覆寫此設定，讓自己可以接收未列名其連絡人清單上之人員的訊息。</p>
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

無。 **New-CsPublicProvider** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

建立 Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider 物件的新執行個體。

## 請參閱

#### 其他資源

[Disable-CsPublicProvider](disable-cspublicprovider.md)  
[Enable-CsPublicProvider](enable-cspublicprovider.md)  
[Get-CsPublicProvider](get-cspublicprovider.md)  
[Remove-CsPublicProvider](remove-cspublicprovider.md)  
[Set-CsPublicProvider](set-cspublicprovider.md)

