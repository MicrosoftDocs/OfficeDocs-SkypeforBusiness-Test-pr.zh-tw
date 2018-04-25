---
title: 位置基礎路由與諮詢通話轉接
TOCTitle: 位置基礎路由與諮詢通話轉接
ms:assetid: b12460c2-36c8-481f-b867-fe10dc1c0bdf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362836(v=OCS.15)
ms:contentKeyID: 56269142
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 位置基礎路由與諮詢通話轉接

 

_**上次修改主題的時間：** 2015-03-09_

除了執行位置基礎路由至 Lync 會議以外，位置基礎路由會議應用程式還會在輸出至 PSTN 端點的諮詢通話轉接上執行位置基礎路由限制。諮詢通話轉接是指在建立於雙方之間的通話中，其中一方將通話轉接給新的使用者。例如，有個 PSTN 端點撥號給使用者 A (Lync 被呼叫者)。使用者 A 判定應將 PSTN 使用者轉接至使用者 B (Lync 使用者)。使用者 A 先保留與 PSTN 使用者的通話，然後撥號給使用者 B。使用者 B 同意與 PSTN 使用者通話後，使用者 A 將保留的通話轉接給使用者 B。

**諮詢通話轉接通話流程**

![會議圖表的以位置為基礎的路由](images/Dn362836.e4d43d6f-23d2-49c9-b12b-15248a743f92(OCS.15).jpg "會議圖表的以位置為基礎的路由")

當啟用位置基礎路由的使用者啟動 PSTN 端點的諮詢通話轉接 (如上圖所示) 時，會建立兩個作用中的通話：一個為 PSTN 使用者與 Lync 使用者 A 之間的通話，另一個則為 Lync 使用者 A 與 Lync 使用者 B 之間的通話。位置基礎路由會議應用程式會執行下列行為：

  - 若是路由 PSTN 通話的 SIP 主幹具備將 PSTN 通話重新路由至 Lync 使用者 B (即轉接目標) 所在網站的權限，則將允許通話轉接；否則諮詢通話轉接會遭到封鎖。若要執行這項權限，遭轉接方的所在位置必須與將作用中通話路由至 PSTN 端點之 SIP 主幹相同。

  - 若是路由傳入的 PSTN 通話的 SIP 主幹並無可將通話路由至遭轉接方 (Lync 使用者 B) 所在網站的權限，或遭轉接方位於未知網站時，則諮詢通話轉接至 PSTN 端點 (即通話轉接目標) 的作業將會遭到封鎖。

下表說明位置基礎路由會議應用程式如何針對諮詢通話轉接套用位置基礎路由限制。雖然 PBX 端點並非直接與網站建立關聯，但可將網站指派給 PBX 所連線的 SIP 主幹。因此，PBX 端點即可與網站有間接關聯。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>通話遭轉接方的網站</p></td>
<td><p>通話轉接目標的網站</p></td>
<td><p>行為</p></td>
</tr>
<tr class="even">
<td><p>PSTN 端點</p></td>
<td><p>相同網站的 Lync 使用者 (即網站 1)</p></td>
<td><p>允許諮詢轉接</p></td>
</tr>
<tr class="odd">
<td><p>PSTN 端點</p></td>
<td><p>不同網站的 Lync 使用者 (即網站 2)</p></td>
<td><p>不允許諮詢轉接</p></td>
</tr>
<tr class="even">
<td><p>PSTN 端點</p></td>
<td><p>未知網站的 Lync 使用者</p></td>
<td><p>不允許諮詢轉接</p></td>
</tr>
<tr class="odd">
<td><p>PSTN 端點</p></td>
<td><p>同盟的 Lync 使用者</p></td>
<td><p>不允許諮詢轉接</p></td>
</tr>
<tr class="even">
<td><p>PSTN 端點</p></td>
<td><p>相同網站的 PBX 端點 (即網站 1)</p></td>
<td><p>允許諮詢轉接</p></td>
</tr>
<tr class="odd">
<td><p>PSTN 端點</p></td>
<td><p>不同網站的 PBX 端點 (即網站 2)</p></td>
<td><p>不允許諮詢轉接</p></td>
</tr>
<tr class="even">
<td><p>相同網站的 PBX 端點 (即網站 1)</p></td>
<td><p>PSTN 端點</p></td>
<td><p>允許諮詢轉接</p></td>
</tr>
<tr class="odd">
<td><p>不同網站的 PBX 端點 (即網站 2)</p></td>
<td><p>PSTN 端點</p></td>
<td><p>不允許諮詢轉接</p></td>
</tr>
<tr class="even">
<td><p>任何網站的 PBX 端點</p></td>
<td><p>相同網站的 Lync 使用者 (即網站 1)</p></td>
<td><p>允許諮詢轉接</p></td>
</tr>
<tr class="odd">
<td><p>任何網站的 PBX 端點</p></td>
<td><p>不同網站的 Lync 使用者 (即網站 2)</p></td>
<td><p>允許諮詢轉接</p></td>
</tr>
<tr class="even">
<td><p>任何網站的 PBX 端點</p></td>
<td><p>未知網站的 Lync 使用者</p></td>
<td><p>允許諮詢轉接</p></td>
</tr>
<tr class="odd">
<td><p>任何網站的 PBX 端點</p></td>
<td><p>同盟的 Lync 使用者</p></td>
<td><p>允許諮詢轉接</p></td>
</tr>
</tbody>
</table>

