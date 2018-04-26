---
title: Lync Server 2013 中的會議原則
TOCTitle: Lync Server 2013 中的會議原則
ms:assetid: 8f92eb7c-ee66-4df6-a726-4bff93b122cb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688133(v=OCS.15)
ms:contentKeyID: 49890206
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的會議原則

 

_**上次修改主題的時間：** 2012-09-18_

會議原則定義使用者可以在會議中使用的特性與功能。會議原則設定包含廣泛的排程和參與選項，從會議是否可包含 IP 音訊和視訊到可出席會議的人數上限都涵蓋在內。系統管理員可以使用會議原則，來管理會議的安全、頻寬和法律層面。

您可以在三個層級定義會議原則：全域範圍、網站範圍，以及使用者範圍。設定值會依據最窄的範圍到最寬的範圍，依序套用至特定使用者。如果將使用者原則指派給使用者，則這些設定具有優先權。如果未指派使用者原則，則會套用網站設定。如果未套用使用者或網站原則，則由全域原則提供預設值。

由於全域原則預設已經存在，因此您無法建立新的全域原則。您也無法刪除現有的全域原則，但可變更現有的全域原則，以自訂您自己的預設值。

## 本章節內容

  - [檢視會議原則資訊](lync-server-2013-view-conferencing-policy-information.md)

  - [在 Lync Server 2013 中建立或修改會議原則](lync-server-2013-create-or-modify-a-conferencing-policy.md)

  - [刪除現有的會議原則](lync-server-2013-delete-an-existing-conferencing-policy.md)

  - [Lync Server 2013 中的會議原則設定參考](lync-server-2013-conferencing-policy-settings-reference.md)

