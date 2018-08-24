---
title: Lync Server 2013：設定未指派號碼表
TOCTitle: 設定未指派號碼表
ms:assetid: eaa01986-e92f-4328-acf6-4e46c4306a04
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399053(v=OCS.15)
ms:contentKeyID: 49292696
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定未指派號碼表

 

_**上次修改主題的時間：** 2012-10-30_

在 Lync Server 2013 中，您可以指定如何處理撥打至組織內有效，但未指派給使用者或電話之電話號碼的來電。來電者可能會聽到訊息及/或可能被路由傳送到其他目的地。

設定未指派號碼表的方式取決於其使用方式。您可以設定包含組織所有有效分機號碼、只包含未指派的分機號碼，或包含結合這兩種類型號碼的表格。未指派號碼表可以同時包含已指派和未指派的號碼，但是只有在來電者撥打目前未指派的號碼時才會叫用。如果您在未指派號碼表中納入所有有效的分機號碼，可以指定每次某人離開組織時要執行的動作，而不必重新設定表格。如果表格中包含未指派的分機號碼，您可以針對特定號碼修改要採取的動作。例如，如果您變更客戶服務人員的分機號碼，則可以在表格中包含舊的客戶服務號碼，並且將它指派給提供新號碼的宣告。

> [!IMPORTANT]  
> 在您設定未指派的號碼表之前，您的系統必須已定義宣告或已設定 Exchange 整合通訊 (UM) 自動語音應答。



> [!TIP]
> 當有人撥打未指派的號碼時， Lync Server 會從上到下搜尋未指派的號碼表，並使用第一個相符的範圍。因此，您想要當做最後一個手段執行的動作，應該是針對表格中最後一個範圍指定的動作。


## 本章節內容

[在 Lync Server 2013 中建立或修改未指派號碼範圍](lync-server-2013-create-or-modify-an-unassigned-number-range.md) [在 Lync Server 2013 中建立宣告](lync-server-2013-create-an-announcement.md)

