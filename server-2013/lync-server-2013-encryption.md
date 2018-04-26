---
title: Lync Server 2013 的加密
TOCTitle: Lync Server 2013 的加密
ms:assetid: d18c74a6-385b-407b-98eb-0d525fa38fea
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn481135(v=OCS.15)
ms:contentKeyID: 59679128
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 的加密

 

_**上次修改主題的時間：** 2015-03-09_

Microsoft Lync Server 2013 使用 TLS 和 MTLS 來加密立即訊息。所有伺服器對伺服器的流量，不論流量是設定在內部網路或可跨過內部網路周邊，都需要 MTLS。TLS 是選用項目，但強烈建議在中繼伺服器與媒體閘道之間使用。若此連結上有設定 TLS，則需要 MTLS。因此，閘道必須設定有受 中繼伺服器 信任之 CA 所發出的憑證。

用戶端對用戶端流量的需求是根據流量是否通過內部企業防火牆而定。嚴格內部流量可以使用 TLS (此時即時訊息會經過加密)，或者使用 TCP (此時就不會加密)。

下表摘要說明每一種流量類型的通訊協定需求。

### 流量保護

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>流量類型</th>
<th>提供保護的通訊協定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>伺服器對伺服器</p></td>
<td><p>MTLS</p></td>
</tr>
<tr class="even">
<td><p>用戶端對伺服器</p></td>
<td><p>TLS</p></td>
</tr>
<tr class="odd">
<td><p>立即訊息和目前狀態</p></td>
<td><p>TLS (若針對 TLS 設定)</p></td>
</tr>
<tr class="even">
<td><p>音訊和視訊及媒體的桌面共用</p></td>
<td><p>SRTP</p></td>
</tr>
<tr class="odd">
<td><p>桌面共用 (訊號)</p></td>
<td><p>TLS</p></td>
</tr>
<tr class="even">
<td><p>Web 會議</p></td>
<td><p>TLS</p></td>
</tr>
<tr class="odd">
<td><p>會議內容下載、通訊錄下載、通訊群組擴充</p></td>
<td><p>HTTPS</p></td>
</tr>
</tbody>
</table>


## 媒體加密

媒體流量都是使用安全 RTP (SRTP) 加密，它是即時傳輸通訊協定 (RTP) 的設定檔，為 RTP 流量提供機密性、驗證功能和重播攻擊防護。SRTP 使用媒體轉送驗證服務所產生的工作階段金鑰，以回應伺服器要求的成功驗證 (代表媒體參與者)。工作階段金鑰受交涉的使用者名稱和密碼保護，會由 前端伺服器 呈現給媒體轉送服務驗證，並透過受 TLS 防護的 SIP 通道傳送給參與者。工作階段金鑰以媒體轉送服務使用的使用者名稱和密碼來將受保護的工作階段金鑰解密，並借助參與者的 TLS 憑證和受保護的 SIP 通道，以安全的方法來提供，可讓參與者將 SRTP 資料流解密。此外，在中繼伺服器及其內部下一個躍點之間往返流動的媒體也是使用 SRTP 加密。在中繼伺服器與媒體閘道之間往返流動的媒體並未加密。中繼伺服器可支援媒體閘道加密，但是閘道必須支援 MTLS 和憑證存放。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>新版 Windows Live Messenger 可支援音訊/視訊 (A/V)。若您搭配 Windows Live Messenger 實作 A/V 同盟，也必須修改 Lync Server 加密層級。根據預設，加密層級為 [必要]。您必須使用 Lync Server 管理命令介面 將此設定變更為 [支援]。若需更多資訊，請參閱＜部署＞文件中的<a href="lync-server-2013-deploying-external-user-access.md">在 Lync Server 2013 中部署外部使用者存取</a>。</td>
</tr>
</tbody>
</table>


Microsoft Lync 2013 與 Windows Live 用戶端之間的音訊和視訊媒體流量並未加密。

## FIPS

若 Windows Server 作業系統的系統密碼編譯是設定為使用 FIPS 140-2 演算法，則 Lync Server 2013 與 Microsoft Exchange Server 2013 運作時會支援聯邦資訊處理標準 (FIPS) 140-2 演算法。若要實作 FIPS 支援，您必須設定執行 Lync Server 2013 的每個伺服器，才能支援。若需使用 FIPS 相容演算法與如何實作 FIPS 支援的詳細資料，請參閱 Microsoft 知識庫文章 811833＜在 Windows XP 及更新版本的 Windows 上啟用 \[系統加密編譯: 使用 FIPS 相容演算法於加密，雜湊，以及簽章\] 安全性設定的效果＞(機器翻譯)，網址為：[http://go.microsoft.com/fwlink/p/?linkid=3052\&kbid=811833](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=811833)。若需 FIPS 140-2 支援與 Exchange 2010 中限制的詳細資訊，請參閱＜Exchange 2010 SP1 與對 FIPS 相容演算法的支援＞(英文)，網址為：[http://go.microsoft.com/fwlink/p/?LinkId=205335](http://go.microsoft.com/fwlink/p/?linkid=205335)。

