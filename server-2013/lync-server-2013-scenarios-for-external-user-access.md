---
title: Lync Server 2013：外部使用者存取案例
TOCTitle: 外部使用者存取案例
ms:assetid: 25697446-b045-4d12-9b1c-47f694b4f224
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425727(v=OCS.15)
ms:contentKeyID: 49290359
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的外部使用者存取案例

 

_**上次修改主題的時間：** 2015-03-09_

若要供外部使用者存取 Lync Server 2013，您需要在周邊網路中部署至少一部 Edge Server 和一個反向 Proxy。您也可以選用在內部網路部署 Director 或 Director 集區。

如果您需要的容量超過一部 Edge Server 可以提供的容量，或是您的 Edge Server 部署需要高可用性，則可設定負載平衡並在負載平衡集區中部署多部 Edge Server。如果組織擁有多個資料中心，您可在多個位置進行 Edge Server 或 Edge 集區部署。不過，只有一個 Edge Server 部署可以被指定為同盟路由。

本節會定義 Edge Server 部署並將其對應於可能案例的規劃章節。例如，若您的部署需要高可用性、與可延伸訊息和顯示狀態通訊協定 (XMPP) 連絡人的同盟以及 Lync 行動性，您應選取下表中可符合這些需求的相符項目，並使用參考的規劃章節來定義您的部署，如下列流程圖所示。

**Edge Server 部署案例選擇程序**

![範例部署流程圖](images/Gg425727.007100b5-6923-4909-bfd7-897d8867205f(OCS.15).jpg "範例部署流程圖")

使用此程序，您可規劃並記錄所有您打算為使用者部署的功能設定。不過，在您部署 Edge Server 並確認正確的作業與新增其他功能之後，還可以新增同盟和 Mobility Service。部署章節中涵蓋了新增功能至現有 Edge Server 部署的程序。如需部署的詳細資訊，請參閱＜ [在 Lync Server 2013 中部署外部使用者存取](lync-server-2013-deploying-external-user-access.md)＞。藉由在初始規劃程序期間包含這些功能的規劃，您就可以準備 DNS、防火牆和新增功能的憑證需求，以讓您事先取得憑證並設定 DNS 和連接埠/通訊協定需求。

> [!TIP]
> 若您打算安裝 Edge Server 和反向 Proxy，然後再新增功能 (例如，同盟和行動性)，請在部署之後判斷所有服務需要的憑證。不論初始部署與否，若您能事先規劃並取得所有功能的憑證，就可以避免為了滿足同盟需求 (針對 Edge Server) 或反向 Proxy (針對 Mobility Service) 還得要求新憑證的麻煩。


> [!NOTE]  
> 所有 Edge Service 都會在每一部 Edge Server 上執行。不能將服務分割到兩個不同的 Edge Server。如果您部署 Edge 集區以提供延展性，所有 Edge Service 都將部署在集區的每一部 Edge Server 上。XMPP 同盟、 Office Communications Server 和 Lync Server 同盟、公用 IM 連線以及用戶端行動性都是額外的服務，其都可在您部署 Edge Server 或 Edge 集區之後才部署。Mobility Service 是一種使用反向 Proxy 的功能。安裝 Mobility Service 並不會新增功能至 Edge Server，但需要重新設定反向 Proxy。 <strong>「安裝目標」</strong>欄會列出這些功能，並可提供 <strong>「Edge Server 規劃章節」</strong>下方之關聯欄位中的規劃指導方針，以在安裝並設定 Edge Server 時同步規劃這些要部署的功能。



