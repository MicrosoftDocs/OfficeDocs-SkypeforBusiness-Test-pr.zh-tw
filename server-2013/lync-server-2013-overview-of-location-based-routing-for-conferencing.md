---
title: 會議位置基礎路由概觀
TOCTitle: 會議位置基礎路由概觀
ms:assetid: 8b86740e-db95-4304-bb83-64d0cbb91d47
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn362815(v=OCS.15)
ms:contentKeyID: 56269118
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 會議位置基礎路由概觀

 

_**上次修改主題的時間：** 2015-03-09_

位置基礎路由會議應用程式能夠為 Lync 會議提供防止 PSTN 電話旁路作業的機制。該應用程式會監控進行中的會議並根據參與會議之 Lync 使用者的所在位置執行位置基礎路由限制。

位置基礎路由會議應用程式能決定是否要在符合下列條件時於 Lync 會議中執行位置基礎路由：

  - 會議召集人已啟用位置基礎路由。位置基礎路由限制僅會套用至由啟用位置基礎路由的使用者組織的會議。

  - 至少有一個會議參與者為 PSTN 端點。位置基礎路由限制僅適用於包含 PSTN 端點的會議。

  - 使用 PSTN 閘道將會議橋接至 PSTN 的網站與召集人和參與者的連線來源網站相同。

位置基礎路由會議應用程式可防止來自不同網站的 Lync 使用者與 PSTN 端點參與相同的會議。若是會議召集人啟用位置基礎路由，則會議應用程式會執行下列限制：

  - 端點是否能夠加入 Lync 會議，得視已加入會議的端點而定，且此限制將會因為會議中已加入端點的離開與新端點的加入而進行調整。若是召集人與參與者均是從相同網站加入 Lync 會議，則 PSTN 端點、來自相同網站的其他參與者、來自不同網站的其他參與者，或來自未知網站的參與者均可加入會議。

  - 若是召集人與參與者從不同或未知的網站加入會議，則當 PSTN 通話從啟用位置基礎路由的 SIP 主幹進入時，不允許 PSTN 端點加入會議。

  - 若是召集人與參與者均從相同網站加入會議，且有參與者從 PSTN 加入相同會議，則不允許來自不同網站的 Lync 端點加入會議。

這些會議位置基礎路由限制摘要說明於下表：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>會議中位於任何指定位置的使用者</p></td>
<td><p>允許加入會議的使用者</p></td>
<td><p>不允許加入會議的使用者</p></td>
</tr>
<tr class="even">
<td><p>Lync VoIP 用戶端使用者來自單一網站</p></td>
<td><p>相同網站的 Lync VoIP 用戶端使用者</p>
<p>不同網站的 Lync VoIP 用戶端使用者</p>
<p>未知網站的 Lync VoIP 用戶端使用者</p>
<p>同盟的 Lync VoIP 用戶端使用者</p>
<p>從 PSTN 端點加入的使用者</p></td>
<td><p>無</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>Lync VoIP 用戶端使用者來自未知網站</p></td>
<td><p>任何網站的 Lync VoIP 用戶端使用者</p>
<p>未知網站的 Lync VoIP 用戶端使用者</p>
<p>同盟的 Lync VoIP 用戶端使用者</p></td>
<td><p>透過 PSTN 端點加入的使用者</p>
<p></p></td>
</tr>
<tr class="even">
<td><p>Lync VoIP 用戶端使用者來自不同網站</p></td>
<td><p>任何網站的 Lync VoIP 用戶端使用者</p>
<p>未知網站的 Lync VoIP 用戶端使用者</p>
<p>同盟的 Lync VoIP 用戶端使用者</p></td>
<td><p>透過 PSTN 端點加入的使用者</p></td>
</tr>
<tr class="odd">
<td><p>Lync VoIP 用戶端使用者來自單一網站且有使用者從 PSTN 端點加入</p></td>
<td><p>相同網站的 Lync VoIP 用戶端使用者</p>
<p></p></td>
<td><p>不同網站的 Lync VoIP 用戶端使用者</p>
<p>未知網站的 Lync VoIP 用戶端使用者</p>
<p>同盟的 Lync VoIP 用戶端使用者</p></td>
</tr>
</tbody>
</table>


以下為位置基礎路由會議應用程式的額外特性：

  - 當使用者不允許加入設有位置基礎路由限制的會議時，發話至會議的使用者將遭拒且其 Lync 用戶端將回報通話未完成或通話結束。

  - 若是加入執行位置基礎路由之會議的 PSTN 端點是透過未啟用位置基礎路由的主幹加入會議，則無論其狀態為何，系統均不會限制該端點加入會議。

  - 透過不會將通話輸出至 PSTN 的 SIP 主幹連線至中繼伺服器的 PBX 系統將與位於定義 SIP 主幹之相同網站中的 Lync 使用者採取相同的執行項目。例如，若是會議中的 PBX 使用者與 Lync 使用者位於相同網站，則 PSTN 端點將可加入會議；若是 PBX 使用者與 Lync 使用者位於不同網站，則 PSTN 端點將無法加入會議。

