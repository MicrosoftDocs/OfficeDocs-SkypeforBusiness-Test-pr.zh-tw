---
title: Get-CsUCPhoneConfiguration
TOCTitle: Get-CsUCPhoneConfiguration
ms:assetid: 014bba9e-b5c4-477d-9273-c993e7a7ee9e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398070(v=OCS.15)
ms:contentKeyID: 49289894
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsUCPhoneConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回 Lync Phone Edition 之管理選項的資訊，包括所需的安全性模式，以及電話是否應在指定的閒置時間後自動鎖定等等。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsUCPhoneConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsUCPhoneConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回目前在組織中使用的所有 UC 電話組態設定。呼叫不含任何參數的 **Get-CsUCPhoneConfiguration** Cmdlet ，一律會傳回電話組態設定的完整集合。

    Get-CsUCPhoneConfiguration

## 範例 2

在範例 2 中，只會傳回 Identity 為 site:Redmond 的 UC 電話組態設定。由於識別身分必須是唯一的，因此這個命令絕不會傳回一個以上的電話組態設定集合。

    Get-CsUCPhoneConfiguration -Identity site:Redmond

## 範例 3

範例 3 會傳回網站範圍所設定的所有 UC 電話設定。為達成此目的，命令會呼叫 **Get-CsUCPhoneConfiguration** Cmdlet 搭配 Filter 參數；篩選值 "site:\*" 可將傳回的資料限制為 Identity 屬性 (唯一可以當做篩選依據的屬性) 開頭為 "site:" 字串值的設定。根據定義，所有 Identity 開頭為 "site:" 字串值的任何設定，都是在網站範圍設定的設定值。

    Get-CsUCPhoneConfiguration -Filter site:*

## 範例 4

範例 4 會傳回 SIP 安全性模式設為 Medium 的 UC 電話組態設定 (SIP 安全性可以設為 Low、Medium 或 High)。為了執行此工作，命令會先使用不含任何額外參數的 **Get-CsUCPhoneConfiguration** Cmdlet，以傳回設定供組織使用之所有 UC 電話設定的集合。然後將此集合管線傳送到 **Where-Object** Cmdlet，這會只挑出 SIPSecurityMode 屬性等於 Medium 的設定。

    Get-CsUCPhoneConfiguration | Where-Object {$_.SIPSecurityMode -eq "Medium"}

## 範例 5

範例 5 會傳回符合下列一或兩個條件的 UC 電話設定：1) 未強制執行電話鎖定；和/或 2) 最小 PIN 長度小於 6 位數。為達成此目的，命令會先呼叫 **Get-CsUCPhoneConfiguration** Cmdlet，來傳回組織目前所使用的所有 UC 電話設定集合。接著，此集合會管線傳送到 **Where-Object** Cmdlet，以選取符合下列一個 (或兩個) 條件的項目：1) EnforcePhoneLock 屬性等於 False；和/或 2) MinPhoneLength 屬性小於 6。

\-or 運算子會告知 **Where-Object** Cmdlet 挑選符合其中一個 (或兩個) 條件的設定。若要挑選符合兩個條件 (在此範例中表示未強制執行電話鎖定，而且 PIN 長度小於 6) 的設定，請使用 -and 運算子：

Where-Object {$\_.EnforcePhoneLock -eq $False -and $\_.MinPhonePinLength -lt 6}

    Get-CsUCPhoneConfiguration | Where-Object {$_.EnforcePhoneLock -eq $False -or $_.MinPhonePinLength -lt 6}

## 詳細描述

Lync Phone Edition 代表電話與 Lync Server 合併。Lync Phone Edition 會使用功能如同 Voice over Internet Protocol (VoIP) 電話的特殊硬體 (亦即與 Lync 相容的電話)。此外，此硬體也會充當類似 Lync 的端點：您可以設定目前的狀態、檢查 Lync 連絡人的狀態、搜尋新的連絡人，並執行許多其他您過去使用 Lync 執行的作業。

CsUCPhoneConfiguration Cmdlet 可讓您管理 Lync Phone Edition 電話；例如，您可以控制用來登入電話的個人識別碼 (PIN) 最小長度，以及電話在一段指定的閒置時間後是否自動鎖住本身。

電話組態設定可套用於全域範圍或網站範圍(在網站範圍套用的設定優先於在全域範圍套用的設定)。**Get-CsUCPhoneConfiguration** Cmdlet 可讓您擷取目前整個組織所採用之電話組態設定的資訊。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsUCPhoneConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsUCPhoneConfiguration"}

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
<td><p><em>Filter</em></p></td>
<td><p>選用</p></td>
<td><p>System.String</p></td>
<td><p>可讓您使用萬用字元傳回一或多個 UC 電話組態設定集合。若要傳回在網站範圍設定的所有設定集合，請使用下列語法：-Filter site:*。若要傳回在 Identity (您唯一可篩選的屬性) 中某處有字串值 &quot;EMEA&quot; 的所有設定集合，請使用下列語法：-Filter *EMEA*。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>表示您要傳回之整合通訊 (UC) 電話組態設定集合的唯一識別碼。若要參考全域設定，請使用下列語法：-Identity global。若要參考在網站範圍設定的集合，請使用類似下列的語法：-Identity &quot;site:Redmond&quot;。請注意，如有指定 Identity，即無法使用萬用字元。如果您必須使用萬用字元，請改為包含 Filter 參數。</p>
<p>若未指定此參數，則 <strong>Get-CsUCPhoneConfiguration</strong> Cmdlet 會傳回組織中目前使用之所有 UC 電話組態設定的集合。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從中央管理存放區的本機複本擷取 UC 電話組態資料，而非從中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**Get-CsUCPhoneConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsUCPhoneConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Policy.Voice.UcPhoneSettings 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsUCPhoneConfiguration](new-csucphoneconfiguration.md)  
[Remove-CsUCPhoneConfiguration](remove-csucphoneconfiguration.md)  
[Set-CsUCPhoneConfiguration](set-csucphoneconfiguration.md)

