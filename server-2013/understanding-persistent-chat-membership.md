﻿---
title: 瞭解常設聊天室成員資格
TOCTitle: 瞭解常設聊天室成員資格
ms:assetid: 900392d6-6e9f-4dae-93d6-39d7474409ef
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398730(v=OCS.15)
ms:contentKeyID: 49291649
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 瞭解常設聊天室成員資格

 

_**上次修改主題的時間：** 2013-02-22_

使用者對於 常設聊天室的存取權是透過成員資格來管理；使用者必須是聊天室的成員，才能張貼和閱讀訊息。只有具備聊天室指定關係的 **主持人**，才能使用 \[張貼至視聽中心\] 。視聽中心是一種聊天室類型 (另一種為 \[一般\] )，只有主持人可以張貼，但每個人都可以閱讀。

此外， 常設聊天室是根據某個類別的規則來運作。如需關於類別的詳細資訊，請參閱＜ [在 Lync Server 2013 中管理類別、聊天室及增益集](lync-server-2013-managing-categories-rooms-and-add-ins.md)＞，另請參閱本主題後續的＜類別範圍的運作方式＞及＜聊天室類別策略＞等小節。

常設聊天室系統管理員可以建立和管理聊天室類別。在建立和管理聊天室類別的過程中， 常設聊天室系統管理員可以設定主體 ( Active Directory 網域服務 群組、容器及使用者)，這些主體具備存取權，可成為特殊類別之聊天室的成員或建立者。

## Active Directory 網域服務和 常設聊天室

常設聊天室伺服器 需仰賴用於內部 常設聊天室使用者集區的 Active Directory。安裝 常設聊天室 (用戶端) 之後，您可以將使用者和使用者群組的網域新增至聊天室類別。接著可將這些使用者和群組新增至聊天室類別的成員資格。

> [!IMPORTANT]  
> 您必須為想要變更其 常設聊天室 的使用者確定不會有重複的名稱。如果有重複的使用者名稱存在，請將它們變更為不同的名稱，以便為使用者解除封鎖來進行這些變更。如果使用者在 Active Directory 中有重複的名稱且嘗試在其聊天室中進行變更，即會出現錯誤訊息，提示使用者連絡系統管理員以尋求解決方式。



## 類別範圍的運作方式

類別會根據其 **AllowedMembers** 屬性，來指定所有可成為該類別中 常設聊天室成員資格清單之成員的的使用者和群組。舉例來說，如果您將類別的 **AllowedMembers** 設定為 contoso.com ，便可將任何位於「Contoso」 的群組或使用者新增為該類別中聊天室的成員。如果將類別中的 **AllowedMembers** 設定為「銷售」 ，則只有這個通訊群組清單中的群組和使用者可以新增為該類別中聊天室的成員。同理， **Creators** 屬性讓您能夠控制可以在該類別中建立聊天室的人員。建立聊天室之後，即可將任何來自 **AllowedMembers** 群組的人員指定為 **Manager**，以便在聊天室中持續不斷地進行管理作業 (例如，成員資格變更與核准)。

為類別定義 **AllowedMembers** 和 **Creators** 有下列優點：

  - 此類別中的所有聊天室都會受限於類別等級上設定的限制。您可以使用這一點，根據業務需要與存取原則來隔離聊天室。

  - 位於 **Creators** 清單中的使用者可以在該類別中建立新的聊天室。如果您想要實作一個系統，讓組織中有限數量的人員可以建立聊天室，就可以使用這個控制項來符合該需求。

## 聊天室類別策略

類別的 **AllowedMembers** 必須包含所有將在此類別中使用任何 常設聊天室的使用者。根據您用以保護業務資料並確定適當存取等級的需求而定，您可能想要定義一或多個類別，來指定可以搜尋和參與聊天室的人。如果只想要允許一組特定的使用者 (中央服務台，或者僅限全職員工) 建立聊天室，您可以將範圍設定為類別的 **Creators**，以滿足該需求。

類別可以用來建立道德管束。道德管束可避免在組織中發生任何利益衝突。例如，系統管理員可以在某個類別中針對貿易商建立聊天室，而另一個類別中的聊天室僅供分析人員使用。

> [!NOTE]  
> 在 Lync Server 2013 中的 常設聊天室伺服器，我們不支援存取同盟使用者。如果有任何來自舊版 常設聊天室伺服器 中同盟使用者的聊天訊息，系統將會移轉這些訊息。您可以將同盟使用者新增為已停用的主體。



## 將成員範圍縮小至使用者群組

當您新增網域至類別時，可以使用其群組物件包含於該網域中的使用者群組，如此，就能將它們指定為該類別中聊天室的成員。

一般而言，建議您使用 Active Directory 容器 (例如，網域和組織單位)，來定義類別的 **AllowedMembers** 和 **Creators**。您可以將來自任何網域的物件新增至 **AllowedMembers** 或 **Creators** 清單。只有 **AllowedMembers** 或 **Creators** 清單內的物件可以新增至該類別下方的聊天室。

