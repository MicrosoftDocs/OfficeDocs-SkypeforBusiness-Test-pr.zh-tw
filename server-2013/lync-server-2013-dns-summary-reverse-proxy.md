---
title: Lync Server 2013：DNS 摘要 - 反向 Proxy
TOCTitle: DNS 摘要 - 反向 Proxy
ms:assetid: 3073affa-4d92-4453-9974-3a82ca0c6445
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204781(v=OCS.15)
ms:contentKeyID: 49290490
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 DNS 摘要 - 反向 Proxy

 

_**上次修改主題的時間：** 2015-03-09_

您可以在反向 Proxy 上設定兩片網路介面卡，如下所示：

## 反向 Proxy 網路介面卡需求

  - **網路介面卡 1 (內部介面)** 範例
    
    已指派 172.25.33.40 的內部介面。
    
    未定義預設閘道。
    
    請確定從內含反向 Proxy 內部介面的網路，到內含 Lync Server前端集區伺服器之間 (例如，從 172.25.33.0 到 192.168.10.0) 存在路由。

  - **網路介面卡 2 (外部介面)** 範例
    
    至少指派一個公用 IP 位址給這個網路介面卡。
    
    已將閘道定義為指向您外部周邊中的路由器或整合式防火牆 (此範例中為 10.45.16.1)。

### 反向 Proxy 所需的 DNS 記錄

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
<th>IP 位址</th>
<th>對應至/註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>外部 DNS/A</p></td>
<td><p>webext.contoso.com</p></td>
<td><p>為對外發佈的資源指派聆聽程式</p></td>
<td><p>從內部部署到外部 Web 服務。您可為所有集區及單一伺服器，針對要使用此反向 Proxy，且具有已定義之外部 Web 服務的 SIP 網域，定義及建立其他記錄。</p></td>
</tr>
<tr class="even">
<td><p>外部 DNS/A</p></td>
<td><p>webdirext.contoso.com</p></td>
<td><p>為對外發佈的資源指派聆聽程式</p></td>
<td><p>您部署中 Director 或 Director 集區的外部 Web 服務。您可以盡可能地定義許多 Director，因為其他 SIP 可能會和不同的 Director 關聯。</p>
<div class="alert">

> [!IMPORTANT]  
> 為 Director 定義 DNS 記錄並發行 Director，並不屬於前端集區或 Director 決策。若您是使用 Director，就必須定義及發行 Director 及 前端集區外部 Web 服務。若已在拓撲中定義了 Director，請先指定要傳送至 Director 的流量類型 (用於驗證和其他使用者)。


</div></td>
</tr>
<tr class="odd">
<td><p>外部 DNS/A</p></td>
<td><p>dialin.contoso.com</p></td>
<td><p>為對外發佈的資源指派聆聽程式</p></td>
<td><p>電話撥入式會議已對外發行</p></td>
</tr>
<tr class="even">
<td><p>外部 DNS/A</p></td>
<td><p>meet.contoso.com</p></td>
<td><p>為對外發佈的資源指派聆聽程式</p></td>
<td><p>已對外發行會議</p></td>
</tr>
<tr class="odd">
<td><p>外部 DNS/A</p></td>
<td><p>officewebapps01.contoso.com</p></td>
<td><p>為 Office Web Apps Server 指派聆聽程式</p></td>
<td><p>已內部部署 Office Web Apps Server 或部署在周邊，且已發行供外部用戶端存取</p></td>
</tr>
<tr class="even">
<td><p>外部 DNS/A</p></td>
<td><p>lyncdiscover.contoso.com</p></td>
<td><p>為對外發佈的資源指派聆聽程式</p></td>
<td><p>外部發行之自動探索的 Lync Discover External 記錄，且包含行動、 Microsoft Lync Web App，以及排程器 Web App</p></td>
</tr>
</tbody>
</table>

