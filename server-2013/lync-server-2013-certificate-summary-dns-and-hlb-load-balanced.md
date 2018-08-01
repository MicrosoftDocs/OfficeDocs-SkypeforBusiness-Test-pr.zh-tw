---
title: Lync Server 2013：憑證摘要 - DNS 與 HLB 負載平衡
TOCTitle: 憑證摘要 - DNS 與 HLB 負載平衡
ms:assetid: 8318a1a4-b423-47b7-95e6-9541adfad391
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205047(v=OCS.15)
ms:contentKeyID: 49291512
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的憑證摘要 - DNS 與 HLB 負載平衡

 

_**上次修改主題的時間：** 2015-03-09_

對於包含 DNS 負載平衡和硬體負載平衡器的 Director，憑證需求將使用預設的憑證，其中含有 Director 可擷取的服務所用的主體名稱和主體別名。對會對集區中的各個 Director 要求憑證。必須注意的是，硬體負載平衡器僅對於來自反向 Proxy 的流量進行負載平衡。此外，各個伺服器上安裝的 OAuth 語彙基元憑證可用於伺服器對伺服器驗證用途。

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
<td><p>dirpool01.contoso.net</p></td>
<td><p>dirpool01.contoso.net</p>
<p>dir01.contoso.net</p>
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
<td><div>

> [!IMPORTANT]  
> 請注意，雖然最小金鑰長度是 1024，但是您可能會收到警告表示建議最小金鑰長度為 2048 位元。


</div>
<p>OAuthTokenIssuer 憑證是單一目的憑證，用於驗證大規模環境中的伺服器，且可向內部 CA 或公用 CA 要求。此憑證為必要。</p></td>
</tr>
</tbody>
</table>

