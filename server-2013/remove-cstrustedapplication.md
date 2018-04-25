---
title: Remove-CsTrustedApplication
TOCTitle: Remove-CsTrustedApplication
ms:assetid: 0d441b74-324b-4dab-8bd6-7d0a7eb18d28
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398176(v=OCS.15)
ms:contentKeyID: 49290076
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsTrustedApplication

 

_**上次修改主題的時間：** 2015-03-09_

從相關信任的服務中移除信任的應用程式。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Remove-CsTrustedApplication -Identity <ExternalApplicationIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

此範例會從相關聯之受信任的服務移除 Identity 為 TrustPool.litwareinc.com/tapp2 之信任的應用程式。

    Remove-CsTrustedApplication -Identity TrustPool.litwareinc.com/tapp2

## 範例 2

範例 2 會移除 Identity 包含字串 “trust” 之所有信任的應用程式。此命令會從呼叫 **Get-CsTrustedApplication** Cmdlet 開始，並傳遞 \*trust\* 的 Filter 值。此命令會擷取 Identity 中任何位置具有字串 trust 之所有信任的應用程式。接著將所擷取之信任的應用程式集合管線傳送到 **Remove-CsTrustedApplication** Cmdlet，以移除每一個信任的應用程式 (請注意，並不會刪除應用程式本身；只會移除與信任的應用程式集區和受信任的服務之關聯)。

    Get-CsTrustedApplication -Filter *trust* | Remove-CsTrustedApplication

## 詳細描述

信任的應用程式是由第三方開發的應用程式，具備做為 Lync Server 之一部分來執行的信任狀態，但不是產品的內建部分。此 Cmdlet 會從信任的應用程式集區移除信任的應用程式。請注意，並不會刪除應用程式本身，只會移除與信任的應用程式集區和受信任的服務之關聯。

當您使用此 Cmdlet 移除信任的應用程式時，必須提供 Identity 參數的值。Identity 是應用程式所在之集區的完整網域名稱 (FQDN)，後面緊接著正斜線 (/) 和應用程式識別碼。例如 TrustPool.litwareinc.com/tapp2，其中 TrustPool.litwareinc.com 是集區 FQDN，而 tapp2 是應用程式識別碼。請注意，如果您透過呼叫 **Get-CsTrustedApplication** Cmdlet 來檢視現有的應用程式，您看到的識別碼會類似如下：TrustPool.litwareinc.com/urn:application:tapp2。請注意應用程式名稱 (tapp2) 之前的首碼 urn:application:。由於此首碼是 Identity 的一部分，因此當您指定 Identity 參數的值時，不需要此首碼。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Remove-CsTrustedApplication** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsTrustedApplication\\b"}

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
<td><p>Microsoft.Rtc.Management.Xds.ExternalApplicationIdentity</p></td>
<td><p>要從信任的應用程式集區移除之信任的應用程式的唯一識別碼。Identity 值必須以 &lt;集區 FQDN&gt;/&lt;應用程式識別碼&gt; 格式輸入，其中「集區 FQDN」是應用程式所在之集區的 FQDN，而「應用程式識別碼」是應用程式的名稱。</p></td>
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
<td><p>隱藏變更前所顯示的確認提示。</p></td>
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

Microsoft.Rtc.Management.Xds.DisplayTrustedApplication 物件。接受管線傳送的受信任應用程式物件輸入。

## 傳回類型

此 Cmdlet 不會傳回值，而會移除 Microsoft.Rtc.Management.Xds.DisplayTrustedApplication 類型的物件。

## 請參閱

#### 其他資源

[New-CsTrustedApplication](new-cstrustedapplication.md)  
[Set-CsTrustedApplication](set-cstrustedapplication.md)  
[Get-CsTrustedApplication](get-cstrustedapplication.md)

