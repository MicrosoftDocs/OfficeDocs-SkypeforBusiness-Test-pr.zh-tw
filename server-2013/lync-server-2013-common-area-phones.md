---
title: Lync Server 2013 中的公共區域電話
TOCTitle: Lync Server 2013 中的公共區域電話
ms:assetid: d63bb3de-154e-4347-9251-9fa94e7d593a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ994076(v=OCS.15)
ms:contentKeyID: 52056231
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的公共區域電話

 

_**上次修改主題的時間：** 2013-02-20_

公用區域電話是未與個別使用者相關聯的 IP 電話。公用區域電話不是位於某個人的辦公室中，通常是位於建築物大廳、餐廳、員工休息室、會議室以及其他一群人可能聚集的地點。在 Lync Server 中使用的電話與公用區域電話不同，其通常是靠各種語音原則和撥號對應表在維護，而原則和對應表是指派給個別使用者，公用區域電話不會被指派個別使用者。這表示必須以異於其他電話的方式管理公用區域電話。

若要管理公用區域電話，您可以為所有公用區域電話建立 Active Directory 網域服務 連絡人物件 (就像使用者帳戶一樣，可以被指派原則和語音對應表)。此方法可讓您對公用區域電話保持控制，即使這些電話與個別使用者無關聯。

透過本節中的主題了解如何建立公用區域電話的連絡人物件、加以修改和刪除，以及設定和檢視部署中有關公用區域電話的設定資訊。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有三種公用區域電話：Aastra 6721ip 公用區域電話、HP 4110 IP Phone 及 Polycom CX500 IP 公用區域電話。Polycom CX3000 IP 會議電話是另一種不同的公用區域電話，它適合在會議室中使用。如需公用區域電話的詳細資訊，請參閱<a href="http://technet.microsoft.com/zh-tw/library/gg398958(v=ocs.14).aspx">選擇新裝置</a>的＜公用區域電話＞一節。</td>
</tr>
</tbody>
</table>


## 本章節內容

  - [檢視公共區域電話資訊](lync-server-2013-view-common-area-phone-information.md)

  - [建立或修改公共區域電話連絡人物件](lync-server-2013-create-or-modify-a-common-area-phone-contact-object.md)

  - [啟用或停用公用辦公桌](lync-server-2013-enable-or-disable-hot-desking.md)

  - [刪除公共區域電話連絡人物件](lync-server-2013-delete-a-common-area-phone-contact-object.md)

  - [指派原則給公共區域電話](lync-server-2013-assign-policies-to-a-common-area-phone.md)

