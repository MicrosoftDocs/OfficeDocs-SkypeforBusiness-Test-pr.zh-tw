---
title: 在 Lync Server 2013 中管理服務品質 (QoS)
TOCTitle: 在 Lync Server 2013 中管理服務品質 (QoS)
ms:assetid: ab1051c3-8380-4d72-86df-37a61b1e4a41
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg405409(v=OCS.15)
ms:contentKeyID: 49315245
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中管理服務品質 (QoS)

 

_**上次修改主題的時間：** 2013-11-07_

服務品質 (QoS) 是某些組織所使用的網路技術，可協助提供音訊與視訊通訊的最佳使用者經驗。QoS 最常用在頻寬有限的網路上：因為大量網路封包爭用相對少量的可用頻寬，服務品質可提供方法讓系統管理員指派較高的優先順序給附帶音訊或視訊資料的封包。藉由提供較高的優先順序給這些封包，相較於包含檔案傳輸、網頁瀏覽或資料庫備份這類的網路工作階段，音訊與視訊通訊就可以在較少的干擾之下更快地完成。這是因為用於檔案傳輸或資料庫備份的網路封包已指派「最佳」優先順序。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在一般的規則之下，服務品質只適用於您內部網路上的通訊工作階段。當您實作 QoS 時，您設定伺服器與路由器來支援封包標示； 然而，您必須以特定的方式設定這些裝置來支援封包標示。您不能假設可在網際網路或其他網路上支援服務品質。即使其他網路支援服務品質，也不保證 QoS 的設定方式會與在您網路上設定該服務的方式一樣。</td>
</tr>
</tbody>
</table>


Microsoft Lync Server 2013 不需要服務品質；若您目前未使用 QoS，在安裝 Lync Server 2013 前不需要安裝該服務。如果您遭遇網路的封包遺失，建議您新增額外的頻寬來減少此問題。若無法新增更多頻寬，則您可能會想要改為實作服務品質。

Lync Server 2013 提供完整的服務品質支援：這表示已經使用 QoS 的組織可輕鬆將 Lync Server 整合至現有的網路基礎結構中。若要這樣做，您必須執行下列作業：

  - [針對非 Windows 型裝置啟用 QoS](lync-server-2013-enabling-qos-for-devices-that-are-not-based-on-windows.md)。在執行其他作業系統的電腦與其他裝置上 (如 iPhone)，QoS 預設為停用。雖然您可以使用 Lync Server 來啟用與停用裝置的服務品質，但是通常無法使用該產品來修改這些裝置使用的 DSCP 程式碼。

  - [針對會議、應用程式及中繼伺服器設定連接埠範圍](lync-server-2013-configuring-port-ranges-for-your-conferencing-application-and-mediation-servers.md)。您必須保留一組唯一的連接埠供不同的封包類型使用，如音訊與視訊。使用 Lync Server 2013，您就不用藉由將屬性值設為 True 或 False 來啟用或停用服務品質。而是透過設定連接埠範圍，然後建立與套用群組原則來啟用服務品質。如果您之後決定不使用 QoS，只要將適當的群組原則物件移除，就可停用服務品質。

  - [設定 Edge Server 的連接埠範圍](lync-server-2013-configuring-port-ranges-for-your-edge-servers.md)。雖然不需要，但您還是可以設定 Edge Server 使用與其他伺服器相同的連接埠範圍。

  - [針對 Microsoft Lync 用戶端設定連接埠範圍](lync-server-2013-configuring-port-ranges-for-your-microsoft-lync-clients.md)。這些連接埠範圍只適用於用戶端電腦，且通常與伺服器上設定的連接埠範圍不同。

  - [在 Lync Server 2013 中針對會議、應用程式及中繼伺服器設定服務品質原則](lync-server-2013-configuring-a-quality-of-service-policy-for-your-conferencing-application-and-mediation-servers.md)。這些原則可判斷套用到不同封包類型的 DSCP 程式碼。

  - [為 A/V Edge Server 設定服務品質原則](lync-server-2013-configuring-a-quality-of-service-policy-for-your-a-v-edge-servers.md)。應只在您 Edge Server 的內部端進行。因為服務品質是設計在您的內部網路上使用，而非網際網路。

  - [針對 Windows 7 或 Windows 8 上執行的用戶端設定服務品質原則](lync-server-2013-configuring-quality-of-service-policies-for-clients-running-on-windows-7-or-windows-8.md)。請注意，Microsoft Lync Server 2013 不支援其他 Windows 作業系統的 QoS ，如 Windows Vista 或 Windows XP。

  - [設定 Microsoft Lync Phone Edition 裝置上的服務品質](lync-server-2013-configuring-quality-of-service-on-microsoft-lync-phone-edition-devices.md)。QoS 預設會為 Lync Phone Edition 裝置啟用。不過，您可能會想要變更預設的 DSCP 值，以確保組織中所有的音訊封包皆使用相同的 DSCP 程式碼。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若您使用 Microsoft Windows Server 2012 或 Windows Server 2012 R2，則可能會想瞭解如何使用新的 Windows PowerShell Cmdlet 集合，在該平台上管理服務品質。若需更多資訊，請參閱＜Windows PowerShell 中的網路服務品質 Cmdlet＞：<a href="http://go.microsoft.com/fwlink/p/?linkid=285379">http://go.microsoft.com/fwlink/p/?LinkId=285379</a>。</td>
</tr>
</tbody>
</table>

