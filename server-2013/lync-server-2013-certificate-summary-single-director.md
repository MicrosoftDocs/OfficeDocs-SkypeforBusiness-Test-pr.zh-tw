---
title: Lync Server 2013：憑證摘要 - 單一 Director
TOCTitle: 憑證摘要 - 單一 Director
ms:assetid: 1b769a76-cbf3-46e9-a955-f6cde5faff93
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204720(v=OCS.15)
ms:contentKeyID: 49290256
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的憑證摘要 - 單一 Director

 

_**上次修改主題的時間：** 2015-03-09_

單一 Director 的憑證需求包含預設憑證，其中具備 Director 可擷取之服務的主體名稱和主體替代名稱。此外，還包含用於伺服器對伺服器驗證所需的 OAuth Token 憑證。

### Director 的憑證

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
<th>主體名稱 (SN)</th>
<th>主體替代名稱 (SAN)</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>預設</p></td>
<td><p>dir01.contoso.net</p></td>
<td><p>dir01.contoso.net</p>
<p>dialin.contoso.com</p>
<p>meet.contoso.com</p>
<p>lyncdiscoverinternal.contoso.com</p>
<p>lyncdiscover.contoso.com</p>
<p>(選用) *.contoso.com</p></td>
<td><p>可向內部管理的憑證授權單位 (CA) 或公用 CA 要求 Director 憑證。</p>
<p>Director 會回應周邊中的反向 Proxy 或 Edge Server 所發出的要求。內部用戶端將不使用 Director。</p>
<p>或者，簡單 URL 的萬用字元項目</p></td>
</tr>
<tr class="even">
<td><p>OAuthTokenIssuer</p></td>
<td><p>dir01.contoso.net</p></td>
<td><p>無項目</p></td>
<td><div class="alert">
> [!IMPORTANT]  
> 請注意，雖然最小金鑰長度是 1024，但是您可能會收到警告表示建議最小金鑰長度為 2048 位元。


</div>
<p>OAuthTokenIssuer 憑證是單一目的憑證，用於驗證大規模環境中的伺服器，且可向內部 CA 或公用 CA 要求。此憑證為必要。</p>
<p></p></td>
</tr>
</tbody>
</table>

