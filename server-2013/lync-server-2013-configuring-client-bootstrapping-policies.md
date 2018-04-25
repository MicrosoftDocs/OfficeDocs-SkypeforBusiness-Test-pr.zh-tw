---
title: 在 Lync Server 2013 中設定用戶端啟動程序原則
TOCTitle: 在 Lync Server 2013 中設定用戶端啟動程序原則
ms:assetid: 45042eca-b845-4207-b12f-b8b7f5d44bdf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425941(v=OCS.15)
ms:contentKeyID: 49290767
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定用戶端啟動程序原則

 

_**上次修改主題的時間：** 2015-03-09_

群組原則管理主控台 (GPMC) 和群組原則物件編輯器是您用於管理群組原則的工具。Office 群組原則系統管理範本隨附 Lync 2013.admx (ADMX) 和 .adml (ADML) 系統管理範本，其中包含您在網域中為群組原則物件設定的登錄型原則設定。ADML 檔案是 ADMX 檔案的語言特定補充。每個 ADMX 和 ADML 檔案都包含單一 Office 應用程式的原則設定。

若為 Lync 2013，在使用者第一次登入伺服器之前，您應該設定數個用戶端啟動載入原則。例如，預設伺服器以及用戶端在完成登入前應使用的安全性模式。在使用者登入之前，您可以使用群組原則在他們的電腦登錄中建立這些設定，然後開始接收來自伺服器的頻內佈建設定。下表列出 Lync 2013 可用的群組原則設定。

### Lync 2013 的群組原則設定

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>群組原則設定</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>指定伺服器<br />
(ConfigurationMode)</p></td>
<td><p>指定 Lync 2013 如何找出登入期間使用的傳輸和伺服器。在這個設定中，您要指定下列項目：</p>
<ul>
<li><p>ServerAddressExternal：指定從外部防火牆的外部連線時，用戶端和同盟連絡人所使用的伺服器名稱或 IP 位址。</p></li>
<li><p>ServerAddressInternal：指定當用戶端從組織防火牆的內部連線時，所使用的伺服器名稱或 IP 位址。</p></li>
<li><p>傳輸：指定傳輸控制通訊協定 (TCP) 或傳輸層安全性 (TLS)。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>支援的其他伺服器版本<br />
(ConfiguredServerCheckValues)</p></td>
<td><p>除了預設支援的伺服器版本以外，指定 Lync Server 2013 將要登入的伺服器版本名稱清單，以分號區隔。</p></td>
</tr>
<tr class="odd">
<td><p>停用登入失敗記錄檔的自動上傳 (DisableAutomaticSendTracing)</p></td>
<td><p>將登入失敗記錄檔自動上傳到 Lync Server 進行分析。如果登入成功，就不會自動上傳記錄檔。如果未設定這個原則，則會發生下列情況：</p>
<dl>
<dt><span></span></dt>
<dd><p>若為 Lync Online 使用者：登入失敗記錄檔會自動上傳。</p>
</dd>
<dt><span></span></dt>
<dd><p>若為 Lync 內部部署使用者：在上傳之前會顯示確認對話方塊。</p>
</dd>
</dl>
<p>停用這個設定時，Lync 內部部署和 Lync Online 使用者的登入記錄檔都會自動上傳到 Lync Server。啟用這個設定時，絕對不會自動上傳登入記錄檔。</p></td>
</tr>
<tr class="even">
<td><p>停用 SIP 連線的 HTTP 後援<br />
(DisableHttpConnect)</p></td>
<td><p>禁止 Lync Server 在 TLS 或 TCP 無法使用時，嘗試使用 HTTP 與伺服器連線。根據預設，Lync 會先嘗試使用 TLS 或 TCP 與伺服器連線，如果這兩種傳輸方式都不成功，Lync 就會嘗試使用 HTTP 來連線。使用此原則可以避免使用後援 HTTP 連線。</p></td>
</tr>
<tr class="odd">
<td><p>需要登入認證<br />
(DisableNTCredentials)</p></td>
<td><p>要求使用者提供 Lync 的登入認證，而不是在登入 SIP 伺服器期間自動使用 Windows 認證。</p></td>
</tr>
<tr class="even">
<td><p>停用伺服器版本檢查<br />
(DisableServerCheck)</p></td>
<td><p>如果您將這個原則設定為 1，會禁止 Lync 在登入之前檢查伺服器名稱和版本。根據預設，Lync 會在登入之前進行這些檢查。</p></td>
</tr>
<tr class="odd">
<td><p>可使用 BITS 下載通訊錄服務檔案<br />
(EnableBitsForGalDownload)</p></td>
<td><p>可讓 Lync 使用背景智慧型傳送服務 (BITS) 下載通訊錄服務檔案。</p></td>
</tr>
<tr class="even">
<td><p>設定 SIP 安全模式<br />
(EnableSIPHighSecurityMode)</p></td>
<td><p>可讓 Lync 提高傳送及接收立即訊息的安全性。這個原則在 Windows .NET 或 Microsoft Exchange Server 服務上沒有作用。</p>
<p>如果您沒有設定這個原則設定，Lync 可以使用任何傳輸。但是如果它沒有使用 TLS 且伺服器驗證使用者，Lync 就必須使用 NTLM 或 Kerberos 驗證。</p></td>
</tr>
<tr class="odd">
<td><p>全域通訊錄下載初始延遲<br />
(GalDownloadInitialDelay)</p></td>
<td><p>指定在下載全域通訊清單 (GAL) 之前的時間週期。預設值為 60 分鐘，表示伺服器延遲下載 GAL 檔案的時間為 0 到 60 分鐘之間的隨機期間。</p></td>
</tr>
<tr class="even">
<td><p>禁止使用者執行 Microsoft Lync<br />
(PreventRun)</p></td>
<td><p>禁止使用者執行 Lync。您可在「電腦設定」和「使用者設定」中設定此原則設定，但系統會優先使用「電腦設定」中的原則設定。</p></td>
</tr>
<tr class="odd">
<td><p>允許儲存使用者密碼<br />
(SavePassword)</p></td>
<td><p>可讓 Lync 儲存密碼。</p></td>
</tr>
<tr class="even">
<td><p>設定 SIP 壓縮模式<br />
(SipCompression)</p></td>
<td><p>指定開啟 SIP 壓縮的時間。依預設，根據介面卡速度啟用 SIP 壓縮。請注意，設定此原則可能導致登入時間變長。</p></td>
</tr>
<tr class="odd">
<td><p>信任的網域清單<br />
(TrustModelData)</p></td>
<td><p>列出與客戶 SIP 網域的首碼不符的信任網域。</p></td>
</tr>
</tbody>
</table>


