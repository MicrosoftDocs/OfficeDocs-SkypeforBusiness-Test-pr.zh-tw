---
title: 將子網路與媒體旁路的網站關聯
TOCTitle: 將子網路與媒體旁路的網站關聯
ms:assetid: 5bc632b7-1446-470f-b332-48ea0ca4d1fd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398401(v=OCS.15)
ms:contentKeyID: 49291030
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 將子網路與媒體旁路的網站關聯

 

_**上次修改主題的時間：** 2012-09-12_

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本主題假定您已經設定好媒體旁路全域設定，以及媒體旁路的網路區域與網路網站。</td>
</tr>
</tbody>
</table>


網路中的每個子網路都必須與特定網路網站關聯。這是因為我們需要子網路資訊來判斷端點所在的網路網站。一旦知道工作階段中的雙方位置，媒體旁路就能判斷出要將媒體傳送到何處以便處理。

媒體旁路不需要任何特殊需求，就能將子網路與網路網站進行關聯。若要在拓撲中建立子網路與網路網站的關聯，請遵循[在 Lync Server 2013 中建立子網路與網路站台的關聯](lync-server-2013-associate-a-subnet-with-a-network-site.md)中的步驟進行。

## 後續步驟：建立頻寬原則設定檔

當您為媒體旁路需要將子網路與網站關聯之後，必須建立一個或多個頻寬原則設定檔，以將子網路分割為具有良好連線能力與不具備良好連線能力的子網路，以因應媒體旁路所需。當網路地區內的所有子網路與沒有頻寬限制的網站關聯時，將提供良好的連線能力，因此這些子網路可以使用媒體旁路。

如需設定頻寬原則設定檔的步驟說明，請參閱＜[在 Lync Server 2013 中建立頻寬原則設定檔](lync-server-2013-create-bandwidth-policy-profiles.md)＞。

