---
title: Lync Server 2013：使用者啟用 E9-1-1
TOCTitle: 使用者啟用 E9-1-1
ms:assetid: 3cc64f5b-492e-4c47-9713-3c376f2aad02
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425892(v=OCS.15)
ms:contentKeyID: 49290661
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中為使用者啟用 E9-1-1

 

_**上次修改主題的時間：** 2012-06-06_

在用戶端註冊期間， Lync Server 會使用位置原則針對啟用 Enterprise Voice 使用者來設定 E9-1-1 屬性。此原則包含的設定會定義 E9-1-1 實作方式。例如，位置原則包含緊急撥號字串之類的資訊，以及如果 位置資訊服務未自動提供位置時，使用者是否需要手動輸入位置。如需位置原則的完整定義，請參閱＜ [針對 Lync Server 2013 定義位置原則](lync-server-2013-defining-the-location-policy.md)＞。

Lync Server 可以根據子網路來指派位置原則給用戶端，或根據通用、每一網站或每一使用者原則來指派位置原則給使用者。如需判斷該如何啟用使用者，請先回答下列問題。

  - **您打算啟用所有使用者，還是打算將支援範圍限定在企業的特定地理區域？**  
    您可以使用通用位置原則，將某個位置指派給企業中所有的使用者。不過，透過指派位置原則給 Lync Server 網站，然後新增子網路至網站，則可以將 E9-1-1 支援限制在企業內的選定位置，並且根據每一網站來指定 E9-1-1 路由行為。

<!-- end list -->

  - **您是否打算透過使用者原則啟用個別使用者？**  
    如果您想自訂使用者的 E9-1-1 支援，可以直接指派位置原則給特定使用者或公共區域電話連絡人物件。

<!-- end list -->

  - **當用戶端漫遊至網路外，或從未定義的子網路連線時，是否仍應啟用用戶端的 E9-1-1？**  
    如果已指派通用、網站或每一使用者位置原則給使用者，當用戶端不在已定義的子網路內，或 位置資訊服務找不到位置時，使用者必須在用戶端手動輸入位置。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中定義手動擷取位置的使用者體驗](lync-server-2013-defining-the-user-experience-for-manually-acquiring-a-location.md)＞。