## 識別並對應您的部署目標


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>安裝目標</th>
<th>Edge Server 規劃文件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>您已決定在您的基礎架構中，只需要一部 Edge Service 伺服器就足夠。您也打算要針對 Edge Server 外部介面使用私人 IP 位址，並使用 NAT 來面向網際網路。</p>
<p>若您要在周邊部署單一 Edge Server，請使用此規劃章節。您將使用指派給 Edge Server 的私人 IP 位址來部署 Edge Server，並使用 NAT 來提供網際網路之外部使用者所需的公用 IP 位址。</p></td>
<td><p><a href="lync-server-2013-single-consolidated-edge-with-private-ip-addresses-and-nat.md">Lync Server 2013 中的單一合併 Edge (利用私人 IP 位址及 NAT)</a></p></td>
</tr>
<tr class="even">
<td><p>您已決定在您的基礎架構中，只需要一部 Edge Service 伺服器就足夠。您也打算要針對 Edge Server 外部介面使用公用 IP 位址來面向網際網路。</p>
<p>若您要在周邊部署單一 Edge Server，請使用此規劃章節。您將使用指派給 Edge Server 的公用 IP 位址來部署 Edge Server。在此案例中，您不打算使用 NAT，而要使用路由傳送，且您要讓 Edge Server 的實際公用 IP 位址可供外部使用者連線使用。</p></td>
<td><p><a href="lync-server-2013-single-consolidated-edge-with-public-ip-addresses.md">Lync Server 2013 中的單一合併 Edge (利用公用 IP 位址)</a></p></td>
</tr>
<tr class="odd">
<td><p>您已決定 Edge Service 的高可用性對使用者來說非常重要，且您要在此集區內部署兩部以上的 Edge Server。您也打算要針對 Edge Server 外部介面使用私人 IP 位址，並使用 NAT 來面向網際網路。</p>
<p>若您要在周邊部署 Edge Server 集區，請使用此規劃章節。您將使用指派給 Edge Server 的私人 IP 位址來部署 Edge Server，並使用 DNS 負載平衡來分送整個集區的通訊。您將使用 NAT 來提供網際網路之外部使用者所需的公用 IP 位址。</p></td>
<td><p><a href="lync-server-2013-scaled-consolidated-edge-dns-load-balancing-with-private-ip-addresses-using-nat.md">Lync Server 2013 中的調整式合併 Edge (使用 NAT 透過私人 IP 位址進行 DNS 負載平衡)</a></p></td>
</tr>
<tr class="even">
<td><p>您已決定 Edge Service 的高可用性對使用者來說非常重要，且您要在此集區內部署兩部以上的 Edge Server。您也打算要針對 Edge Server 外部介面使用公用 IP 位址來面向網際網路。</p>
<p>若您要在周邊部署 Edge Server 集區，請使用此規劃章節。您將使用指派給 Edge Server 的公用 IP 位址來部署 Edge Server，並使用 DNS 負載平衡來分送整個集區的通訊。您不打算使用 NAT，而要使用路由傳送來提供網際網路之外部使用者所需的公用 IP 位址。</p></td>
<td><p><a href="lync-server-2013-scaled-consolidated-edge-dns-load-balancing-with-public-ip-addresses.md">Lync Server 2013 中的調整式合併 Edge (透過公用 IP 位址進行 DNS 負載平衡)</a></p></td>
</tr>
<tr class="odd">
<td><p>您已決定 Edge Service 的高可用性對使用者來說非常重要，且您要使用硬體負載平衡器在此集區內部署兩部以上的 Edge Server。</p>
<p>若您要在周邊部署 Edge Server 集區，請使用此規劃章節。您將使用指派給 Edge Server 的公用 IP 位址來部署 Edge Server，並使用硬體負載平衡器來分送整個集區的通訊。您不打算使用 NAT，而要使用路由傳送來提供網際網路之外部使用者所需的公用 IP 位址。</p></td>
<td><p><a href="lync-server-2013-scaled-consolidated-edge-with-hardware-load-balancers.md">Lync Server 2013 中含硬體負載平衡器的調整式合併 Edge</a></p></td>
</tr>
<tr class="even">
<td><p>您可使用同盟案例來規劃可擴充與使用者進行通訊之協力廠商類型的功能。</p>
<ul>
<li><p>Lync Server 同盟</p></li>
<li><p>Office Communications Server 同盟</p></li>
<li><p>公用 IM 連線</p></li>
<li><p>XMPP 同盟</p></li>
</ul></td>
<td><p>規劃同盟案例</p>
<ul>
<li><p><a href="lync-server-2013-planning-for-lync-server-and-office-communications-server-federation.md">規劃 Lync Server 與 Office Communications Server 同盟</a></p></li>
<li><p><a href="lync-server-2013-planning-for-public-instant-messaging-connectivity.md">規劃 Lync Server 2013 中的公用立即訊息連線</a></p></li>
<li><p><a href="lync-server-2013-planning-for-extensible-messaging-and-presence-protocol-xmpp-federation.md">規劃 Lync Server 2013 中的可延伸的訊息和顯示狀態通訊協定 (XMPP) 同盟</a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Mobility Service 是透過反向 Proxy 來提供的，其可確保外部使用者行動性，並部署在 前端伺服器或 前端集區上。您必須在反向 Proxy 上建立或修改現有的發行規則，以啟用外部使用者的 Mobility Service。</p></td>
<td><p><a href="lync-server-2013-planning-for-mobility.md">Lync Server 2013 中的行動規劃</a></p></td>
</tr>
</tbody>
</table>


> [!TIP]
> 在下列的「案例」章節中，包含參考架構、範例 DNS、連接埠/通訊協定定義以及憑證需求，另外也包括 DNS、連接埠/通訊協定定義以及憑證需求的圖表。圖表可提供便於您填入與傳送給其他團隊 (例如，組織的網路團隊、公開金鑰基礎架構團隊以及伺服器部署團隊) 的範本。圖表的目的主要是強化溝通，並確保與即將實際進行組態工作的人員能順利進行必要的 Edge Server 組態元素溝通事宜。建議您使用圖表以及關聯的參考架構來規劃部署。

