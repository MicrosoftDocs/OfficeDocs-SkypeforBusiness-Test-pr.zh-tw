---
title: Lync Server 2013：DNS 摘要 - 調整式合併 Edge (利用硬體負載平衡器)
TOCTitle: DNS 摘要 - 調整式合併 Edge (利用硬體負載平衡器)
ms:assetid: 8453297c-da1d-4b9e-a37e-6721458c6feb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398670(v=OCS.15)
ms:contentKeyID: 49291526
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 DNS 摘要 - 調整式合併 Edge (利用硬體負載平衡器)

 

_**上次修改主題的時間：** 2015-03-09_

與憑證及連接埠的 DNS 記錄需求相比， Lync Server 2013 的遠端存取對 DNS 記錄需求則相對簡單許多。此外，依據您設定執行 Lync 2013 的用戶端以及是否啟用同盟關係而定，許多記錄都是選用的。

如需 Lync 2013 DNS 需求的詳細資訊，請參閱＜ [針對 Lync Server 2013 判定 DNS 需求](lync-server-2013-determine-dns-requirements.md)＞。

如需在 split-brain DNS 尚未設定之情況下設定 Lync 2013 用戶端自動設定的詳細資訊，請參閱＜ [針對 Lync Server 2013 判定 DNS 需求](lync-server-2013-determine-dns-requirements.md)＞的＜不透過 Split Brain DNS 執行的自動設定＞一節。

下表含有支援「調整式合併邊緣拓撲 (硬體負載平衡)」圖表所需的 DNS 記錄摘要。請注意，只有當 Lync 用戶端進行自動設定時，才需要特定 DNS 記錄。如果您打算使用群組原則物件 (GPO) 來設定 Lync 用戶端，則不需要關聯的記錄。

## 重要： Edge Server 網路介面卡需求

若要避免路由問題，請確認您的 Edge Server 中至少有兩個網路介面卡，且預設閘道僅在網路介面卡上設定與外部介面卡相關聯。例如，在 [Lync Server 2013 中含硬體負載平衡器的調整式合併 Edge](lync-server-2013-scaled-consolidated-edge-with-hardware-load-balancers.md) 的「調整式合併 Edge」情況中，預設閘道指向外部防火牆。

您可以在每部 Edge Server 中設定兩片網路介面卡，如下所示： UNRESOLVED\_TOKEN\_VAL()

  - **網路介面卡 1 (內部介面)**
    
    已指派 172.25.33.10 的內部介面。
    
    無預設閘道。
    
    請確定從內含 Edge Server 內部介面的網路，到內含 Lync Server 用戶端或執行 Lync Server 的伺服器所屬網路之間 (例如，從 172.25.33.0 到 192.168.10.0) 存在路由。

  - **網路介面卡 2 (外部介面)**
    
    三個公開 IP 位址會被指派到這個網路介面卡，例如 131.107.155.10 用於 Access Edge Service，131.107.155.20 用於 Web Conferencing Edge Service，131.107.155.30 用於 A/V Edge 服務。
    
    > [!NOTE]  
    > 指派至 Edge Server 實際外部網路介面的 IP 位址視您選擇的硬體負載平衡而訂。請參閱硬體負載平衡器的文件，以了解實際 IP 位址需求。<br />
    > 上述的三個 Edge Service 介面確實能夠使用單一 IP 位址 (但不建議這樣做)。這樣做，雖能節省 IP 位址，但每個服務都要有不同的連接埠號碼。預設連接埠號碼為 443/TCP，其可確保大部分遠端防火牆均允許流量通過。將連接埠值變更為 (例如) 5061/TCP 以用於 Access Edge Service、444/TCP 以用於 Web Conferencing Edge Service 以及 443/TCP 以用於 A/V Edge 服務，可能會對遠端使用者造成問題，因為其防火牆不允許來自 5061/TCP 與 444/TCP 的流量通過。此外，由於能夠根據 IP 位址進行篩選，這三個不同的 IP 位址可讓疑難排解變得更輕鬆。
    
    Access Edge Service IP 位址為主要位址，且其預設閘道將設為整合式路由器 (131.107.155.1)。
    
    Web Conferencing Edge Service與 A/V Edge 服務 IP 位址為次要位址。

> [!TIP]
> 設定 Edge Server 使用兩片網路介面卡是兩個選項之一。另一個選項是使用一片網路介面卡供內部使用，並使用三個網路介面卡供 Edge Server 的外部使用。這個選項的主要優點是每個 Edge Server Service 都有一片不同的網路介面卡，而且能夠在疑難排解時更簡潔地收集資料。


### 調整式合併邊緣所需的 DNS 記錄，硬體負載平衡 (範例)

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
<td><p>Access Edge Service 外部介面 (Contoso)。視需要對於有 Lync 啟用的使用者包含在其中的所有 SIP 網域重複進行</p></td>
</tr>
<tr class="even">
<td><p>外部 DNS/A</p></td>
<td><p>webcon.contoso.com</p></td>
<td><p>131.107.155.20</p></td>
<td><p>Web Conferencing Edge Service 外部介面</p></td>
</tr>
<tr class="odd">
<td><p>外部 DNS/A</p></td>
<td><p>av.contoso.com</p></td>
<td><p>131.107.155.30</p></td>
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
<td><p>SIP Access Edge Service 外部介面。DNS 自動探索同盟合作夥伴 (亦稱為「允許的 SIP 網域」，先前版本稱為增強型同盟) 所需。視需要對於有 Lync 啟用的使用者以及使用 推播通知服務 或 Apple 推播通知服務的 Microsoft Lync Mobile 用戶端包含在其中的所有 SIP 網域重複進行</p></td>
</tr>
<tr class="even">
<td><p>內部 DNS/A</p></td>
<td><p>lsedge.contoso.net</p></td>
<td><p>172.25.33.10</p></td>
<td><p>合併 Edge 內部介面</p></td>
</tr>
</tbody>
</table>

