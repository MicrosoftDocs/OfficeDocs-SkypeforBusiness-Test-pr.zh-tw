---
title: Lync Server 2013：內部伺服器的憑證需求
TOCTitle: 內部伺服器的憑證需求
ms:assetid: 0444cdbd-538c-43b1-b9a1-9d7d6cf818d6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398094(v=OCS.15)
ms:contentKeyID: 49289941
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中內部伺服器的憑證需求

 

_**上次修改主題的時間：** 2015-03-09_

執行 Lync Server 以及需要憑證的內部伺服器，包含 Standard Edition Server、Enterprise Edition 前端伺服器、中繼伺服器和 Director。下表顯示這些伺服器的憑證需求。您可以使用 Lync Server 憑證精靈來要求這些憑證。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>與 前端集區、 前端伺服器或 Director 上簡單 URL 相關聯的主體替代名稱支援萬用字元憑證。如需萬用字元憑證支援的詳細資訊，請參閱＜ <a href="lync-server-2013-wildcard-certificate-support.md">Lync Server 2013 中的萬用字元憑證支援</a>＞。</td>
</tr>
</tbody>
</table>


雖然建議內部伺服器使用內部企業憑證授權單位 (CA)，但您也可以使用公用 CA。有些公用 CA 提供的憑證符合整合通訊 (UC) 憑證的特定需求，而且也與 Microsoft 合作以確保其憑證適用於 Lync Server 憑證精靈，請參閱 Microsoft 知識庫文章 929395＜Exchange Server 和 Communications Server 的整合通訊憑證合作夥伴＞，網址為 [http://go.microsoft.com/fwlink/?linkid=202834\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=202834%26clcid=0x404)。

與其他應用程式和伺服器 (例如 Exchange 2013) 通訊時，需要其他應用程式和產品支援的憑證。 Lync Server 2013 及其他 2013 版的 Microsoft 伺服器產品 (包括 Exchange 2013 和 SharePoint Server) 支援使用開放授權 (OAuth) 通訊協定來進行伺服器對伺服器驗證和授權。如需詳細資訊，請參閱部署文件或作業文件中的＜ [在 Lync Server 2013 中管理伺服器對伺服器驗證 (Oauth) 與夥伴應用程式](lync-server-2013-managing-server-to-server-authentication-oauth-and-partner-applications.md)＞。

對於從執行 Windows 7 作業系統、 Windows Server 2008 作業系統、 Windows Server 2008 R2 作業系統、 Windows Vista 作業系統 和 Microsoft Lync Phone Edition 的用戶端建立的連線， Lync Server 2013 支援 (但不需要) 以 SHA-256 加密編譯雜湊函數簽署的憑證。為了支援使用 SHA-256 的外部存取，外部憑證由公用 CA 使用 SHA-256 發行。

下表依伺服器角色顯示前端集區和 Standard Edition Server 的憑證需求。這些全部都是不可匯出的標準 Web 伺服器憑證、私密金鑰。

請注意，當您使用憑證精靈要求憑證時，會自動設定伺服器增強金鑰使用方法 (EKU)。

> [!NOTE]  
> 每個憑證易記名稱在電腦存放區中都必須是唯一的。



> [!NOTE]  
> 如果您已在您的 DNS 中設定 sipinternal.contoso.com 或 sipexternal.contoso.com，則必須將其新增至憑證的主體替代名稱。



### Standard Edition Server 的憑證

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>憑證</th>
<th>主體名稱/ 一般名稱</th>
<th>主體替代名稱</th>
<th>範例</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>預設</p></td>
<td><p>集區的完整網域名稱 (FQDN)</p></td>
<td><p>集區的 FQDN 和伺服器的 FQDN</p>
<p>如果您擁有多個 SIP 網域，且已啟用用戶端自動設定，則憑證精靈會偵測並新增每個支援的 SIP 網域 FQDN</p>
<p>如果此集區是用戶端的自動登入伺服器且群組原則中需要嚴格網域名稱系統 (DNS) 比對，則您也需要 sip.sipdomain (對於您具有的每個 SIP 網域) 的項目。</p></td>
<td><p>SN=se01.contoso.com；SAN=se01.contoso.com</p>
<p>如果此集區是用戶端的自動登入伺服器且群組原則中需要嚴格 DNS 比對，則您也需要 SAN=sip.contoso.com；SAN=sip.fabrikam.com</p></td>
<td><p>在 Standard Edition Server，伺服器 FQDN 與集區 FQDN 相同。</p>
<p>精靈會偵測任何您在安裝期間指定的 SIP 網域，並將之自動新增到主體替代名稱。</p>
<p>您也可以使用此憑證來進行伺服器對伺服器驗證。</p></td>
</tr>
<tr class="even">
<td><p>Web 內部</p></td>
<td><p>伺服器的 FQDN</p></td>
<td><p>下列每一項：</p>
<ul>
<li><p>內部 Web FQDN (與伺服器的 FQDN 相同)</p></li>
<li><p>Meet 簡單 URL</p></li>
<li><p>Dial-in 簡單 URL</p></li>
<li><p>Admin 簡單 URL</p>
<p></p></li>
<li><p>或者，簡單 URL 的萬用字元項目</p></li>
</ul>
<p></p></td>
<td><p>SN=se01.contoso.com；SAN=se01.contoso.com；SAN=meet.contoso.com；SAN=meet.fabrikam.com；SAN=dialin.contoso.com；SAN=admin.contoso.com</p>
<p>使用萬用字元憑證：</p>
<p>SN=se01.contoso.com；SAN=se01.contoso.com；SAN=*.contoso.com</p></td>
<td><p>您無法在 拓撲產生器中覆寫內部 Web FQDN。</p>
<p>如果您具有多個 Meet 簡單 URL，則必須將這些 URL 納入為主體替代名稱。</p>
<p>簡單 URL 項目支援萬用字元項目。</p></td>
</tr>
<tr class="odd">
<td><p>Web 外部</p></td>
<td><p>伺服器的 FQDN</p></td>
<td><p>下列每一項：</p>
<ul>
<li><p>外部 Web FQDN</p></li>
<li><p>Dial-in 簡單 URL</p></li>
<li><p>Meet 簡單 URL (按 SIP 網域)</p></li>
<li><p>或者，簡單 URL 的萬用字元項目</p></li>
</ul></td>
<td><p>SN=se01.contoso.com；SAN=webcon01.contoso.com；SAN=meet.contoso.com；SAN=meet.fabrikam.com；SAN=dialin.contoso.com</p>
<p>使用萬用字元憑證：</p>
<p>SN=se01.contoso.com；SAN=webcon01.contoso.com；SAN=*.contoso.com</p></td>
<td><p>如果您具有多個 Meet 簡單 URL，則必須將這些 URL 納入為主體替代名稱。</p>
<p>簡單 URL 項目支援萬用字元項目。</p></td>
</tr>
</tbody>
</table>


### 前端集區中前端伺服器的憑證

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>憑證</th>
<th>主體名稱/ 一般名稱</th>
<th>主體替代名稱</th>
<th>範例</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>預設</p></td>
<td><p>集區的 FQDN</p></td>
<td><p>集區的 FQDN 和伺服器的 FQDN。</p>
<p>如果您擁有多個 SIP 網域，且已啟用用戶端自動設定，則憑證精靈會偵測並新增每個支援的 SIP 網域 FQDN</p>
<p>如果此集區是用戶端的自動登入伺服器且群組原則中需要嚴格 DNS 比對，則您也需要 sip.sipdomain (對於您具有的每個 SIP 網域) 的項目。</p></td>
<td><p>SN=eepool.contoso.com；SAN=eepool.contoso.com；SAN=ee01.contoso.com</p>
<p>如果此集區是用戶端的自動登入伺服器且群組原則中需要嚴格 DNS 比對，則您也需要 SAN=sip.contoso.com；SAN=sip.fabrikam.com</p></td>
<td><p>精靈會偵測任何您在安裝期間指定的 SIP 網域，並將之自動新增到主體替代名稱。</p>
<p>您也可以使用此憑證來進行伺服器對伺服器驗證。</p></td>
</tr>
<tr class="even">
<td><p>Web 內部</p></td>
<td><p>集區的 FQDN</p></td>
<td><p>下列每一項：</p>
<ul>
<li><p>內部 Web FQDN (與伺服器的 FQDN 不同)</p></li>
<li><p>伺服器 FQDN</p></li>
<li><p>Lync 集區 FQDN</p></li>
<li><p>Meet 簡單 URL</p></li>
<li><p>Dial-in 簡單 URL</p></li>
<li><p>Admin 簡單 URL</p></li>
<li><p>或者，簡單 URL 的萬用字元項目</p></li>
</ul>
<p></p></td>
<td><p>SN=ee01.contoso.com；SAN=ee01.contoso.com；SAN=meet.contoso.com；SAN=meet.fabrikam.com；SAN=dialin.contoso.com；SAN=admin.contoso.com</p>
<p>使用萬用字元憑證：</p>
<p>SN=ee01.contoso.com；SAN=ee01.contoso.com；SAN=*.contoso.com</p></td>
<td><p>如果您具有多個 Meet 簡單 URL，則必須將這些 URL 納入為主體替代名稱。</p>
<p>簡單 URL 項目支援萬用字元項目。</p></td>
</tr>
<tr class="odd">
<td><p>Web 外部</p></td>
<td><p>集區的 FQDN</p></td>
<td><p>下列每一項：</p>
<ul>
<li><p>外部 Web FQDN</p></li>
<li><p>Dial-in 簡單 URL</p></li>
<li><p>Admin 簡單 URL</p></li>
<li><p>或者，簡單 URL 的萬用字元項目</p></li>
</ul></td>
<td><p>SN=ee01.contoso.com；SAN=webcon01.contoso.com；SAN=meet.contoso.com；SAN=meet.fabrikam.com；SAN=dialin.contoso.com</p>
<p>使用萬用字元憑證：</p>
<p>SN=ee01.contoso.com；SAN=webcon01.contoso.com；SAN=*.contoso.com</p></td>
<td><p>如果您具有多個 Meet 簡單 URL，則必須將這些 URL 納入為主體替代名稱。</p>
<p>簡單 URL 項目支援萬用字元項目。</p></td>
</tr>
</tbody>
</table>


### Director 的憑證

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>憑證</th>
<th>主體名稱/ 一般名稱</th>
<th>主體替代名稱</th>
<th>範例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>預設</p></td>
<td><p>Director 集區的 FQDN</p></td>
<td><p>Director 的 FQDN，Director 集區的 FQDN</p>
<p>如果此集區是用戶端的自動登入伺服器且群組原則中需要嚴格 DNS 比對，則您也需要 sip.sipdomain (對於您具有的每個 SIP 網域) 的項目。</p></td>
<td><p>SN=dir-pool.contoso.com；SAN=dir-pool.contoso.com；SAN=dir01.contoso.com</p>
<p>如果此 Director 集區是用戶端的自動登入伺服器且群組原則中需要嚴格 DNS 比對，則您也需要 SAN=sip.contoso.com；SAN=sip.fabrikam.com</p></td>
</tr>
<tr class="even">
<td><p>Web 內部</p></td>
<td><p>伺服器的 FQDN</p></td>
<td><p>下列每一項：</p>
<ul>
<li><p>內部 Web FQDN (與伺服器的 FQDN 相同)</p></li>
<li><p>Meet 簡單 URL</p></li>
<li><p>Dial-in 簡單 URL</p></li>
<li><p>Admin 簡單 URL</p></li>
<li><p>或者，簡單 URL 的萬用字元項目</p></li>
</ul>
<p></p></td>
<td><p>SN=dir01.contoso.com；SAN=dir01.contoso.com；SAN=meet.contoso.com；SAN=meet.fabrikam.com；SAN=dialin.contoso.com；SAN=admin.contoso.com</p>
<p>SN=dir01.contoso.com；SAN=dir01.contoso.com SAN=*.contoso.com</p></td>
</tr>
<tr class="odd">
<td><p>Web 外部</p></td>
<td><p>伺服器的 FQDN</p></td>
<td><p>下列每一項：</p>
<ul>
<li><p>外部 Web FQDN</p></li>
<li><p>Dial-in 簡單 URL</p></li>
<li><p>Admin 簡單 URL</p></li>
<li><p>或者，簡單 URL 的萬用字元項目</p></li>
</ul></td>
<td><p>Director 外部 Web FQDN 必須與 前端集區或 前端伺服器不同。</p>
<p>SN=dir01.contoso.com；SAN=directorwebcon01.contoso.com SAN=meet.contoso.com；SAN=meet.fabrikam.com；SAN=dialin.contoso.com</p>
<p>SN=dir01.contoso.com；SAN=directorwebcon01.contoso.com SAN=*.contoso.com</p></td>
</tr>
</tbody>
</table>


如果您具有獨立中繼伺服器集區，則該集區中的每個中繼伺服器都需要下表所列的憑證。如果您將中繼伺服器與前端伺服器組合在一起，則本主題中前面的「前端集區中前端伺服器的憑證」表格中所列的憑證已足夠。

### 獨立中繼伺服器的憑證

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>憑證</th>
<th>主體名稱/ 一般名稱</th>
<th>主體替代名稱</th>
<th>範例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>預設</p></td>
<td><p>集區的 FQDN</p></td>
<td><p>集區的 FQDN</p>
<p>集區成員伺服器的 FQDN</p></td>
<td><p>SN=medsvr-pool.contoso.net；SAN=medsvr-pool.contoso.net；SAN=medsvr01.contoso.net</p></td>
</tr>
</tbody>
</table>


### Survivable Branch Appliance 的憑證

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>憑證</th>
<th>主體名稱/ 一般名稱</th>
<th>主體替代名稱</th>
<th>範例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>預設</p></td>
<td><p>Appliance 的 FQDN</p></td>
<td><p>SIP.&lt;sipdomain&gt; (每個 SIP 網域需要一個項目)</p></td>
<td><p>SN=sba01.contoso.net；SAN=sip.contoso.com；SAN=sip.fabrikam.com</p></td>
</tr>
</tbody>
</table>


## 請參閱

#### 概念

[Lync Server 2013 中的萬用字元憑證支援](lync-server-2013-wildcard-certificate-support.md)

