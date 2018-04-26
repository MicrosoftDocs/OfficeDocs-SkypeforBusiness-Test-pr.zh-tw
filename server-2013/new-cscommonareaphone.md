---
title: New-CsCommonAreaPhone
TOCTitle: New-CsCommonAreaPhone
ms:assetid: 6082d24d-de92-4a3c-8639-5d28341cbc84
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398430(v=OCS.15)
ms:contentKeyID: 49291079
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsCommonAreaPhone

 

_**上次修改主題的時間：** 2015-03-09_

建立可以透過 Lync Server 加以管理的新公共區域電話。公共區域電話是位於大樓大廳、員工休息室，或其他可能由許多不同人使用之區域內的電話，用途可能各異。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    New-CsCommonAreaPhone -DN <ADObjectId> <COMMON PARAMETERS>

    New-CsCommonAreaPhone -OU <OUIdParameter> <COMMON PARAMETERS>

    COMMON PARAMETERS: -LineUri <String> -RegistrarPool <Fqdn> [-Confirm [<SwitchParameter>]] [-Description <String>] [-DisplayName <String>] [-DisplayNumber <String>] [-PassThru <SwitchParameter>] [-SipAddress <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會建立電話號碼為 1-425-555-6710 的公用區域電話 (請注意，LineUri 必須使用 E.164 格式指定)。除了指定電話號碼外，此命令也會指定登錄器集區 (RegistrarPool)、Active Directory 顯示名稱 (DisplayName)，以及應建立對應連絡人物件之 OU 的辨別名稱 (OU)。

    New-CsCommonAreaPhone -LineUri tel:+14255556710 -RegistrarPool redmond-cs-001.litwareinc.com -DisplayName "Building 14 Lobby" -OU "ou=Telecommunications,dc=litwareinc,dc=com"

## 範例 2

範例 2 所示的命令是範例 1 所示命令的變化。但範例 2 的新公用區域電話與現有的 Active Directory 連絡人物件相關聯。為達此目的，命令會使用 DN 參數而不使用 OU 參數，以使用現有連絡人物件的辨別名稱 (cn=Building 14 Lobby,ou=Telecommunications,dc=litwareinc,dc=com) 做為參數值。此命令中也省略了 DisplayName，表示新的公用區電話會使用已指派給現有連絡人物件的顯示名稱。

    New-CsCommonAreaPhone -LineUri tel:+14255556710 -RegistrarPool redmond-cs-001.litwareinc.com -DN "cn=Building 14 Lobby,ou=Telecommunications,dc=litwareinc,dc=com"

## 詳細描述

公用區電話是未與個別使用者相關聯的 IP 電話。 公用區電話不是位於某個人的辦公室中，通常是位於建築物大廳、餐廳、員工休息室、會議室及其他可能會聚集一群人的地點。這讓系統管理員在管理時面臨挑戰，因為在 Lync Server 中使用的電話通常是由指派給個別使用者的語音原則和撥號對應表維護。然而，公用區電話未指派有個別使用者。

解決此難題的方法是，針對所有的公用區電話建立 Active Directory 連絡人物件 (使用 **New-CsCommonAreaPhone** Cmdlet 建立這些連絡人物件)。就像使用者帳戶一樣，可以指派原則和語音對應表給這些連絡人物件。這樣一來，您就能夠對公用區電話保持控制，即使這些電話與個別使用者無關聯。例如，如果不要讓人從公用區電話轉接或保留通話，唯一要做的就是建立禁止通話轉接和保留通話的語音原則，然後將原則指派給公用區電話。(或者，更正確的說法是指派給代表公用區電話的連絡人物件)。這個命令會指派語音原則 CommonAreaPhoneVoicePolicy 給您所有的公用區電話：

Get-CsCommonAreaPhone | Grant-CsVoicePolicy –PolicyName "CommonAreaPhoneVoicePolicy"

如前所述，您可以使用 **New-CsCommonAreaPhone** Cmdlet 建立新的公用區電話。 **New-CsCommonAreaPhone** Cmdlet 可用於建立新的連絡人物件來與公共區域電話的唯一識別碼。電話搭配使用，或是讓現有的連絡人物件與新的公用區電話產生關聯。如需詳細資訊，請參閱本主題中的 OU 和 DN 參數描述。

誰可以執行此 Cmdlet：依預設，下列群組的成員獲授權可在本機上執行 **New-CsCommonAreaPhone** Cmdlet：網域系統管理員。您可以使用 **Grant-CsOUPermission** Cmdlet，指派針對特定網站或特定 Active Directory 組織單位 (OU) 執行此 Cmdlet 的權限。若要傳回已獲指派此 Cmdlet 之所有角色型存取控制 (RBAC) 角色的清單 (包括您自行建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsCommonAreaPhone"}

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
<td><p><em>DN</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.ADObjectId</p></td>
<td><p>可讓您將現有的 Active Directory 連絡人物件與新的公用區電話產生關聯。如果您有想要與公用區電話相關聯的連絡人物件，請使用 DN 參數，後面加上該連絡人的辨別名稱。例如：-DN &quot;cn=Building 14 Lobby,dc=litwareinc,dc=com&quot;。請注意，如果指定的連絡人不存在，您的命令將會失敗。如果指定的連絡人已在 Lync Server 中啟用，命令也會失敗。在這種情況下，您必須先使用 <strong>Disable-CsUser</strong> Cmdlet 停用連絡人，然後再執行 <strong>New-CsCommonAreaPhone</strong> Cmdlet。</p>
<p>在已針對會議室和其他實體建立連絡人物件的組織中，DN 參數顯得格外實用。由於這些連絡人通常是供排程之用，因此使用 DN 參數可讓您利用這些既存的連絡人物件建立新公用區電話。</p>
<p>您無法在同一個命令中使用 OU 和 DN 參數。</p></td>
</tr>
<tr class="even">
<td><p><em>LineUri</em></p></td>
<td><p>必要</p></td>
<td><p>System.String</p></td>
<td><p>公用區電話的電話號碼。指定線路統一資源識別元 (URI) 時應該採用 E.164 格式，並在開頭加上 &quot;TEL:&quot;首碼。例如：TEL:+14255551297。任何分機號碼都應該新增至線路 URI 的尾端，例如：TEL:+14255551297; ext=51297。</p></td>
</tr>
<tr class="odd">
<td><p><em>OU</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>連絡人物件應位於其中之 Active Directory 組織單位 (OU) 的辨別名稱。例如：-OU &quot;ou=Redmond,dc=litwareinc,dc=com&quot;。</p>
<p>如果您加入 OU 參數，會在指定的 OU 中建立一個新連絡人，而且該連絡人會自動被指派一個全域唯一識別碼 (GUID) 做為其一般名稱。因此，連絡人物件將具備類似下列的名稱：{ce84964a-c4da-4622-ad34-c54ff3ed361f}。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>RegistrarPool</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>連絡人物件應隸屬之登錄器集區的完整網域名稱 (FQDN)。例如：-RegistrarPool &quot;atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您設定公用區電話的 Active Directory Description 屬性。接下來，此屬性提供的方法可讓您提供關於電話的其他資訊；例如，您可能想要提供電話發生問題時要連絡之對象的詳細資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayName</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您設定公用區電話的 Active Directory 顯示名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayNumber</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>在 Lync 中顯示的電話號碼。DisplayNumber 屬性可設為任何您偏好的格式，例如 1-800-555-1234、1-(800)-555-1234、1.800.555.1234 等。選擇顯示號碼時，請記住，此號碼只有經過正規化後才會顯示在公共區域電話的顯示畫面上 (正規化是將號碼字串轉譯為標準電話號碼格式的程序)。設定顯示號碼時，如果使用的電話號碼格式沒有正規化規則，則公共區域電話的顯示畫面會顯示 LineUri 屬性的值，而非 DisplayNumber 屬性的值。</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>傳回代表一般區域電話的物件。</p></td>
</tr>
<tr class="even">
<td><p><em>SipAddress</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>唯一識別碼讓公共區域電話可以和 SIP 裝置通訊，如 Lync。SIP 位址的開頭必須是 &quot;sip:&quot; 首碼且必須包含有效的 SIP 網域。例如：sip:bldg14lobby@litwareinc.com。</p></td>
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

無。 **New-CsCommonAreaPhone** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsCommonAreaPhone** Cmdlet 會建立 Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsCommonAreaPhone](get-cscommonareaphone.md)  
[Move-CsCommonAreaPhone](move-cscommonareaphone.md)  
[Remove-CsCommonAreaPhone](remove-cscommonareaphone.md)  
[Set-CsCommonAreaPhone](set-cscommonareaphone.md)

