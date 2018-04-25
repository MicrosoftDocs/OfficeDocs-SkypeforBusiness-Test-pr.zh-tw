---
title: 在 Lync Server 2013 中設定電話撥入式會議個人識別碼 (PIN) 規則
TOCTitle: 在 Lync Server 2013 中設定電話撥入式會議個人識別碼 (PIN) 規則
ms:assetid: 27b79fb1-e2dc-4f71-bc82-b6eb61be2b16
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg520967(v=OCS.15)
ms:contentKeyID: 49290390
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定電話撥入式會議個人識別碼 (PIN) 規則

 

_**上次修改主題的時間：** 2012-06-19_

您的組織中具有 Active Directory 網域服務 (AD DS) 認證的 Lync Server 2013 使用者，可使用個人識別碼 (PIN) 以驗證使用者的身分加入電話撥入式會議。PIN 原則可定義電話撥入式會議 PIN 的運作方式規則。

如果您要將特定原則套用至網站或特定使用者群組，您可以建立新的 PIN 原則。如果您要對整個組織使用相同的 PIN 原則，您可以使用全域 PIN 原則，並視需要加以修改。對使用者套用 PIN 原則時，會優先套用最小的範圍。如果您為使用者指派了使用者層級 PIN 原則，這些設定將會優先套用。如果您未指派使用者原則，則會套用網站層級 PIN 原則 (若有的話)。如果未套用使用者或網站原則，則會使用全域 PIN 原則的預設設定。

## 本章節內容

  - [在 Lync Server 2013 中修改預設電話撥入式會議 PIN 設定](lync-server-2013-modify-the-default-dial-in-conferencing-pin-settings.md)

  - [在 Lync Server 2013 中建立或修改使用者站台或群組的電話撥入式會議 PIN 設定](lync-server-2013-create-or-modify-dial-in-conferencing-pin-settings-for-a-site-or-group-of-users.md)

  - [刪除站台或使用者群組的電話撥入式會議 PIN 設定](lync-server-2013-delete-dial-in-conferencing-pin-settings-for-a-site-or-group-of-users.md)

