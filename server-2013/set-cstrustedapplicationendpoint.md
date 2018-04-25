---
title: Set-CsTrustedApplicationEndpoint
TOCTitle: Set-CsTrustedApplicationEndpoint
ms:assetid: 6c2713f4-8e2c-48fc-9f27-07c1d6b87a18
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398509(v=OCS.15)
ms:contentKeyID: 49291227
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTrustedApplicationEndpoint

 

_**上次修改主題的時間：** 2015-03-09_

修改信任之應用程式目前的端點連絡人。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsTrustedApplicationEndpoint -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-DisplayName <String>] [-DisplayNumber <String>] [-Enabled <$true | $false>] [-EnabledForFederation <$true | $false>] [-EnterpriseVoiceEnabled <$true | $false>] [-ExchangeArchivingPolicy <Uninitialized | UseLyncArchivingPolicy | NoArchiving | ArchivingToExchange>] [-LineURI <String>] [-PassThru <SwitchParameter>] [-PrimaryLanguage <String>] [-SecondaryLanguages <MultiValuedProperty>] [-SipAddress <String>] [-Type <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會修改 SIP 位址為 endpoint1@litwareinc.com 的應用程式端點連絡人物件。請注意，Identity 值的開頭為字串 sip:，後面再接著 SIP 位址。下一個參數 DisplayName 已被指定值 “Endpoint 1”，它會將連絡人的顯示名稱變更為該值。

    Set-CsTrustedApplicationEndpoint -Identity "sip:endpoint1@litwareinc.com" -DisplayName "Endpoint 1"

## 範例 2

此範例會修改顯示名稱為 Endpoint 1 之端點應用程式的顯示號碼。此命令會先呼叫 **Get-CsTrustedApplicationEndpoint** Cmdlet 並指定 Identity 為 Endpoint 1，以擷取使用該顯示名稱的端點連絡人物件。然後再將該物件管線傳送到 **Set-CsTrustedApplicationEndpoint** Cmdlet，以將 DisplayNumber 修改為此值 (此範例中為 (425)555-1212)。

    Get-CsTrustedApplicationEndpoint -Identity "Endpoint 1" | Set-CsTrustedApplicationEndpoint -DisplayNumber "(425)555-1212"

## 詳細描述

信任的應用程式端點是一個 Active Directory 連絡人物件，可將來電路由傳送至信任的應用程式。此 Cmdlet 移除 Active Directory 網域服務中現有的端點連絡人物件。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsTrustedApplicationEndpoint** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsTrustedApplicationEndpoint"}

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
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>要修改之應用程式端點的 Identity (辨別名稱) 或 SIP 位址。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>端點連絡人物件的顯示名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayNumber</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>將顯示在通訊錄中之連絡人的電話號碼。</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>決定是否針對 Lync Server 啟用連絡人。</p>
<p>預設值：True</p></td>
</tr>
<tr class="even">
<td><p><em>EnabledForFederation</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>決定同盟使用者是否可以存取此連絡人。</p>
<p>預設值：False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnterpriseVoiceEnabled</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>決定是否針對 Enterprise Voice 啟用連絡人。</p>
<p>預設值：True</p></td>
</tr>
<tr class="even">
<td><p><em>ExchangeArchivingPolicy</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.ExchangeArchivingPolicyOptionsEnum</p></td>
<td><p>指出連絡人的立即訊息工作階段封存位置。允許的值為：</p>
<p>* Uninitialized</p>
<p>* UseLyncArchivingPolicy</p>
<p>* ArchivingToExchange</p>
<p>* NoArchiving</p></td>
</tr>
<tr class="odd">
<td><p><em>LineURI</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>連絡人的電話號碼。格式必須為 TEL:&lt;number&gt;，例如 TEL:+14255551212。</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>加上此參數會讓 Cmdlet 不僅修改連絡人物件，而且會將新的物件當做輸出傳回。</p></td>
</tr>
<tr class="odd">
<td><p><em>PrimaryLanguage</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>受信任應用程式所使用的主要語言。必須使用有效的語言代碼來設定該語言，例如 en-US (美國英文)、fr-FR (法文) 等等。</p></td>
</tr>
<tr class="even">
<td><p><em>SecondaryLanguages</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.MultiValuedProperty</p></td>
<td><p>也可用於受信任應用程式的語言集合。必須將值設定為以逗號分隔的語言代碼清單。例如，下列語法可將法文 (加拿大) 和法文設為次要語言：-SecondaryLanguages &quot;fr-CA&quot;,&quot;fr-FR&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>SipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>您無法修改連絡人的 SIP 位址。建立應用程式端點時，會指派 SIP 位址。</p></td>
</tr>
<tr class="even">
<td><p><em>Type</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>此參數不會搭配這個 Cmdlet 使用。</p></td>
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

Microsoft.Rtc.Management.ADConnect.Schema.OCSADApplicationContact 物件。接受管線傳送的受信任應用程式端點物件輸入。

## 傳回類型

此 Cmdlet 不會傳回值，而會修改 Microsoft.Rtc.Management.ADConnect.Schema.OCSADApplicationContact 類型的物件。

## 請參閱

#### 其他資源

[New-CsTrustedApplicationEndpoint](new-cstrustedapplicationendpoint.md)  
[Remove-CsTrustedApplicationEndpoint](remove-cstrustedapplicationendpoint.md)  
[Get-CsTrustedApplicationEndpoint](get-cstrustedapplicationendpoint.md)

