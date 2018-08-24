---
title: Lync Server 2013：前端集區的 DNS 需求
TOCTitle: 前端集區的 DNS 需求
ms:assetid: 02d2aa6b-9e01-437b-a2df-00590280150d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398082(v=OCS.15)
ms:contentKeyID: 49289916
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中前端集區的 DNS 需求

 

_**上次修改主題的時間：** 2015-03-09_

若要順利完成此程序，您至少應該以 Domain Admins 群組成員或 DnsAdmins 群組成員的身分登入伺服器或網域。

您必須在 拓撲產生器中發行拓撲之前，先設定必要的網域名稱系統 (DNS) 記錄。此外，用於 Lync Server 2013 部署設定中的某些完整網域名稱 (FQDN) 是邏輯而非實體伺服器 FQDN，所以在發行之前需要額外的 DNS 設定。

> [!WARNING]
> Lync Server 2013 不支援單一標籤的網域。例如，根網域名稱為 <strong>contoso.local</strong> 的樹系是受支援的，名為 <strong>local</strong> 的根網域則不受支援。如需詳細資訊，請參閱 Microsoft 知識庫文章 300684＜為具有單一標籤 DNS 名稱之網域設定 Windows 的相關資訊＞，網址為 <a href="http://support.microsoft.com/kb/300684/zh-tw" class="uri">http://support.microsoft.com/kb/300684/zh-tw</a>。


> [!IMPORTANT]  
> 您指定的名稱必須與伺服器上設定的電腦名稱相同。根據預設，未加入網域的電腦，其電腦名稱是簡稱，而不是 FQDN。拓撲產生器使用 FQDN，而不是簡稱。當您為執行 Lync Server、Edge Server 和集區的伺服器指派 FQDN 時，<strong>只能使用標準字元</strong> (包括 A–Z、a–z、0–9 與連字號)。請勿使用 Unicode 字元或底線。當 FQDN 必須指派給憑證的 SN 時，外部 DNS 與公用憑證授權單位 (CA) 通常不支援在 FQDN 中使用非標準字元。



在部署拓撲後進行操作以前，請確保已建立下列 Active Directory 和 DNS 記錄 (如您的特定功能需求所規定)：

  - 將存在於拓撲中的每個伺服器角色都會發行為 Active Directory 物件 (將電腦加入至網域中即可完成此動作)。

  - 每個伺服器都存在 DNS A 記錄。

  - 如果您打算針對格式為 \_sipinternaltls\_tcp.*\<SIP domain\>* 的用戶端使用自動登錄，則每個 SIP 網域都存在 DNS SRV 記錄。如果您將對用戶端使用手動設定，則不需要此記錄。

  - 每個已設定簡單 URL 的 DNS A 記錄通常有四種：meet、dialin、lwa 及 scheduler。此外，還有 admin 簡單 URL，這是用於存取 Lync Server 2013 控制台的特別 URL。

  - 執行 SQL Server 的伺服器必須加入網域，並可由發行 拓撲產生器的電腦連線。

下表追蹤規劃章節中呈現的參考架構。如需詳細資訊，請參閱規劃文件中的＜ [Lync Server 2013 中的外部使用者存取案例](lync-server-2013-scenarios-for-external-user-access.md)＞。

