---
title: Lync Server 2013：行動的部署程序
TOCTitle: 行動的部署程序
ms:assetid: 5a1cebda-c14b-4ff4-9c36-f7caa868160f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690023(v=OCS.15)
ms:contentKeyID: 49291012
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中行動的部署程序

 

_**上次修改主題的時間：** 2015-03-09_

    Some information in this topic pertains to Cumulative Updates for Lync Server 2013: February 2013. It is noted accordingly.

本節說明部署 Lync Server 2013 行動功能所需的步驟順序。

### 行動性部署程序

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>階段</th>
<th>步驟</th>
<th>權限</th>
<th>部署文件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>建立網域名稱系統 (DNS) 記錄</p></td>
<td><ul>
<li><p>建立內部 DNS CNAME 或 A (主機，如果是 IPv6，則為 AAAA) 記錄，以解析內部自動探索服務 URL。</p></li>
<li><p>建立外部 DNS CNAME 或 A (主機，如果是 IPv6，則為 AAAA) 記錄，以解析外部自動探索服務 URL。</p></li>
</ul></td>
<td><p>Domain Admins</p>
<p>DnsAdmins</p></td>
<td><p><a href="lync-server-2013-creating-dns-records-for-the-autodiscover-service.md">在 Lync Server 2013 中建立自動探索服務的 DNS 記錄</a></p></td>
</tr>
<tr class="even">
<td><p>修改憑證</p></td>
<td><p>新增主體替代名稱項目至下列憑證，以支援行動使用者的安全連線：</p>
<ul>
<li><p>Director憑證</p></li>
<li><p>前端集區憑證</p></li>
<li><p>反向 Proxy 憑證</p></li>
</ul></td>
<td><p>本機系統管理員</p></td>
<td><p><a href="lync-server-2013-modifying-certificates-for-mobility.md">在 Lync Server 2013 中修改行動憑證</a></p></td>
</tr>
<tr class="odd">
<td><p>設定反向 Proxy</p></td>
<td><ul>
<li><p>將以主體替代名稱更新的憑證指派給 Secure Sockets Layer (SSL) 接聽程式。</p></li>
<li><p>為外部自動探索服務 URL 重新設定 Web 發行規則。</p></li>
<li><p>確定 前端集區上有外部 Lync Server 2013 Web 服務 URL 的 Web 發行規則存在。</p></li>
</ul>
<p>或者</p>
<ul>
<li><p>如果您選擇使用 HTTP 來進行初始自動探索要求，而且不更新憑證上的主體替代名稱清單，請為連接埠 80 HTTP 設定新的 Web 發行規則或者重新設定現有的發行規則。</p></li>
</ul></td>
<td><p>本機系統管理員</p></td>
<td><p><a href="lync-server-2013-configuring-the-reverse-proxy-for-mobility.md">在 Lync Server 2013 中設定行動的反向 Proxy</a></p></td>
</tr>
<tr class="even">
<td><p>使用 Mcx Mobility Service 測試 Lync 2010 Mobile 的行動部署</p></td>
<td><p>執行 <strong>Test-CsMcxP2PIM</strong>，以測試從一個人傳送立即訊息給另一個人。</p>
<p>如需 <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Test-CsMcxP2PIM">Test-CsMcxP2PIM</a> 選項的完整清單，請參閱 Lync Server 管理命令介面 Cmdlet 文件。</p></td>
<td><p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-verifying-your-mobility-deployment.md">在 Lync Server 2013 中驗證行動性部署</a></p></td>
</tr>
<tr class="odd">
<td><p>使用 UCWA Web 元件測試 Lync 2013 Mobile 用戶端的行動部署</p></td>
<td><p>使用 <strong>Test-CsUcwaConference</strong> Cmdlet，以測試並驗證預先定義的測試使用者或一對實際使用者可使用 UCWA 來建立並參與會議。</p>
<p>如需 <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Test-CsUcwaConference">Test-CsUcwaConference</a> 選項的完整清單，請參閱 Lync Server 管理命令介面 Cmdlet 文件。</p></td>
<td><p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-verifying-your-mobility-deployment.md">在 Lync Server 2013 中驗證行動性部署</a></p></td>
</tr>
<tr class="even">
<td><p>設定推入通知</p></td>
<td><ul>
<li><p>針對 Lync Server 2013Edge Server，新增 Lync Server 線上裝載提供者，並設定裝載提供者同盟。</p></li>
<li><p>針對 Lync Server 2010Edge Server，新增 Lync Server 線上裝載提供者，並設定裝載提供者同盟。</p></li>
<li><p>針對 Office Communications Server 2007 R2Edge Server，新增同盟協力廠商。</p></li>
<li><p>如果您要透過 Wi-Fi 網路來支援推入通知，請設定 TCP 連接埠 5223 的輸出防火牆規則。</p></li>
<li><p>使用 <strong>Set-CsPushNotificationConfiguration</strong> Cmdlet 來啟用推入通知至 Apple Push Notification Service (APNS) 及 Microsoft Push Notification Service (MPNS)。此功能預設為停用。</p></li>
<li><p>使用 <strong>Test-CsFederatedPartner</strong> Cmdlet 來測試同盟設定，並使用 <strong>Test-CsMCXPushNotification</strong> Cmdlet 來測試推入通知。</p>
<div class="alert">
> [!NOTE]
> 推入通知是用於 Apple 裝置和 Windows Phone 上的 Lync 2010 Mobile 用戶端<br />
> 推入通知只對 Windows Phone 上的 Lync 2013 Mobile 用戶端是必要的

</div></li>
</ul></td>
<td><p>RtcUniversalServerAdmins</p></td>
<td><p><a href="lync-server-2013-configuring-for-push-notifications.md">在 Lync Server 2013 中設定推播通知</a></p></td>
</tr>
<tr class="odd">
<td><p>設定行動原則</p></td>
<td><p>使用 <strong>Set-CsMobilityPolicy</strong> Cmdlet，以允許或禁止下列項目︰</p>
<ul>
<li><p>從公司撥號</p></li>
<li><p>啟用 IP 音訊和 IP 視訊</p></li>
<li><p>要求 IP 音訊和/或 IP 視訊使用 WiFi</p></li>
</ul></td>
<td><p>CsAdministrator</p></td>
<td><p><a href="lync-server-2013-configuring-mobility-policy.md">在 Lync Server 2013 中設定行動原則</a></p></td>
</tr>
</tbody>
</table>

