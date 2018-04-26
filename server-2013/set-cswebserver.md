---
title: Set-CsWebServer
TOCTitle: Set-CsWebServer
ms:assetid: 95a7be5b-9e53-40b9-b7b8-3a4bae9c946c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398759(v=OCS.15)
ms:contentKeyID: 49291717
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsWebServer

 

_**上次修改主題的時間：** 2015-03-09_

修改 Lync Server 所使用的一或多個 Web 伺服器服務。 Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsWebServer [-Identity <XdsGlobalRelativeIdentity>] [-AppSharingPortCount <UInt16>] [-AppSharingPortStart <UInt16>] [-Confirm [<SwitchParameter>]] [-ExternalFqdn <Fqdn>] [-ExternalHttpPort <UInt16>] [-ExternalHttpsPort <UInt16>] [-Force <SwitchParameter>] [-InternalFqdn <Fqdn>] [-McxSipExternalListeningPort <UInt16>] [-McxSipPrimaryListeningPort <UInt16>] [-MeetingRoomAdminPortalExternalListeningPort <UInt16>] [-MeetingRoomAdminPortalInternalListeningPort <UInt16>] [-PrimaryHttpPort <UInt16>] [-PrimaryHttpsPort <UInt16>] [-PublishedExternalHttpPort <UInt16>] [-PublishedExternalHttpsPort <UInt16>] [-PublishedPrimaryHttpPort <UInt16>] [-PublishedPrimaryHttpsPort <UInt16>] [-ReachExternalPsomServerPort <UInt16>] [-ReachPrimaryPsomServerPort <UInt16>] [-RmWebSipExternalListeningPort <UInt16>] [-RmWebSipPrimaryListeningPort <UInt16>] [-SupportConferenceConsoleSipExternalListeningPort <UInt16>] [-SupportConferenceConsoleSipPrimaryListeningPort <UInt16>] [-UcwaSipExternalListeningPort <UInt16>] [-UcwaSipPrimaryListeningPort <UInt16>] [-UserServer <String>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會變更單一 Web 服務集區的 PrimaryHttpPort：其 Identity 為 WebServer:atl-cs-001.litwareinc.com 的集區。在此範例中，連接埠會變更為連接埠號碼 89。

    Set-CsWebServer -Identity "WebServer:atl-cs-001.litwareinc.com" -PrimaryHttpPort 89

## 範例 2

範例 2 所示的命令是範例 1 所示命令的變化；此範例會修改組織中所有 Web 服務集區的 PrimaryHttpPort。為達成此目的，命令會先使用 **Get-CsService** Cmdlet 並搭配 WebServer 參數，以傳回目前使用之所有 Web 服務集區的集合。然後再將該集合管線傳送至 **ForEach-Object** Cmdlet，以將集合中每個集區的 PrimaryHttpPort 設為連接埠 89。因為 **Set-CsWebServer** Cmdlet 本身無法接受管線傳送的資料，所以必須將資料管線傳送至 **ForEach-Object** Cmdlet。

    Get-CsService -WebServer | ForEach-Object {Set-CsWebServer -Identity $_.Identity -PrimaryHttpPort 89}

## 詳細描述

Lync Server 會大量使用 Web 伺服器和 Web 服務。例如，通訊錄查詢可以透過 Web 服務 (通訊錄查詢 Web 服務) 進行。 Lync Server 也可代管網頁，讓使用者可以設定其電話撥入式會議個人識別碼 (PIN) 等等。有鑑於 Web 伺服器及 Web 服務所扮演的重要角色，系統管理員必須知道如何設定這些伺服器及服務。若要傳回該資訊，可以使用下列命令：

Get-CsService –WebServer

有時候，讓系統管理員能變更設定其 Web 伺服器的方法，也很重要。例如，您可能需要修改外部 HTTP 或 HTTPS 連線使用的連接埠。這類連接埠的變更 (和其他修改) 可以使用 **Set-CsWebServer** Cmdlet 來進行。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsWebServer** Cmdlet：RTCUniversalServerAdmins。若要傳回指派給該 Cmdlet 的所有角色型存取控制 (RBAC) 角色清單 (包括您自己建立的任何自訂 RBAC 角色)，請在 Windows PowerShell 提示中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsWebServer"}

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
<td><p><em>AppSharingPortCount</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>配置用於應用程式共用的連接埠總數。要開啟的實際連接埠會從設定給 AppSharingPortStart 的值開始算起，延續到指定給 AppSharingPortCount 的連接埠數目。例如，如果 AppSharingPortStart 設為 60000，而 AppSharingPortCount 設為 100，則連接埠 60000 至 60099 將會用於應用程式共用。預設值為 16383。</p></td>
</tr>
<tr class="even">
<td><p><em>AppSharingPortStart</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>配置用於應用程式共用之連接埠範圍中的第一個連接埠。預設值為 49152。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>供內部網路外的人員用於連線至 Web 服務集區的完整網域名稱 (FQDN)。例如：-ExternalFqdn &quot;www.litwareinc.com&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>ExternalHttpPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>使用 HTTP 通訊協定建立之外部 Web 連線使用的連接埠號碼。預設值為連接埠 8080。</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalHttpsPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>使用 HTTPS 通訊協定建立之外部 Web 連線使用的連接埠號碼。預設值為連接埠 4443。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Web 服務集區的唯一識別碼。例如：-Identity &quot;WebServer:atl-cs-001.litwareinc.com&quot;。</p>
<p>請注意，您可以省略首碼 &quot;WebServer&quot;：指定 Web 伺服器時。例如：-Identity &quot;atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>InternalFqdn</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Mobility Service 的完整網域名稱。您只能從組織防火牆的內部存取 InternalFqdn。</p></td>
</tr>
<tr class="even">
<td><p><em>McxSipExternalListeningPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>Mobility Service 的外部聆聽連接埠。</p></td>
</tr>
<tr class="odd">
<td><p><em>McxSipPrimaryListeningPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>Mobility Service 的內部聆聽連接埠。</p></td>
</tr>
<tr class="even">
<td><p><em>MeetingRoomAdminPortalExternalListeningPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>Lync 會議室管理入口網站的外部聆聽連接埠。該管理入口網站是以網路為基礎的公用程式，可讓系統管理員輕鬆管理會議室。</p></td>
</tr>
<tr class="odd">
<td><p><em>MeetingRoomAdminPortalInternalListeningPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>Lync 會議室管理入口網站的內部聆聽連接埠。該管理入口網站是以網路為基礎的公用程式，可讓系統管理員輕鬆管理會議室。</p></td>
</tr>
<tr class="even">
<td><p><em>PrimaryHttpPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>使用 HTTP 通訊協定建立之內部 Web 連線使用的連接埠號碼。預設值為連接埠 80。</p></td>
</tr>
<tr class="odd">
<td><p><em>PrimaryHttpsPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>使用 HTTPS 通訊協定建立的內部 Web 連線使用的連接埠號碼。預設值為連接埠 443。</p></td>
</tr>
<tr class="even">
<td><p><em>PublishedExternalHttpPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>所發佈之外部 HTTP 連接埠的連接埠號碼。</p></td>
</tr>
<tr class="odd">
<td><p><em>PublishedExternalHttpsPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>Mobility Service 的外部連接埠。</p></td>
</tr>
<tr class="even">
<td><p><em>PublishedPrimaryHttpPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>所發佈之主要 HTTP 連接埠的連接埠號碼。</p></td>
</tr>
<tr class="odd">
<td><p><em>PublishedPrimaryHttpsPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>Mobility Service 的內部連接埠。</p></td>
</tr>
<tr class="even">
<td><p><em>ReachExternalPsomServerPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>持續性共用物件模型通訊協定 (用於會議的 Microsoft 通訊協定) 使用的外部連接埠號碼。預設連接埠號碼為 8061。</p></td>
</tr>
<tr class="odd">
<td><p><em>ReachPrimaryPsomServerPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>持續性共用物件模型通訊協定 (用於會議的 Microsoft 通訊協定) 使用的主要連接埠號碼。預設連接埠號碼為 8060。</p></td>
</tr>
<tr class="even">
<td><p><em>RmWebSipExternalListeningPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>Persistent Chat Room Management Web App 的外部聆聽連接埠。只有安裝並設定常設聊天室的使用者，才可使用此應用程式。</p></td>
</tr>
<tr class="odd">
<td><p><em>RmWebSipPrimaryListeningPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>Persistent Chat Room Management Web App 的主要聆聽連接埠。只有安裝並設定常設聊天室的使用者，才可使用此應用程式。</p></td>
</tr>
<tr class="even">
<td><p><em>SupportConferenceConsoleSipExternalListeningPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>支援會議主控台的聆聽連接埠。預設值為 6007。</p></td>
</tr>
<tr class="odd">
<td><p><em>SupportConferenceConsoleSipPrimaryListeningPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>Office 365 支援會議主控台使用的連接埠。此主控台可供支援人員疑難排解有關會議和線上會議的問題。</p></td>
</tr>
<tr class="even">
<td><p><em>UcwaSipExternalListeningPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>整合通訊 Web API (UCWA) 的外部 SIP 聆聽連接埠。預設值為 5088。</p></td>
</tr>
<tr class="odd">
<td><p><em>UcwaSipPrimaryListeningPort</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt16</p></td>
<td><p>整合通訊 Web API (UCWA) 的內部 SIP 聆聽連接埠。預設值為 5089。</p></td>
</tr>
<tr class="even">
<td><p><em>UserServer</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>與 Web 服務集區相關聯之 User Services 集區的服務 ID。例如：-UserServer &quot;UserServer:atl-cs-001.litwareinc.com&quot;。</p></td>
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

無。**Set-CsWebServer** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

無。反之， **Set-CsWebServer** Cmdlet 會修改 Microsoft.Rtc.Management.Xds.DisplayWebServer 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsService](get-csservice.md)