### 前端集區 所需的 DNS 記錄

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>位置</th>
<th>類型</th>
<th>FQDN</th>
<th>對應至/註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>內部 DNS</p></td>
<td><p>A</p></td>
<td><p>pool01.contoso.net</p></td>
<td><p>Pool01 (DNS 負載平衡)。集區內對應至集區 FQDN 之每部 前端伺服器的 IP 位址需要 DNS A 記錄。</p></td>
</tr>
<tr class="even">
<td><p>內部 DNS</p></td>
<td><p>A</p></td>
<td><p>pool01.contoso.net</p></td>
<td><p>Pool01 (硬體負載平衡器的虛擬 IP (VIP))。</p></td>
</tr>
<tr class="odd">
<td><p>內部 DNS</p></td>
<td><p>A</p></td>
<td><p>fe01.contoso.net</p>
<p>fe02.contoso.net</p>
<p>fe03.contoso.net</p>
<p>…</p></td>
<td><p>Pool01 前端伺服器 (節點 1)。</p>
<p>Pool01 前端伺服器 (節點 2)。</p>
<p>Pool01 前端伺服器 (節點 3)。</p>
<p>…</p></td>
</tr>
<tr class="even">
<td><p>內部 DNS</p></td>
<td><p>A</p></td>
<td><p>fe02.contoso.net</p></td>
<td><p>Pool01 前端伺服器 (節點 2)。</p></td>
</tr>
<tr class="odd">
<td><p>內部 DNS</p></td>
<td><p>A</p></td>
<td><p>lsweb.contoso.net</p></td>
<td><p>用戶端到伺服器 Web 流量的 Pool01 (VIP)。</p></td>
</tr>
<tr class="even">
<td><p>內部 DNS</p></td>
<td><p>A</p></td>
<td><p>sqlbe.contoso.net</p></td>
<td><p>執行 SQL Server 2008 R2 的 Pool01 後端伺服器。</p></td>
</tr>
<tr class="odd">
<td><p>內部 DNS</p></td>
<td><p>A</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>下列情況所需的記錄： Lync Phone Edition，或自動登入不具 DNS SRV 記錄的用戶端，以及嚴格網域比對。並非所有情況下都需要此種記錄。</p></td>
</tr>
<tr class="even">
<td><p>內部 DNS</p></td>
<td><p>A</p></td>
<td><p>sip.fabrikam.com</p></td>
<td><p>假設第二個 SIP 網域。下列情況所需的記錄： Lync Phone Edition、自動登入不具 DNS SRV 記錄的用戶端，以及嚴格網域比對。並非所有情況下都需要此種記錄。</p></td>
</tr>
<tr class="odd">
<td><p>內部 DNS</p></td>
<td><p>A</p></td>
<td><p>dialin.contoso.com</p></td>
<td><p>適用於內部發行電話撥入式會議的簡單 URL - 前端伺服器 (或已安裝的 Director) 回應簡單 URL 查詢。</p></td>
</tr>
<tr class="even">
<td><p>內部 DNS</p></td>
<td><p>A</p></td>
<td><p>meet.contoso.com</p></td>
<td><p>適用於內部發行會議的簡單 URL - 前端伺服器 (或已安裝的 Director) 回應簡單 URL 查詢。</p></td>
</tr>
<tr class="odd">
<td><p>內部 DNS</p></td>
<td><p>A</p></td>
<td><p>admin.contoso.com</p>
<p>admin</p></td>
<td><p>適用於內部發行 Lync Server 2013 控制台的選用記錄、簡單 URL - 前端伺服器 (或已安裝的 Director) 回應簡單 URL 查詢。建議僅使用主機名稱 (沒有網域名稱)。</p></td>
</tr>
</tbody>
</table>


> [!NOTE]  
> VIP = 硬體負載平衡器的虛擬 IP 位址



## 前端集區的 DNS SRV 記錄


<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>位置</th>
<th>類型</th>
<th>FQDN</th>
<th>目標 FQDN</th>
<th>[Port] (連接埠)</th>
<th>對應至/註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>內部 DNS</p></td>
<td><p>SRV</p></td>
<td><p>_sipinternaltls._tcp.contoso.com</p></td>
<td><p>pool01.contoso.com</p></td>
<td><p>5061</p></td>
<td><p>在內部進行 Lync 2013 用戶端的自動設定時所需的記錄。</p></td>
</tr>
<tr class="even">
<td><p>內部 DNS</p></td>
<td><p>SRV</p></td>
<td><p>_sipinternaltls._tcp.fabrikam.com</p></td>
<td><p>pool01.fabrikam.com</p></td>
<td><p>5061</p></td>
<td><p>在內部進行 Lync 2013 用戶端的自動設定時所需的記錄。</p></td>
</tr>
<tr class="odd">
<td><p>內部 DNS</p></td>
<td><p>SRV</p></td>
<td><p>_ntp._udp.contoso.com</p></td>
<td><p>dc01.contoso.com</p></td>
<td><p>123</p></td>
<td><p>執行 Lync Phone Edition 的裝置所需的網路時間通訊協定 (NTP) 來源。在內部，此記錄應指向網域控制站。如果未定義網域控制站，則會嘗試使用 NTP 伺服器 time.windows.com。</p></td>
</tr>
</tbody>
</table>

