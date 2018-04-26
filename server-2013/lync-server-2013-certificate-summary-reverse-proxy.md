---
title: Lync Server 2013：憑證摘要 - 反向 Proxy
TOCTitle: 憑證摘要 - 反向 Proxy
ms:assetid: f2b9a53f-aead-413d-81e9-4a294a010fbb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205381(v=OCS.15)
ms:contentKeyID: 49292784
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的憑證摘要 - 反向 Proxy

 

_**上次修改主題的時間：** 2015-03-09_

反向 Proxy 的憑證需求比 Edge Server 的憑證需求簡單。提供的流程圖顯示必要的需求。隨附的表格顯與已在 Edge Server 討論中提及之相關案例相關的示一般的憑證主體名稱和主體替代名稱。如需 Edge Server 案例的詳細資訊，請參閱 [Lync Server 2013 中的外部使用者存取案例](lync-server-2013-scenarios-for-external-user-access.md)。

**反向 Proxy 的憑證流程圖**

![Edge Server 的憑證流程圖](images/JJ205381.026045d7-1b4b-4651-b32f-2d43a7161198(OCS.15).jpg "Edge Server 的憑證流程圖")

### 反向 Proxy：外部介面

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>元件</th>
<th>主體名稱</th>
<th>主體替代名稱 (SAN)/順序</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>反向 Proxy</p></td>
<td><p>webext.contoso.com</p></td>
<td><p>webext.contoso.com</p>
<p>webdirext.contoso.com</p>
<p>dialin.contoso.com</p>
<p>meet.contoso.com</p>
<p>officewebapps01.contoso.com</p>
<p>lyncdiscover.contoso.com</p>
<p>(選擇性)：*.contoso.com</p></td>
<td><p>必須由公開 CA 發行憑證，並連同伺服器 EKU 發行。服務包含通訊錄服務、適用於會議的通訊群組擴充 Office Web Apps 及 Lync IP 裝置發行規則。主體替代名稱包括：</p>
<ul>
<li><p>前端伺服器 或 前端集區 的外部 Web 服務 FQDN</p></li>
<li><p>Director 或 Director 集區的外部 Web 服務 FQDN</p></li>
<li><p>電話撥入式會議</p></li>
<li><p>線上會議發行規則</p></li>
<li><p>適用於會議的 Office Web Apps</p></li>
<li><p>Lyncdiscover (自動探索)</p></li>
</ul>
<p>選用萬用字元會取代 meet 和 dialin SAN</p></td>
</tr>
</tbody>
</table>

