---
title: 常設聊天室伺服器的 DNS 需求
TOCTitle: 常設聊天室伺服器的 DNS 需求
ms:assetid: f7531374-d7ed-4b63-ae81-02294cb4496a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205391(v=OCS.15)
ms:contentKeyID: 49292849
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 常設聊天室伺服器的 DNS 需求

 

_**上次修改主題的時間：** 2015-03-09_

本節描述部署 常設聊天室伺服器 所需的網域名稱系統 (DNS) 記錄。

## Persistent Chat Server 的 DNS 記錄

下表指定 常設聊天室伺服器 部署的 DNS 需求。

### Persistent Chat Server 的 DNS 需求

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
<td><p>一部 Persistent Chat Server</p></td>
<td><p>一筆內部 A 記錄，用來將伺服器的完整網域名稱 (FQDN) 解析為 IP 位址。</p></td>
</tr>
<tr class="even">
<td><p>Persistent Chat 集區</p></td>
<td><p>一筆內部 A 記錄，用來將伺服器的完整網域名稱 (FQDN) 解析為 IP 位址。</p>
<p><strong>範例</strong></p>
<p>PersistentChatServer01.contoso.com     10.10.10.1</p>
<p>PersistentChatServer02.contoso.com     10.10.10.2</p>
<p>一筆內部 A 記錄，用來將伺服器的完整網域名稱 (FQDN) 解析為 IP 位址。</p>
<p><strong>範例</strong></p>
<p>PersistentChatPool.contoso.com    10.10.10.1</p>
<p>PersistentChatPool.contoso.com    10.10.10.2</p></td>
</tr>
</tbody>
</table>

