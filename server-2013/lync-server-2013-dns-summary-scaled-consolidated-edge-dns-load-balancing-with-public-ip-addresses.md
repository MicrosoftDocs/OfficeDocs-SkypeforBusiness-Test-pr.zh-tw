---
title: Lync Server 2013：DNS 摘要 - 調整式合併 Edge (透過公用 IP 位址進行 DNS 負載平衡)
TOCTitle: DNS 摘要 - 調整式合併 Edge (透過公用 IP 位址進行 DNS 負載平衡)
ms:assetid: dc8f096a-a0a4-4f71-8930-88ff8fc089d9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205319(v=OCS.15)
ms:contentKeyID: 49292530
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 DNS 摘要 - 調整式合併 Edge (透過公用 IP 位址進行 DNS 負載平衡)

 

_**上次修改主題的時間：** 2015-03-09_

與憑證及連接埠的 DNS 記錄需求相比， Lync Server 2013 的遠端存取對 DNS 記錄需求則相對簡單許多。此外，依據您設定執行 Lync 2013 的用戶端以及是否啟用同盟關係而定，許多記錄都是選用的。

如需 Lync 2013 DNS 需求的詳細資訊，請參閱＜ [針對 Lync Server 2013 判定 DNS 需求](lync-server-2013-determine-dns-requirements.md)＞。

如需在 split-brain DNS 尚未設定之情況下設定 Lync 2013 用戶端自動設定的詳細資訊，請參閱＜ [針對 Lync Server 2013 判定 DNS 需求](lync-server-2013-determine-dns-requirements.md)＞的＜不透過 Split Brain DNS 執行的自動設定＞一節。

下表包含用以支援單一整合 Edge 拓撲 (如單一整合 Edge 拓撲圖中所示) 所需的 DNS 記錄摘要。請注意，只有當 Lync 2013 用戶端進行自動設定時，才需要特定 DNS 記錄。如果您打算使用群組原則物件 (GPO) 來設定 Lync 用戶端，則不需要關聯的記錄。

## 重要： Edge Server 網路介面卡需求

為避免發生路由問題，請確認您的 Edge Server 至少有兩片網路介面卡，並且只在與外部介面關聯的唯一網路介面卡上設定預設閘道。例如，如＜ [Lync Server 2013 中的調整式合併 Edge (透過公用 IP 位址進行 DNS 負載平衡)](lync-server-2013-scaled-consolidated-edge-dns-load-balancing-with-public-ip-addresses.md)＞中的「經調整的合併 Edge 案例」圖中所示，預設閘道會指向外部防火牆。

您可以在每部 Edge Server 中設定兩片網路介面卡，如下所示：

  - **網路介面卡 1 - 節點 1 (內部介面)**
    
    已指派 172.25.33.10 的內部介面。
    
    未定義預設閘道。
    
    確認有一條路由從包含 Edge 內部介面的網路，連到任何包含執行 Lync Server 2013 或 Lync Server 2013 用戶端之伺服器的網路 (例如，從 172.25.33.0 到 192.168.10.0)。

  - **網路介面卡 1 - 節點 2 (內部介面)**
    
    已指派 172.25.33.11 的內部介面。
    
    未定義預設閘道。
    
    確認有一條路由從包含 Edge 內部介面的網路，連到任何包含執行 Lync Server 2013 或 Lync Server 2013 用戶端之伺服器的網路 (例如，從 172.25.33.0 到 192.168.10.0)。

  - **網路介面卡 2 - 節點 1 (外部介面)**
    
    有三個私人 IP 位址指派給這片網路介面卡，例如 131.107.155.10 用於 Access Edge Service、131.107.155.20 用於 Web Conferencing Edge Service、131.107.155.30 用於 A/V Edge 服務。
    
    Access Edge Service 公用 IP 位址主要與設定為公用路由器 (131.107.155.1) 的預設閘道搭配使用。
    
    Web Conferencing Edge Service 與 A/V Edge 服務 私人 IP 位址就是 Windows Server 裡，\[區域連線內容\] 的 \[網際網路通訊協定第 4 版 (TCP/IPv4)\] 與 \[網際網路通訊協定第 6 版 (TCP/IPv6)\] 內容中 \[進階\] 區段裡的其他 IP 位址。
    
    > [!NOTE]  
    > 上述的三個 Edge Service 介面確實能夠使用單一 IP 位址 (但不建議這樣做)。這樣做，雖能節省 IP 位址，但每個服務都要有不同的連接埠號碼。預設連接埠號碼為 443/TCP，其可確保大部分遠端防火牆均允許流量通過。將連接埠值變更為 (例如) 5061/TCP 以用於 Access Edge Service、444/TCP 以用於 Web Conferencing Edge Service 以及 443/TCP 以用於 A/V Edge 服務，可能會對遠端使用者造成問題，因為其防火牆不允許來自 5061/TCP 與 444/TCP 的流量通過。此外，由於能夠根據 IP 位址進行篩選，這三個不同的 IP 位址可讓疑難排解變得更輕鬆。
    


  - **網路介面卡 2 - 節點 2 (外部介面)**
    
    有三個私人 IP 位址指派給這片網路介面卡，例如 131.107.155.11 用於 Access Edge Service、131.107.155.21 用於 Web Conferencing Edge Service、131.107.155.31 用於 A/V Edge 服務。
    
    Access Edge Service 公用 IP 位址主要與設定為公用路由器 (131.107.155.1) 的預設閘道搭配使用。
    
    Web Conferencing Edge Service 與 A/V Edge 服務 私人 IP 位址就是 Windows Server 裡，\[區域連線內容\] 的 \[網際網路通訊協定第 4 版 (TCP/IPv4)\] 與 \[網際網路通訊協定第 6 版 (TCP/IPv6)\] 內容中 \[進階\] 區段裡的其他 IP 位址。

