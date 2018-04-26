---
title: New-CsExternalAccessPolicy
TOCTitle: New-CsExternalAccessPolicy
ms:assetid: 624a878e-6bbf-4e8b-9a5e-e7b5521fa4c1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398441(v=OCS.15)
ms:contentKeyID: 49291113
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsExternalAccessPolicy

 

_**上次修改主題的時間：** 2015-03-09_

可讓您建立新的外部存取原則。外部存取原則可指定使用者是否可以：1) 和同盟組織中用工作階段初始通訊協定 (SIP) 帳戶的使用者通訊；2) 與具有公用即時訊息 (IM) 供應商 (如 MSN) SIP 帳戶的使用者通訊；以及 3) 直接從網際網路存取 Lync Server，而無須登入內部網路。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsExternalAccessPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Description <String>] [-EnableFederationAccess <$true | $false>] [-EnableOutsideAccess <$true | $false>] [-EnablePublicCloudAccess <$true | $false>] [-EnablePublicCloudAudioVideoAccess <$true | $false>] [-EnableXmppAccess <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會建立 Identity 為 site:Redmond 的新外部存取原則；在建立時，系統會自動將此原則指派給 Redmond 網站。請注意，這個新的原則會將 EnableFederationAccess 與 EnableOutsideAccess 屬性設為 True。

    New-CsExternalAccessPolicy -Identity site:Redmond -EnableFederationAccess $True -EnableOutsideAccess $True

## 範例 2

範例 2 示範 InMemory 參數的使用方式；此參數可讓您為外部存取原則建立僅存在於記憶體中的執行個體。建立執行個體後，您可以修改僅存在於記憶體中的執行個體，然後使用 **Set-CsExternalAccessPolicy** Cmdlet 將虛擬原則轉換成實際的外部存取原則。

為達成此目的，範例的第一個命令會使用 **New-CsExternalAccessPolicy** Cmdlet 與 InMemory 參數來建立 Identity 為 RedmondAccessPolicy 的虛擬原則，此虛擬原則會儲存在名為 $x 的變數中。接下來的三個命令則用來修改虛擬原則的三個屬性：EnableFederationAccess、EnablePublicCloudAccess 以及 EnableOutsideAccess。最後，最終一個命令會使用 **Set-CsExternalAccessPolicy** Cmdlet 實際建立 Identity 為 RedmondAccessPolicy 的個別使用者外部存取原則。如果您未呼叫 **Set-CsExternalAccessPolicy** Cmdlet，則一旦您終止 Windows PowerShell 工作階段或刪除變數 $x，該虛擬原則便會消失。如果發生這種狀況，將不會建立 Identity 為 RedmondAccessPolicy 的外部存取原則。

``` 
$x = New-CsExternalAccessPolicy -Identity RedmondAccessPolicy -InMemory
$x.EnableFederationAccess = $True
$x.EnablePublicCloudAccess = $True
$x.EnableOutsideAccess = $True
Set-CsExternalAccessPolicy -Instance $x  
```

## 詳細描述

安裝 Lync Server 時，只允許使用者彼此交換立即訊息和目前狀態資訊：根據預設，他們只能與 Active Directory 網域服務 中具有 SIP 帳戶的其他人員通訊。此外，不允許使用者透過網際網路存取 Lync Server；他們必須先登入您的內部網路，才可以登入 Lync Server。

這可能足以符合您的通訊需求。如果不符合您的需求，您可以使用外部存取原則，擴充使用者通訊和共同作業的能力。外部存取原則可以授與 (或撤銷) 使用者執行下列任何或全部作業的能力：

1\. 與具有含同盟組織 SIP 帳戶的人員通訊。請注意，單獨啟用同盟將不提供使用者這項功能。而是您必須啟用同盟，然後指派使用者外部存取原則，給予他們與同盟使用者通訊的權限。

2\. 透過公用立即訊息服務 (例如 MSN) 與具有 SIP 帳戶的人員通訊。

3\. 透過網際網路存取 Lync Server，而不必先登入您的內部網路。這讓使用者可以使用 Lync Server，並從網路咖啡廳或其他遠端位置登入 Lync Server。

當您安裝 Lync Server 時，系統會自動為您建立全域外部存取原則。除了全域原則外，您也可以在網站範圍或個別使用者範圍建立自訂的外部存取原則。如果您在網站範圍建立外部存取原則，則在建立時會自動將該原則指派給網站。如果您在個別使用者範圍建立外部存取原則，雖會建立原則，但不會指派給任何的使用者。若要將原則指派給使用者或使用者群組，請使用 **Grant-CsExternalAccessPolicy** Cmdlet。

可以使用 **New-CsExternalAccessPolicy** Cmdlet 建立新的外部存取原則。請注意，只能在網站或個別使用者範圍建立這些原則；您無法在全域範圍建立新原則。此外，每個網站只能有一個外部存取原則：如果 Redmond 網站已指派有外部存取原則，則您無法為該網站建立第二個原則。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **New-CsExternalAccessPolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

    Get-CsAdminRole | Where-Object  {$_.Cmdlets -match "New-CsExternalAccessPolicy"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>指派給原則的唯一 Identity。新的外部存取原則會在網站範圍或個別使用者範圍建立。若要建立新的網站原則，請使用首碼 &quot;site:&quot;以及網站名稱做為您的 Identity。例如，這個語法會為 Redmond 網站建立新的原則：-Identity site:Redmond。若要建立新的個別使用者原則，請使用如下的 Identity：-Identity SalesAccessPolicy。</p>
<p>請注意，您無法建立新的全域原則；如果您要對全域原則進行變更，請改用 <strong>Set-CsExternalAccessPolicy</strong> Cmdlet。同樣地，如果使用該 Identity 的原則已存在，您便無法建立新的網站原則或個別使用者原則。如果您需要變更現有的原則，請使用 <strong>Set-CsExternalAccessPolicy</strong> Cmdlet。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>可讓系統管理員提供原則隨附的說明文字。例如，Description 可包含被指派原則的使用者相關資訊。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableFederationAccess</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出是否允許使用者與在同盟組織中具有 SIP 帳戶的人通訊。預設值為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableOutsideAccess</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出是否允許使用者透過網際網路連線到 Lync Server，而不必登入組織的內部網路。預設值為 False。</p></td>
</tr>
<tr class="even">
<td><p><em>EnablePublicCloudAccess</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出是否允許使用者與在公用網際網路連線供應商 (例如 MSN) 中有 SIP 帳戶的人通訊。預設值為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePublicCloudAudioVideoAccess</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出是否允許使用者與具有公用網際網路連線供應商 (如 MSN) SIP 帳戶的人進行音訊/視訊交談。設為 False 時，每當使用者與可連上公用網際網路的連絡人通訊時，都會停用 Lync Server 中的音訊與視訊選項。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableXmppAccess</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出是否允許使用者與在同盟 XMPP (Extensible Messaging and Presence Protocol) 合作夥伴中具有 SIP 帳戶的使用者通訊。預設值為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照但不實際將該物件認可為永久變更。如果您會將這個利用此參數呼叫之 Cmdlet 的輸出指派給變數，可以變更物件參照的屬性，然後呼叫與此 Cmdlet 配對的 Set- Cmdlet，認可這些變更。</p></td>
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

無。**New-CsExternalAccessPolicy** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

建立 Microsoft.Rtc.Management.WritableConfig.Policy.ExternalAccess.ExternalAccessPolicy 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsExternalAccessPolicy](get-csexternalaccesspolicy.md)  
[Grant-CsExternalAccessPolicy](grant-csexternalaccesspolicy.md)  
[Remove-CsExternalAccessPolicy](remove-csexternalaccesspolicy.md)  
[Set-CsExternalAccessPolicy](set-csexternalaccesspolicy.md)

