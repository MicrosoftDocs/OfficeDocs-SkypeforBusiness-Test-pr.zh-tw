---
title: Get-CsDialInConferencingDtmfConfiguration
TOCTitle: Get-CsDialInConferencingDtmfConfiguration
ms:assetid: 764741e4-c1cb-4627-8774-95cf08f6cf98
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398578(v=OCS.15)
ms:contentKeyID: 49291354
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsDialInConferencingDtmfConfiguration

 

_**上次修改主題的時間：** 2015-03-09_

傳回電話撥入式會議所要使用的複頻式 (DTMF) 訊號設定。DTMF 可讓撥電話參與會議的使用者使用其電話鍵盤控制會議設定 (例如自行設定靜音和解除靜音，或鎖定和解除鎖定會議)。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsDialInConferencingDtmfConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsDialInConferencingDtmfConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 範例

## 範例 1

範例 1 所示的命令會傳回 Redmond 網站的 DTMF 設定。

    Get-CsDialInConferencingDtmfConfiguration -Identity site:Redmond

## 範例 2

範例 2 會傳回所有 DTMF 設定的集合，然後顯示集合中每個項目在私下播放 DTMF 命令的說明時所須按下的鍵值。為達成此目的，會呼叫 **Get-CsDialInConferencingDtmfConfiguration** Cmdlet，以傳回組織目前所使用之所有 DTMF 設定之所有屬性值的集合。然後，此集合會管線傳送到 **Select-Object** Cmdlet，這會挑選畫面上所要顯示的兩個屬性 (Identity 和 HelpCommand)。

    Get-CsDialInConferencingDtmfConfiguration | Select-Object Identity, HelpCommand

## 範例 3

範例 3 所示的命令會傳回網站範圍所設定的所有 DTMF 設定。此項作業可透過包含 Filter 參數和篩選值 "site:\*" 加以完成。該篩選值限制傳回具有以字元 "site:" 為開頭之 Identity 的設定資料。根據定義，那些是在網站範圍所設定的設定。

    Get-CsDialInConferencingDtmfConfiguration -Filter "site:*"

## 範例 4

範例 4 會傳回 AdmitAll 屬性不等於 8 (預設值) 的所有 DTMF 組態設定。為了完成此工作，會先呼叫不含任何參數的 **Get-CsDialInConferencingDtmfConfiguration** Cmdlet，以傳回目前使用之所有 DTMF 設定的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 AdmitAll 屬性不等於 8 的設定。

    Get-CsDialInConferencingDtmfConfiguration | Where-Object {$_.AdmitAll -ne 8}

## 詳細描述

Lync Server 可讓使用者透過撥入電話以參與會議。撥入的使用者無法檢視視訊或與其他會議出席者交換立即訊息，但他們可以完整參與會議的音訊部分。

除了可以參與會議，使用者還可以使用其電話按鍵來管理選取的會議部分。(使用者所能管理的特定會議設定會取決於使用者是否為簡報者)。例如，根據預設使用者可以按其鍵盤上的數字鍵 6，自行設定靜音或解除靜音。參與者可以私下播放參與會議的所有其他人員名字，而簡報者可對所有會議出席者設定靜音或解除靜音，以及隨時有某人加入或離開會議時啟用/停用宣告播放。

使用電話鍵盤來做選擇的功能稱為複頻式 (DTMF) 訊號：如果您曾經撥打電話號碼，並且接受指示，依照「英語請按 1，或西班牙語請按 2」的順序執行某些動作，即表示您已用過 DTMF 訊號。 **Get-CsDialInConferencingDtmfConfiguration** Cmdlet 可讓您擷取所有可用的 DTMF 命令清單，以及用來執行那些命令的數字鍵。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsDialInConferencingDtmfConfiguration** Cmdlet：RTCUniversalUserAdmins、RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsDialInConferencingDtmfConfiguration"}

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
<td><p>可讓您使用萬用字元傳回 DTMG 組態設定的一或多個集合。若要傳回在網站範圍所設定之所有設定集合，請使用下列語法：-Filter site:*。若要傳回在 Identity (您唯一可篩選的屬性) 中某處有字串值 &quot;EMEA&quot; 的所有設定集合，請使用下列語法：-Filter *EMEA*。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>指出您要傳回之 DTMF 設定集合的唯一識別碼。若要參考全域設定，請使用下列語法：-Identity global。若要參照在此網站範圍設定的集合，請使用如下語法：-Identity site:Redmond。請注意，如有指定 Identity，即無法使用萬用字元。如果您必須使用萬用字元，請改用 Filter 參數。</p>
<p>若未指定此參數，則 <strong>Get-CsDialInConferencingDtmfConfiguration</strong> Cmdlet 會傳回組織中使用之所有 DTMF 組態設定的集合。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>從 中央管理存放區本機複本擷取 DTMF 組態資料，而不從 中央管理存放區本身擷取。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Get-CsDialInConferencingDtmfConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**Get-CsDialInConferencingDtmfConfiguration** Cmdlet 會傳回 Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.DialInConferencingDtmfConfiguration 物件的執行個體。

## 請參閱

#### 其他資源

[New-CsDialInConferencingDtmfConfiguration](new-csdialinconferencingdtmfconfiguration.md)  
[Remove-CsDialInConferencingDtmfConfiguration](remove-csdialinconferencingdtmfconfiguration.md)  
[Set-CsDialInConferencingDtmfConfiguration](set-csdialinconferencingdtmfconfiguration.md)

