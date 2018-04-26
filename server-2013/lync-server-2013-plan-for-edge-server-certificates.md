---
title: Lync Server 2013：規劃 Edge Server 憑證
TOCTitle: 規劃 Edge Server 憑證
ms:assetid: f1dfe220-2398-4ac8-ba4c-206c8c0cbc50
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413010(v=OCS.15)
ms:contentKeyID: 49292786
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中規劃 Edge Server 憑證

 

_**上次修改主題的時間：** 2012-11-05_

Edge 的憑證建立作業已在 Lync Server 2013 中簡化。

**Edge Server 的憑證流程圖**

![憑證流程圖](images/Gg413010.a5fc20db-7ced-4364-b577-6a709a8367cd(OCS.15).jpg "憑證流程圖")

建立單一共用憑證，確定您有針對憑證定義的可匯出私密金鑰，並使用憑證精靈將它指派至下列 Edge Server 外部介面：

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lync Server 不支援萬用字元憑證，以反向 Proxy 摘要簡單 URL 除外。您必須針對每個 SIP 網域名稱、 Web Conferencing Edge Service、 A/V Edge 服務 以及部署所提供的 XMPP 網域定義不同的主體替代名稱 (SAN)。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>由 Lync Server 2013 引入，在目前憑證到期前先進行「音訊/視訊驗證」憑證，必須要另行規劃。您會需要兩個憑證，一個指派至 Access Edge Service 與 Web Conferencing Edge Service，另一個指派至 A/V Edge 服務；而非一個憑證適用於多個外部 Edge 介面。如需詳細資訊，請參閱 <a href="lync-server-2013-staging-av-and-oauth-certificates-using-roll-in-set-cscertificate.md">於 Set-CsCertificate 使用 -Roll 以預備 Lync Server 2013 中的 AV 與 OAuth 憑證</a></td>
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
<td>在 Edge Server 集區的事件中，您要將具私密金鑰的憑證匯出至每個 Edge Server，並將憑證至派至每個 Edge Server 服務。內部 Edge Server 憑證的做法也相同，將具私密金鑰的憑證匯出並指派至每個內部 Edge 介面。</td>
</tr>
</tbody>
</table>


  - 請確定憑證有指派可匯出的私密金鑰

  - Access Edge Service (在憑證精靈中稱為 \[SIP Access Edge 外部\] )

  - Web Conferencing Edge Service (在憑證精靈中稱為 \[Web 會議 Edge 外部\] )

  - A/V 驗證服務 (在憑證精靈中稱為 \[A/V Edge 外部\] )

建立具可匯出私密金鑰的單一內部憑證，並將它複製與指派至每個 Edge Server 內部介面：

  - Edge Server (在憑證精靈中稱為 \[Edge 內部\] )

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在每個 Edge Server 服務中可使用分開且不同的憑證。選擇分開憑證主要是因為您可在 A/V Edge 服務 憑證上使用新推出的憑證功能。在這種情況下，建議從 Access Edge Service 與 Web Conferencing Edge Service 中減少 A/V Edge 服務 憑證。如果您選擇每個服務都必須有、取得及指派分開的憑證，必須可匯出 A/V Edge 服務 的私密金鑰 (再強調一次，這實際上就是「A/V 驗證」服務)，並在每個 Edge Server 上將相同的憑證指派至「A/V Edge 外部」介面。</td>
</tr>
</tbody>
</table>


## 請參閱

#### 工作

[於 Set-CsCertificate 使用 -Roll 以預備 Lync Server 2013 中的 AV 與 OAuth 憑證](lync-server-2013-staging-av-and-oauth-certificates-using-roll-in-set-cscertificate.md)  

#### 概念

[在 Lync Server 2013 中會影響 Edge Server 規劃的變更](lync-server-2013-changes-in-lync-server-that-affect-edge-server-planning.md)

