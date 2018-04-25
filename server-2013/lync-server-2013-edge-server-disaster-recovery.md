---
title: Lync Server 2013：Edge Server 災害復原
TOCTitle: Edge Server 災害復原
ms:assetid: 05ec8d26-d167-4a6f-a966-a1f8873cf974
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ687960(v=OCS.15)
ms:contentKeyID: 49889926
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Edge Server 災害復原

 

_**上次修改主題的時間：** 2014-03-12_

如同其他伺服器角色，為 Edge Server 提供高可用性的最佳作法，是在每個網站的集區中部署多部 Edge Server。如果其中一部 Edge Server 中斷連線，集區中的其他伺服器將會繼續提供 Edge Service。

若要啟用嚴重損壞修復程序，您必須將在不同的網站上部署個別 Edge Server 集區。您不需要像是對前端集區一樣，明確將 Edge 集區配對在一起，但是具有多個 Edge 集區仍可在一整個 Edge 集區中斷連線時，提供可用的集區繼續執行作業。下列各節提供各種 Edge Server 功能之嚴重損壞修復的詳細資訊。

## 遠端存取

如果您有多個網站且每個網站備有一個 Edge Server 集區，當一整個 Edge 集區失敗時，遠端存取服務將會繼續運作，而不需要系統管理員採取任何動作。當在其他網站建立 Edge 集區時，您無法使用相同的 FQDN。每個 Edge 集區都必須有唯一的 FQDN (內部與外部)。Edge 集區不會使用反向 Proxy 發行規則來與前端伺服器交談。當用戶端重新查詢遠端存取 DNS 服務記錄時，便會發生自動容錯移轉，並且會將遠端使用者傳送至其他網站中的 Edge 伺服器。用戶端會根據 DNS SRV 記錄的優先順序嘗試每個外部 Edge FQDN。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要順利完成容錯移轉，請確保防火牆允許來自每個集區的前端伺服器與所有 Edge Server 通訊。</td>
</tr>
</tbody>
</table>


## 同盟

對於和執行 Lync Server 的其他組織之間的同盟關係，只要您已在 SRV 記錄中將各Edge 集區設定為不同的優先順序，輸入同盟要求就會繼續運作。任何傳送到已關閉 Edge 集區的同盟要求都會容錯回復，然後連線至正在執行的 Edge 集區。

輸出同盟一律透過組織中一部已發行的 Edge 集區或 Edge Server 來設定。如果此 Edge 集區中斷連線，則必須使用拓撲產生器，變更輸出同盟路由以使用仍在執行的 Edge 集區。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中容錯移轉用於 Lync Server 同盟的 Edge 集區](lync-server-2013-failing-over-the-edge-pool-used-for-lync-server-federation.md)＞。

## XMPP 同盟

以 XMPP 同盟來說，當指定為 XMPP 同盟閘道的 Edge 集區中斷連線時，輸出及輸入流量都會失敗。若要讓 XMPP 同盟恢復運作，您必須變更 XMPP 同盟以使用其他 Edge 集區。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中容錯移轉用於 XMPP 同盟的 Edge 集區](lync-server-2013-failing-over-the-edge-pool-used-for-xmpp-federation.md)＞。

## Edge 集區失敗但前端集區仍在執行中

如果某個網站上的 Edge 集區失敗，但是該網站上的前端集區仍在執行中，您必須在第一個 Edge 集區中斷連線時，變更前端集區使用其他網站上不同的 Edge 集區。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中變更與前端集區相關聯的 Edge 集區](lync-server-2013-changing-the-edge-pool-associated-with-a-front-end-pool.md)＞。

