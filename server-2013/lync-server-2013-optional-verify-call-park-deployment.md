---
title: Lync Server 2013：(選用) 驗證通話駐留部署
TOCTitle: (選用) 驗證通話駐留部署
ms:assetid: fcfe0962-1a9c-4cbd-847c-fed40e3b1480
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg413076(v=OCS.15)
ms:contentKeyID: 49292920
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# (選用) 在 Lync Server 2013 中驗證通話駐留部署

 

_**上次修改主題的時間：** 2012-09-11_

在安裝及設定 通話駐留 之後，需要驗證設定以確認駐留和擷取通話如預期般運作。請至少確認下列項目：

  - 打電話給已啟用 通話駐留 的使用者，並請使用者駐留通話。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您在執行此測試前才剛於語音原則中啟用了 通話駐留，則駐留通話的使用者需要登出 Lync Server，然後再次登入，才能在來電轉接清單中看到 通話駐留 選項。</td>
    </tr>
    </tbody>
    </table>


  - 撥打軌道號碼以擷取通話。

  - 駐留另一通電話，並讓駐留的通話逾時，且不要接聽回電。確認逾時的通話會正確地路由傳送到為 \[OnTimeoutURI\] 指定的後援目的地。

