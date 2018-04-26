---
title: Lync Server 2013：DNS 摘要 - 單一合併 Edge (利用公用 IP 位址)
TOCTitle: DNS 摘要 - 單一合併 Edge (利用公用 IP 位址)
ms:assetid: 7b83eae4-aa1a-4cc6-8077-42176d56cab5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205025(v=OCS.15)
ms:contentKeyID: 49291416
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 DNS 摘要 - 單一合併 Edge (利用公用 IP 位址)

 

_**上次修改主題的時間：** 2015-03-09_

與憑證及連接埠的 DNS 記錄需求相比， Lync Server 2013 的遠端存取對 DNS 記錄需求則相對簡單許多。此外，依據您設定執行 Lync 2013 的用戶端以及是否啟用同盟關係而定，許多記錄都是選用的。

如需 Lync 2013 DNS 需求的詳細資訊，請參閱＜ [針對 Lync Server 2013 判定 DNS 需求](lync-server-2013-determine-dns-requirements.md)＞。

如需在 split-brain DNS 尚未設定之情況下自動設定執行 Lync 2013 之用戶端的詳細資訊，請參閱＜ [針對 Lync Server 2013 判定 DNS 需求](lync-server-2013-determine-dns-requirements.md)＞中的＜不透過 Split-Brain DNS 執行的自動設定＞一節。

下表包含用以支援單一合併邊緣拓撲 (如「單一合併邊緣拓撲」圖中所示) 所需的 DNS 記錄摘要。請注意，只有當 Lync 2013 和 Lync 2010 用戶端進行自動設定時，才需要特定 DNS 記錄。如果您打算使用群組原則物件 (GPO) 來設定 Lync 用戶端，則不需要相關聯的自動設定記錄。

## 重要： Edge Server 網路介面卡需求

為避免發生路由問題，請確認您的 Edge Server 上至少有兩張網路介面卡，並且只在與外部介面關聯的唯一網路介面卡上設定預設閘道。例如，如＜ [Lync Server 2013 中的單一合併 Edge (利用公用 IP 位址)](lync-server-2013-single-consolidated-edge-with-public-ip-addresses.md)＞中含有公開 IP 位址圖的單一合併邊緣拓撲所示，預設閘道會指向網際網路範圍內的外部路由器或可提供公開 IP 位址的防火牆。 Edge Server 頁面的網路關係是路由關係，而分 NAT 關係。

您可以在 Edge Server 中設定兩個網路介面卡，如下所示：

  - **網路介面卡 1 (內部介面)**
    
    已指派 172.25.33.10 的內部介面。
    
    未定義預設閘道。
    
    確認有一條路由從包含 Edge 內部介面的網路，連到任何包含執行 Lync Server 2013 或 Lync Server 2013 用戶端之伺服器的網路 (例如，從 172.25.33.0 到 192.168.10.0)。

  - **網路介面卡 2 (外部介面)**
    
    將三個公開 IP 位址指派給這個網路介面卡，例如，131.107.155.10 指派給 Access Edge、131.107.155.20 指派給 Web Conferencing Edge，而 131.107.155.30 指派給 AV Edge。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>對於所有三個 Edge 服務介面使用相同的 IP 位址，不過不建議這麼做。雖然這確實能夠節省 IP 位址，不過對於各個服務仍然需要不同的連接埠編號。預設的連接埠編號是 443/TCP，這能夠確保大多數遠端防火牆將允許流量。 例如，將連接埠值變更為 5061/TCP (Access Edge)、 444/TCP (Web Conferencing Edge) 和 443/TCP (AV Edge)，可能導致遠端使用者發生問題，以致其使用的防火牆埠不允許透過 5061/TCP 和 444/TCP 的流量。此外，由於能夠篩選 IP 位址，所以三個不同的 IP 位址比較容易進行疑難排解。</td>
    </tr>
    </tbody>
    </table>
    
    Access Edge 公開 IP 位址為主要位址，且其預設閘道將設為公開路由器 (131.107.155.1)。
    
    Web 會議和 A/V Edge 公開 IP 位址是 Windows Server 的 **本機區域連線內容**中 **網際網路協定第 4 版 (TCP/IPv4)** 和 **網際網路通訊協定第 6 版(TCP/IPv6)** 所出現的 **進階**區段中額外的 IP 位址。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>設定 Edge Server 使用兩片網路介面卡是兩個選項之一。另一個選項是使用一片網路介面卡供內部使用，並使用三個網路介面卡供 Edge Server 的外部使用。這個選項的主要優點是每個 Edge Server Service 都有一片不同的網路介面卡，而且能夠在疑難排解時更簡潔地收集資料。</td>
