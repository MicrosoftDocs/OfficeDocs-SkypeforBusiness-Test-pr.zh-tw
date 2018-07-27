---
title: DNS 摘要 - SIP、XMPP 同盟和公用立即訊息
TOCTitle: DNS 摘要 - SIP、XMPP 同盟和公用立即訊息
ms:assetid: 1ed24fb8-a849-44c0-a52e-7aef7527e644
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ618369(v=OCS.15)
ms:contentKeyID: 49290293
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# DNS 摘要 - SIP、XMPP 同盟和公用立即訊息

 

_**上次修改主題的時間：** 2015-03-09_

您可判斷是否要讓其他協力廠商針對您的網域進行自動化網域名稱系統 (DNS) 記錄探索 (定義 Office Communications Server 或 Lync Server 協力廠商同盟時需要此記錄)，來決定您的 DNS。若您發行 \_sipfederationtls.\_tcp. *\<SIP 網域名稱\>* SRV 記錄，任何其他的 SIP 同盟網域就可以「探索」您的同盟。您可以使用 Lync Server 控制台 中的「允許網域」和「封鎖網域」設定，或者，使用 Lync Server 管理命令介面以及 **Get**、**Set**、**New**、**Remove-CsAllowedDomain** 和 **-CsBlockedDomain** PowerShell Cmdlet，進行允許網域或封鎖網域設定，以控制哪些同盟網域可以和您進行通訊。如需如何進行這些設定以及 PowerShell Cmdlet 的用法之詳細資訊，請參閱本主題最後的**相關主題**。

DNS 記錄摘要表格會說明針對開放或可公開同盟的必要輸入。若您不想實作「同盟探索」，則可不設定 \_sipfederationtls.\_tcp. *\<SIP 網域名稱\>* 記錄。

> [!IMPORTANT]  
> 在某些特定案例中，您可能並不想使用可公開的同盟，卻仍必須使用 _sipfederationtls._tcp. <em>&lt;SIP 網域名稱&gt;</em> SRV 記錄，例如，當您已為使用者部署了行動性時。行動性推播通知結算所 (PNCH) 是一種特殊的同盟類型，主要供使用 Lync 2010 Mobile 用戶端之 Apple iPhone 或 iPad，或是使用 Lync 2010 Mobile 或 Lync 2013 Mobile 用戶端之 Windows Phone 上的 Microsoft Lync Mobile 用戶端使用。行動性和推播通知都需要使用 _sipfederationtls._tcp. <em>&lt;SIP 網域名稱&gt;</em> SRV 記錄。若要減輕此問題的影響，並控制可探索性，請清除 <strong>[啟用協力廠商網域探索]</strong> 設定以關閉探索。



若要為您的部署設定可延伸訊息和目前狀態通訊協定 (XMPP)，請在外部 DNS 伺服器中建立兩個網域名稱系統 (DNS) 記錄，該伺服器會將記錄解析至 Edge Server 或 Edge 集區的 Access Edge Service。

設定適用於公用立即訊息連線的網域名稱系統 (DNS) 時，您會發現支援外部使用者的設定將支援公用 IM 連線。如果您已經設定 Edge Server 或 Edge 集區，則必須有 DNS 記錄才能支援公用 IM 連線。

## DNS 摘要 - SIP 同盟


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>位置/類型/連接埠</th>
<th>FQDN</th>
<th>IP 位址/FQDN 主機記錄</th>
<th>對應至/註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>外部 DNS/SRV/5061</p></td>
<td><p>_sipfederationtls._tcp.contoso.com</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>您的同盟和其他潛在同盟協力廠商之自動 DNS 探索的必要 Access Edge Service 外部介面，其亦稱為「允許的 SIP 網域」(舊版則稱為增強型同盟)。您可視需要，針對啟用了 Lync 之使用者的所有 SIP 網域重複此項目。</p>
<div class="alert">
> [!IMPORTANT]  
> 行動性和推播通知結算所都必須使用此 SRV 記錄。若您有一個以上的 SIP 網域，請針對將服務 Lync Mobile 用戶端的每個網域建立並發行 SRV 記錄。若不是每個部署支援的 SIP 網域都具備明確的 SRV 記錄，則推播通知服務和 Apple 推播通知服務可能無法如預期般運作。


</div></td>
</tr>
</tbody>
</table>


## DNS 摘要 - 可延伸的訊息和顯示狀態通訊協定 (XMPP)


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>位置/類型/連接埠</th>
<th>FQDN</th>
<th>IP 位址/FQDN 主機記錄</th>
<th>對應至/註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>外部 DNS/SRV/5269</p></td>
<td><p>_xmpp-server._tcp.contoso.com</p></td>
<td><p>xmpp.contoso.com</p></td>
<td><p>Access Edge Service 或 Edge 集區上的 XMPP Proxy 外部介面。請針對具有啟用 Lync 之使用者的所有內部 SIP 網域，依需要重複，在該網域中，若要與 XMPP 連絡人聯繫，可以透過全域原則、使用者所在的網站原則，或套用至啟用 Lync 之使用者的使用者原則，來設定外部存取原則。XMPP 同盟協力廠商原則中也必須設定允許的 XMPP 網域。如需詳細資訊，請參閱＜ <strong>請參閱</strong>＞中的主題。</p></td>
</tr>
<tr class="even">
<td><p>外部 DNS/A</p></td>
<td><p>xmpp.contoso.com (範例)</p></td>
<td><p>裝載 XMPP Proxy 的 Edge Server 或 Edge 集區上的 Access Edge Service IP 位址</p></td>
<td><p>指向裝載 XMPP Proxy 服務的 Access Edge Service 或 Edge 集區。一般而言，您所建立的 SRV 記錄將指向此主機 (A 或 AAAA) 記錄</p></td>
</tr>
</tbody>
</table>


## DNS 摘要 – 公用立即訊息連線


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>位置/類型/連接埠</th>
<th>FQDN/DNS 記錄</th>
<th>IP 位址/FQDN</th>
<th>對應至/註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>外部 DNS/A</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>Access Edge Service 介面</p></td>
<td><p>Access Edge Service 外部介面 (Contoso)。必要時，重複用於含有啟用 Lync 之使用者的所有 SIP 網域。</p></td>
</tr>
</tbody>
</table>


## 請參閱

#### 工作

[在 Lync Server 2013 中設定 XMPP 同盟](lync-server-2013-setting-up-xmpp-federation.md)  
[在 Lync Server 2013 中設定推播通知](lync-server-2013-configuring-for-push-notifications.md)  
[在 Lync Server 2013 中啟用或停用探索同盟協力廠商](lync-server-2013-enable-or-disable-discovery-of-federation-partners.md)  

#### 概念

[Lync Server 2013 中的外部使用者存取案例](lync-server-2013-scenarios-for-external-user-access.md)  
[針對 Lync Server 2013 判定 DNS 需求](lync-server-2013-determine-dns-requirements.md)  

#### 其他資源

[在 Lync Server 2013 中管理組織的 SIP 同盟網域](lync-server-2013-manage-sip-federated-domains-for-your-organization.md)