> [!TIP]
> 設定 Edge Server 使用兩片網路介面卡是兩個選項之一。另一個選項是使用一片網路介面卡供內部使用，並使用三個網路介面卡供 Edge Server 的外部使用。這個選項的主要優點是每個 Edge Server Service 都有一片不同的網路介面卡，而且能夠在疑難排解時更簡潔地收集資料。


### 經調整的合併 Edge、DNS 負載平衡搭配使用公用 IP 位址所需的 DNS 記錄 (範例)

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
<td><p>131.107.155.10 與 131.107.155.11</p></td>
<td><p>Access Edge Service 外部介面 (Contoso) 必要時，重複用於含有 Lync 啟用之使用者的所有 SIP 網域</p></td>
</tr>
<tr class="even">
<td><p>外部 DNS/A</p></td>
<td><p>webcon.contoso.com</p></td>
<td><p>131.107.155.20 與 131.107.155.21</p></td>
<td><p>Web Conferencing Edge Service 外部介面</p></td>
</tr>
<tr class="odd">
<td><p>外部 DNS/A</p></td>
<td><p>av.contoso.com</p></td>
<td><p>131.107.155.30 與 131.107.155.31</p></td>
<td><p>A/V Edge 服務 外部介面</p></td>
</tr>
<tr class="even">
<td><p>外部 DNS/SRV/443</p></td>
<td><p>_sip._tls.contoso.com</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>Access Edge Service 外部介面。讓 Lync 2013 與 Lync 2010 用戶端能夠在外部順利完成自動設定所需。必要時，重複用於含有 Lync 啟用之使用者的所有 SIP 網域。</p></td>
</tr>
<tr class="odd">
<td><p>外部 DNS/SRV/5061</p></td>
<td><p>_sipfederationtls._tcp.contoso.com</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>Access Edge Service 外部介面。DNS 自動探索同盟合作夥伴 (亦稱為「允許的 SIP 網域」，先前版本稱為增強型同盟) 所需。必要時，重複用於含有 Lync 啟用之使用者的所有 SIP 網域</p></td>
</tr>
<tr class="even">
<td><p>內部 DNS/A</p></td>
<td><p>lsedge.contoso.net</p></td>
<td><p>172.25.33.10 與 172.25.33.11</p></td>
<td><p>合併 Edge 內部介面</p></td>
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
<td><p>SIP Access Edge Service 外部介面。DNS 自動探索同盟合作夥伴 (亦稱為「允許的 SIP 網域」，先前版本稱為增強型同盟) 所需。</p>
<div>

> [!IMPORTANT]   
> 必要時，重複用於含有 Lync 啟用的使用者及使用 推播通知服務或 Apple 推播通知服務的 Microsoft Lync Mobile 用戶端的所有 SIP 網域


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
<td><p>Access Edge Service 外部介面 (Contoso) 必要時，重複用於含有 Lync 啟用之使用者的所有 SIP 網域</p></td>
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
<td><p>Access Edge Service 或 Edge 集區的 XMPP Proxy 外部介面。必要時，重複用於含有 Lync 啟用之使用者的所有內部 SIP 網域，藉由全域原則、使用者所在網站的原則，或是 Lync 啟用的使用者套用的使用者原則，透過外部存取原則的設定，允許前述使用者與 XMPP 連絡人連絡。您也必須在 XMPP 同盟合作夥伴原則中設定允許的 XMPP 網域。如需詳細資訊，請參閱＜另請參閱＞ 中的主題</p></td>
</tr>
<tr class="even">
<td><p>外部 DNS/A</p></td>
<td><p>xmpp.contoso.com (範例)</p></td>
<td><p>裝載 XMPP Proxy 的 Edge Server 或 Edge 集區上的 Access Edge Service IP 位址</p></td>
<td><p>指向裝載 XMPP Proxy 服務的 Access Edge Service 或 Edge 集區。一般而言，您所建立的 SRV 記錄將指向此主機 (A 或 AAAA) 記錄</p></td>
</tr>
</tbody>
</table>