在伺服器上設定的原則優先於群組原則設定和使用者設定的用戶端選項。下表摘要列出當衝突發生時，設定的優先順序。

### 群組原則優先順序

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>優先順序</th>
<th>設定的位置或方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p>Lync Server 2013 頻內佈建</p>
<p></p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p>HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Office\15.0\Lync</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p>HKEY_CURRENT_USER\SOFTWARE\Policies\Microsoft\Office\15.0\Lync</p>
<p></p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>Lync 2013 中的 [Lync - 選項] 對話方塊</p></td>
</tr>
</tbody>
</table>


## 使用 Lync 2013 系統管理範本檔案來定義群組原則設定

1.  建立根層級資料夾，以包含所有語言中立的 ADMX 檔案。例如，在此位置為您網域控制站上的集中存放區建立根資料夾：
    
    `%systemroot%\sysvol\domain\policies\PolicyDefinitions`
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>這個程序假設您想要管理您網域中的多部電腦。在這種情況下，您會將集中存放區中的範本儲存在主要網域控制站上的 Sysvol 資料夾中。這樣可以為網域系統管理範本提供一個複製的集中存放區位置。</td>
    </tr>
    </tbody>
    </table>


2.  為您將要使用的每種語言建立子資料夾。這些子資料夾包含語言特定的 ADML 資源檔案。例如，在此位置建立美國英文 (EN-US) 的子資料夾：
    
    `%systemroot%\sysvol\domain\policies\PolicyDefinitions\EN-US`

如需 ADMX 檔案的詳細資訊，請參閱＜管理群組原則 ADMX 檔案逐步指南＞，網址為 [http://go.microsoft.com/fwlink/?linkid=75124\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=75124%26clcid=0x404)。

