---
title: Lync Server 2013：轉譯規則
TOCTitle: 轉譯規則
ms:assetid: 6e067bd4-4931-4385-81ac-2acae45a16d8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398520(v=OCS.15)
ms:contentKeyID: 49291259
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的轉譯規則

 

_**上次修改主題的時間：** 2015-03-09_

Lync Server 2013企業語音需要所有撥號字串都必須正常化為 E.164 格式，以便於執行反向號碼查閱 (RNL)。在 Microsoft Lync Server 2010 中，轉譯規則僅支援撥號。在 Microsoft Lync Server 2013 中的新增功能，轉譯規則亦支援撥號。 *「主幹對等」* (亦即相關聯的閘道、專用交換機 (PBX) 或 SIP 主幹) 可能要求號碼必須為本地撥號格式。若要將號碼從 E.164 格式轉譯為本地撥號格式，則可以先定義一或多個轉譯規則來操作要求 URI，再將其路由傳送至主幹對等。例如，您可以撰寫轉譯規則，移除撥號字串開頭的 +44，並改為 0144。

在伺服器上執行輸出路由轉譯，則可以減少在每個個別主幹對等上的設定需求，以將電話號碼轉譯為區域撥號格式。在規劃要與給定 中繼伺服器叢集相關聯的閘道及其數目時，分組具有類似區域撥號需求的主幹對等也許非常實用。如此，可減少所需的轉譯規則數目以及寫入它們所需的時間。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>建立一個或多個轉譯規則與 企業語音主幹設定的關聯，應用作在主幹對等上設定轉譯規則的替代方法。如果您已在主幹對等上設定轉譯規則，請不要建立轉譯規則與 企業語音主幹設定的關聯，因為兩個規則可能會發生衝突。</td>
</tr>
</tbody>
</table>


## 範例轉譯規則

下列轉譯規則範例顯示如何在伺服器上開發規則，以將號碼從 E.164 格式轉譯為主幹對等的區域格式。

如需如何實作轉譯規則的詳細資訊，請參閱部署文件中的＜ [在 Lync Server 2013 中定義轉譯規則](lync-server-2013-defining-translation-rules.md)＞。


<table>
<colgroup>
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
</colgroup>
<thead>
<tr class="header">
<th>說明</th>
<th>開頭數字</th>
<th>長度</th>
<th>要移除的數字</th>
<th>要加入的數字</th>
<th>比對模式</th>
<th>轉譯</th>
<th>範例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>美國的傳統長途撥號</p>
<p>(除去 ‘+’)</p></td>
<td><p>+1</p></td>
<td><p>剛好 12 個</p></td>
<td><p>1</p></td>
<td><p>0</p></td>
<td><p>^\+(1\d{10})$</p></td>
<td><p>$1</p></td>
<td><p>+14255551010 變成 14255551010</p></td>
</tr>
<tr class="even">
<td><p>美國國際長途撥號</p>
<p>(除去 ‘+’ 並加上 011)</p></td>
<td><p>+</p></td>
<td><p>至少 11 個</p></td>
<td><p>1</p></td>
<td><p>011</p></td>
<td><p>^\+(\d{9}\d+)$</p></td>
<td><p>011$1</p></td>
<td><p>+441235551010 變成 011441235551010</p></td>
</tr>
</tbody>
</table>

