---
title: Lync Server 2013：Standard Edition Server 的 DNS 需求
TOCTitle: Standard Edition Server 的 DNS 需求
ms:assetid: 5d1daf54-6e60-4ce0-9254-7d57a0835fa4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204936(v=OCS.15)
ms:contentKeyID: 49291052
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中 Standard Edition Server 的 DNS 需求

 

_**上次修改主題的時間：** 2015-03-09_

本節說明 Standard Edition Server 部署所需的網域名稱系統 (DNS) 記錄。

## Standard Edition Server 的 DNS 記錄

下表指出 Lync Server 2013 Standard Edition Server 部署的 DNS 需求。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>部署案例</th>
<th>DNS 需求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Standard Edition 伺服器</p></td>
<td><p>一筆內部 A 記錄，用來將伺服器的完整網域名稱 (FQDN) 解析為 IP 位址。</p></td>
</tr>
<tr class="even">
<td><p>自動用戶端登入</p></td>
<td><p>每個受支援的 SIP 網域，皆需一筆 _sipinternaltls._tcp.&lt;domain&gt; (透過連接埠 5061) 的 SRV 記錄，對應到用以驗證並重新導向用戶端登入要求的 Standard Edition Server FQDN。如需詳細資訊，請參閱＜<a href="lync-server-2013-dns-requirements-for-automatic-client-sign-in.md">Lync Server 2013 中的自動用戶端登入的 DNS 需求</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p>整合通訊 (UC) 裝置的裝置更新 Web 服務探索</p></td>
<td><p>一筆名稱為 ucupdates-r2.&lt;SIP domain&gt; 的內部 A 記錄，解析為裝載 [裝置更新] Web 服務之 Standard Edition Server 的 IP 位址。在 UC 裝置已開啟，但尚未有使用者登入裝置的情況下，此 A 記錄會允許裝置去探索裝載著 [裝置更新] Web 服務的伺服器並取得更新。否則，裝置會透過使用者首次登入時的頻內佈建取得伺服器資訊。如需詳細資訊，請參閱作業文件中的＜<a href="lync-server-2013-device-update-web-service.md">Lync Server 2013 中的裝置更新 Web 服務</a>＞。</p></td>
</tr>
<tr class="even">
<td><p>支援 HTTP 流量的反向 Proxy</p></td>
<td><p>一筆外部 A 記錄，將外部 Web 伺服陣列 FQDN 解析為反向 Proxy 的外部 IP 位址。 用戶端和 UC 裝置會使用這個記錄來連線至反向 Proxy。如需詳細資訊，請參閱規劃文件中的 <a href="lync-server-2013-determine-dns-requirements.md">針對 Lync Server 2013 判定 DNS 需求</a>。</p></td>
</tr>
</tbody>
</table>


## 請參閱

#### 概念

[Lync Server 2013 中的自動用戶端登入的 DNS 需求](lync-server-2013-dns-requirements-for-automatic-client-sign-in.md)  
[針對 Lync Server 2013 判定 DNS 需求](lync-server-2013-determine-dns-requirements.md)  

#### 其他資源

[Lync Server 2013 中的裝置更新 Web 服務](lync-server-2013-device-update-web-service.md)

