---
title: 在 Lync Server 2013 中設定位置資料庫
TOCTitle: 在 Lync Server 2013 中設定位置資料庫
ms:assetid: 8544be31-6958-47ef-b926-fdc80d56191c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398679(v=OCS.15)
ms:contentKeyID: 49291548
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定位置資料庫

 

_**上次修改主題的時間：** 2012-09-17_

若要讓用戶端自動偵測在網路中的位置，您需要先設定位置資料庫。如果您尚未設定位置資料庫，並將位置原則中的 **\[所需地點\]** 設定為 **\[是\]** 或 **\[免責聲明\]**，系統將會提示使用者手動輸入位置。

若要設定位置資料庫，您需要執行下列工作：

1.  將網路元素與位置的對應填入資料庫。如果您使用緊急定位辨識號碼 (ELIN) 閘道，將需要在 \<CompanyName\> 欄位中填入 ELIN。

2.  依據 E9-1-1 服務提供者維護的主要街道地址指南 (MSAG) 驗證地址。

3.  發行更新過的資料庫。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您也可以定義次要位置來源資料庫，該資料庫可用來取代位置資料庫。如需詳細資訊，請參閱＜<a href="lync-server-2013-configure-a-secondary-location-information-service.md">在 Lync Server 2013 中設定次要位置資訊服務</a>＞。</td>
</tr>
</tbody>
</table>


## 本章節內容

  - [填入位置資料庫](lync-server-2013-populate-the-location-database.md)

  - [驗證位址](lync-server-2013-validate-addresses.md)

  - [在 Lync Server 2013 中發佈位置資料庫](lync-server-2013-publish-the-location-database.md)

