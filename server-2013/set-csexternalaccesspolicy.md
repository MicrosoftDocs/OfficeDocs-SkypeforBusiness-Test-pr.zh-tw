---
title: Set-CsExternalAccessPolicy
TOCTitle: Set-CsExternalAccessPolicy
ms:assetid: d3e45fbb-357f-4ff2-b52d-58b94e8f2241
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398916(v=OCS.15)
ms:contentKeyID: 49292415
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsExternalAccessPolicy

 

_**上次修改主題的時間：** 2015-03-09_

可讓您修改現有外部存取原則的屬性。外部存取原則可指定使用者是否可以：1) 和同盟組織中用工作階段初始通訊協定 (SIP) 帳戶的使用者通訊；2) 和使用公用立即訊息 (IM) 之 SIP 帳戶的使用者通訊 (例如 MSN)；以及 3) 直接從網際網路存取 Lync Server，而無須登入內部網路。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsExternalAccessPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsExternalAccessPolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-EnableFederationAccess <$true | $false>] [-EnableOutsideAccess <$true | $false>] [-EnablePublicCloudAccess <$true | $false>] [-EnablePublicCloudAudioVideoAccess <$true | $false>] [-EnableXmppAccess <$true | $false>] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會修改 Identity 為 RedmondExternalAccessPolicy 的個別使用者外部存取原則。在此範例中，命令會將 EnableFederationAccess 屬性的值變更為 True。

    Set-CsExternalAccessPolicy -Identity RedmondExternalAccessPolicy -EnableFederationAccess $True

## 範例 2

範例 2 會針對設定供組織使用的所有外部存取原則啟用同盟存取功能。為達成此目的，命令會先呼叫不含任何參數的 **Get-CsExternalAccessPolicy** Cmdlet，以傳回目前設定使用的所有外部原則集合。然後，此集合會管線傳送到 **Set-CsExternalAccessPolicy** Cmdlet，以變更集合中每一個原則的 EnableFederationAccess 屬性值。

    Get-CsExternalAccessPolicy | Set-CsExternalAccessPolicy -EnableFederationAccess $True

## 範例 3

範例 3 會針對已在個別使用者範圍設定的所有外部存取原則啟用同盟存取功能。為了執行此工作，命令會先使用 **Get-CsExternalAcessPolicy** Cmdlet 搭配 Filter 參數，以傳回在個別使用者範圍設定之所有原則的集合；篩選值 "tag:\*" 可將傳回的資料限制在 Identity 開頭為字串值 "tag:" 的原則。所有 Identity 開頭為 "tag:" 的原則都是已在個別使用者範圍設定的原則。然後將篩選後的集合管線傳送到 **Set-CsExternalAccessPolicy** Cmdlet，以修改集合中每一個原則的 EnableFederationAccess 屬性。

    Get-CsExternalAccessPolicy -Filter tag:* | Set-CsExternalAccessPolicy -EnableFederationAccess $True

## 範例 4

範例 4 會針對允許公用雲端存取的所有外部存取原則啟用同盟存取功能。為達成此目的，命令會先使用 **Get-CsExternalAccessPolicy**，以傳回目前設定供組織使用之所有外部存取原則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 EnablePublicCloudAccess 屬性等於 True 的原則。接著將篩選後的集合管線傳送到 **Set-CsExternalAccessPolicy** Cmdlet，以取得每一個原則，並將 EnableFederationAccess 屬性設為 True。整體效果：允許公用雲端存取的所有外部存取原則也允許同盟存取。

    Get-CsExternalAccessPolicy | Where-Object {$_.EnablePublicCloudAccess -eq $True} | Set-CsExternalAccessPolicy -EnableFederationAccess $True

## 詳細描述

安裝 Lync Server 時，只允許使用者彼此交換立即訊息和目前狀態資訊：根據預設，他們只能與在您的 Active Directory 網域服務 中擁有 SIP 帳戶的人員進行通訊。此外，不允許使用者透過網際網路存取 Lync Server；而是在他們可以登入 Lync Server 之前，必須登入您的內部網路。

這可能足以符合您的通訊需求。如果不符合您的需求，您可以使用外部存取原則，擴充使用者通訊和共同作業的能力。外部存取原則可以授與 (或撤銷) 使用者執行下列任何或全部作業的能力：

1\. 與具有含同盟組織 SIP 帳戶的人員通訊。請注意，單獨啟用同盟將不提供使用者這項功能。而是您必須啟用同盟，然後指派使用者外部存取原則，給予他們與同盟使用者通訊的權限。

2\. 透過公用立即訊息服務 (例如 MSN) 與具有 SIP 帳戶的人員通訊。

3.透過網際網路存取 Lync Server，而不必先登入您的內部網路。這讓使用者可以使用 Lync，並從網路咖啡廳或其他遠端位置登入 Lync Server。

在建立外部存取原則後，您可以使用 **Set-CsExternalAccessPolicy** Cmdlet，以變更該原則的屬性值。例如，根據預設，全域原則不允許使用者和擁有同盟組織帳戶的人員通訊。如果您想要將此功能授與所有使用者，可呼叫 **Set-CsExternalAccessPolicy** Cmdlet 並將全域原則的 EnableFederationAccess 屬性值設為 True。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsExternalAccessPolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsExternalAccessPolicy"}

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
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>讓系統管理員能夠提供原則隨附的其他文字。例如，Description 可包含被指派原則的使用者相關資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableFederationAccess</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出是否允許使用者與在同盟組織中具有 SIP 帳戶的人通訊。預設值為 False。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableOutsideAccess</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>表示使用者是否可以透過網際網路連線至 Lync Server，而不必登入組織的內部網路。預設值為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePublicCloudAccess</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出是否允許使用者與在公用網際網路連線供應商 (例如 MSN) 中有 SIP 帳戶的人通訊。預設值為 False。</p></td>
</tr>
<tr class="even">
<td><p><em>EnablePublicCloudAudioVideoAccess</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出是否允許使用者與在公用網際網路連線供應商 (例如 MSN) 中有 SIP 帳戶的人進行音訊/視訊交談。設為 False 時，每當使用者與公用網際網路連線連絡人通訊時，都會停用 Lync 中的音訊與視訊選項。預設值為 False。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableXmppAccess</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出是否允許使用者與在同盟 XMPP (Extensible Messaging and Presence Protocol) 合作夥伴中具有 SIP 帳戶的使用者通訊。預設值為 False。</p></td>
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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要修改之外部存取原則的唯一識別碼。您可以在全域、網站或個別使用者範圍內設定外部存取原則。若要修改全域原則，請使用下列語法：-Identity global。若要修改網站原則，請使用類似下列的語法：-Identity site:Redmond。若要修改個別使用者原則，請使用類似下列的語法：-Identity SalesAccessPolicy。若未指定此參數，則會修改全域原則。</p>
<p>請注意，指定 Identity 時不得使用萬用字元。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>ExternalAccessPolicyObject</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.ExternalAccess.ExternalAccessPolicy 物件。**Set-CsExternalAccessPolicy** Cmdlet 會接受外部存取原則物件的管線傳送資料。

## 傳回類型

**Set-CsExternalAccessPolicy** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Policy.ExternalAccess.ExternalAccessPolicy 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsExternalAccessPolicy](get-csexternalaccesspolicy.md)  
[Grant-CsExternalAccessPolicy](grant-csexternalaccesspolicy.md)  
[New-CsExternalAccessPolicy](new-csexternalaccesspolicy.md)  
[Remove-CsExternalAccessPolicy](remove-csexternalaccesspolicy.md)