</tr>
</tbody>
</table>


### 含有公開 IP 位址的單一合併 Edge 所需的 DNS 記錄 (範例)

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
<td><p>131.107.155.10</p></td>
<td><p>Access Edge 外部介面 (Contoso)。視需要針對所有含啟用 Lync 之使用者的 SIP 網域重複</p></td>
</tr>
<tr class="even">
<td><p>外部 DNS/A</p></td>
<td><p>webcon.contoso.com</p></td>
<td><p>131.107.155.20</p></td>
<td><p>Web Conferencing Edge 外部介面</p></td>
</tr>
<tr class="odd">
<td><p>外部 DNS/A</p></td>
<td><p>av.contoso.com</p></td>
<td><p>131.107.155.30</p></td>
<td><p>A/V Edge 外部介面</p></td>
</tr>
<tr class="even">
<td><p>外部 DNS/SRV/443</p></td>
<td><p>_sip._tls.contoso.com</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>Access Edge 外部介面。在進行 Lync 2013 和 Lync 2010 用戶端的自動設定時所需，可在外部運作。視需要針對所有含啟用 Lync 之使用者的 SIP 網域重複。</p></td>
</tr>
<tr class="odd">
<td><p>外部 DNS/SRV/5061</p></td>
<td><p>_sipfederationtls._tcp.contoso.com</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>SIP Access Edge 外部介面。DNS 自動探索同盟合作夥伴 (亦稱為「允許的 SIP 網域」，先前版本稱為增強型同盟) 所需。視需要針對所有含啟用 Lync 之使用者的 SIP 網域重複</p></td>
</tr>
<tr class="even">
<td><p>內部 DNS/A</p></td>
<td><p>lsedge.contoso.net</p></td>
<td><p>172.25.33.10</p></td>
<td><p>合併 Edge 內部介面</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>上表所列記錄內含 <em>.net</em> 延伸網址或 <em>.com</em> 延伸網址，以強調在您未使用 split-brain DNS 時這些項目應該歸屬的區域。如果您使用 split-brain DNS，則所有記錄將位於相同區域，唯一區別在於該記錄的版本 (內部或外部)。如需詳細資訊，請參閱＜ <a href="lync-server-2013-determine-dns-requirements.md">針對 Lync Server 2013 判定 DNS 需求</a>＞中的＜Split-Brain DNS＞。</td>
</tr>
</tbody>
</table>


## 同盟所需的記錄


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
<td><p>SIP Access Edge 外部介面。DNS 自動探索其他可能同盟合作夥伴 (亦稱為「允許的 SIP 網域」，先前版本稱為增強型同盟) 的同盟所需。視需要針對所有含啟用 Lync 之使用者的 SIP 網域重複</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>行動性和推入通知結算需要此 SRV 記錄</td>
</tr>
</tbody>
</table>

</div></td>
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
<td><p>Access Edge 外部介面 (Contoso)。視需要針對所有含啟用 Lync 之使用者的 SIP 網域重複</p></td>
</tr>
</tbody>
</table>


## 可延伸傳訊與顯示通訊協定的 DNS 摘要


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
<td><p>Access Edge Service 或 Edge 集區 上的 XMPP Proxy 外部介面。視需要針對所有含啟用 Lync 之使用者的內部 SIP 網域重複，允許藉由設定外部存取原則，並透過全域原則、使用者所在的網站原則，或套用至已啟用 Lync 之使用者的使用者原則來與 XMPP 連絡人連絡。還必須在 XMPP 同盟合作夥伴中設定允許的 XMPP 網域。如需其他詳細資訊，請參閱 <strong>請參閱</strong>＞中的主題。</p></td>
</tr>
<tr class="even">
<td><p>外部 DNS/A</p></td>
<td><p>xmpp.contoso.com (範例)</p></td>
<td><p>裝載 XMPP Proxy 的 Edge Server 或 Edge 集區上的 Access Edge Service IP 位址</p></td>
<td><p>指向裝載 XMPP Proxy 服務的 Access Edge Service 或 Edge 集區。一般而言，您所建立的 SRV 記錄將指向此主機 (A 或 AAAA) 記錄</p></td>
</tr>
</tbody>
</table>

