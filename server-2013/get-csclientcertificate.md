---
title: Get-CsClientCertificate
TOCTitle: Get-CsClientCertificate
ms:assetid: 0949288e-9df2-42c4-8297-0dc4cb40d544
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398143(v=OCS.15)
ms:contentKeyID: 49290023
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsClientCertificate

 

_**上次修改主題的時間：** 2015-03-09_

傳回已發行給使用者之用戶端憑證的資訊。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Get-CsClientCertificate -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會傳回發行給 Ken Myer 的所有用戶端憑證。

    Get-CsClientCertificate -Identity "Ken Myer"

## 範例 2

範例 2 會傳回已發行給 Ken Myer 且設定在 2011 年 9 月 1 日前過期的所有用戶端憑證。為達成此目的，命令會先使用 **Get-CsClientCertificate** Cmdlet 傳回所有已發行給 Ken Myer 之用戶端憑證的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 ExpirationTime 內容早於 2011 年 9 月 1 日 (9/1/2011) 的憑證。在此範例中指定的日期 (9/1/2011) 係使用「英文 (美國)」格式的日期時間值。請使用相容於您的 \[地區及語言選項\] 的格式指定日期。

    Get-CsClientCertificate -Identity "Ken Myer" | Where-Object {$_.ExpirationTime -lt "9/1/2011"}

## 範例 3

範例 3 傳回自 2010 年 1 月 1 日起已發行給 Ken Myer 的所有用戶端憑證。為了完成此工作，命令會先呼叫 **Get-CsClientCertificate** Cmdlet 傳回所有已發行給 Ken Myer 之用戶端憑證的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 PublicationTime 屬性晚於 2010 年 1 月 1 日 (1/1/2010) 的憑證。

    Get-CsClientCertificate -Identity "Ken Myer" | Where-Object {$_.PublicationTime -gt "1/1/2010"}

## 範例 4

範例 4 所示的命令會傳回所有已啟用 Lync Server 且已指派給登錄器集區之使用者的用戶端憑證 (如果您嘗試擷取尚未指派到登錄器集區之使用者的憑證資訊，則會傳回錯誤)。為達成此目的，命令會呼叫不含任何參數的 **Get-CsUser** Cmdlet。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只選取 RegistrarPool 屬性不等於 Null 值的使用者。接著將篩選後的集合管線傳送到 **Get-CsClientCertificate** Cmdlet，以傳回指派給集合中每一個使用者的憑證。

    Get-CsUser | Where-Object {$_.RegistrarPool -ne $Null} | Get-CsClientCertificate

## 詳細描述

用戶端憑證提供使用者另一種獲得 Lync Server 驗證的方法。使用者向系統出示 X.509 憑證，而不提供使用者名稱和密碼 (此憑證必須具有可識別使用者的主體名稱或主體別名)。若要進行驗證，使用者只需輸入個人識別碼 (PIN)；比起輸入英數字的使用者名稱和/或密碼，輸入 PIN 對行動電話使用者來說要容易得多。

**Get-CsClientCertificate** Cmdlet 讓系統管理員能夠擷取已發行給使用者的 Lync Server 用戶端憑證相關資訊。此資訊包含發行憑證的日期與時間，還有憑證到期的日期與時間。

請注意，當您安裝 Lync Server 標準版時，預設不會啟用 SQL Server Express 的防火牆例外。這表示您不能從 Windows PowerShell 的遠端執行個體執行 **Get-CsClientCertificate** Cmdlet。原因在於您的命令將無法周遊防火牆及存取 SQL Server Express 資料庫 (但是，您仍然可以在 Standard Edition 伺服器本機上執行 Cmdlet)。如果您需要從遠端針對 Standard Edition 伺服器執行 **Get-CsClientCertificate** Cmdlet，則必須以手動方式啟用 SQL Server Express 的防火牆例外。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Get-CsClientCertificate** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsClientCertificate"}

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
<td><p>指出要擷取其憑證資訊之使用者帳戶 Identity。可以使用下列四種格式的其中一種來指定使用者識別：1) 使用者的工作階段初始通訊協定 (SIP) 位址；2) 使用者的萬用主要名稱；3) 使用者的網域名稱和登入名稱，必須是「網域\登入」格式 (例如，litwareinc\kenmyer)；以及 4) 使用者的 Active Directory 網域服務顯示名稱 (例如，Ken Myer)。您也可以利用使用者的 Active Directory 辨別名稱來參考使用者帳戶。</p>
<p>在指定使用者 Identity 時不能使用萬用字元。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
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

字串值或 Microsoft.Rtc.Management.ADConnect.Schema.ADUser 物件。**Get-CsClientCertificate** Cmdlet 接受代表使用者帳戶之 Identity 字串值的管線傳送輸入。Cmdlet 也接受管線傳送的使用者物件輸入。

## 傳回類型

**Get-CsClientCertificate** Cmdlet 會傳回 Microsoft.Rtc.Management.UserPinService.CertInfoDetails 物件的執行個體。

## 請參閱

#### 其他資源

[Revoke-CsClientCertificate](revoke-csclientcertificate.md)

