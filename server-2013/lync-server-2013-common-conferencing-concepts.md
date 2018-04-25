---
title: Lync Server 2013 中的一般會議概念
TOCTitle: Lync Server 2013 中的一般會議概念
ms:assetid: a21d4987-1c0a-44c8-8a39-9c17ffb57f3c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688158(v=OCS.15)
ms:contentKeyID: 49890236
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的一般會議概念

 

_**上次修改主題的時間：** 2012-09-19_

所有會議類型皆有套用幾個相同的概念。這些概念的細節會在後續各節詳述。

## 原則和頻寬管理

Lync Server 2013 可讓系統管理員針對使用者可召集的會議類型來設定原則。如此可以落實組織的政策，並控制頻寬使用情形。 您可以定義各種會議原則，並將這些原則指派給使用者和使用者群組。 您也可以針對對等交談來設定原則。如需設定會議原則的詳細資訊，請參閱作業文件中的＜[Lync Server 2013 中的會議原則](lync-server-2013-conferencing-policies.md)＞。如需頻寬管理的詳細資訊，請參閱＜[Lync Server 2013 中的通話許可控制概觀](lync-server-2013-overview-of-call-admission-control.md)＞及＜[在 Lync Server 2013 設定視訊頻寬](lync-server-2013-configuring-video-bandwidth.md)＞。

## 封存和規範功能

如果您的組織必須遵循規範要求，Lync Server 2013 也提供相關功能。 您可以使用封存功能來封存會議中呈現的內容，以及立即訊息 (IM) 交談和 IM 會議的內容。如需詳細資訊，請參閱規劃文件中的＜[在 Lync Server 2013 中規劃封存](lync-server-2013-planning-for-archiving.md)＞。您可以使用 Persistent Chat Server 的規範功能來封存後續的多方、主題式交談。如需詳細資訊，請參閱規劃文件中的＜[在 Lync Server 2013 中規劃常設聊天室伺服器](lync-server-2013-planning-for-persistent-chat-server.md)＞。

## 監控功能

監控伺服器功能可以擷取詳細通話記錄 (CDR)，供您用來追蹤哪些使用者透過 Lync Server 2013 與其他哪些使用者交談。如需部署和設定監控功能的詳細資訊，請參閱＜[在 Lync Server 2013 中部署監控](lync-server-2013-deploying-monitoring.md)＞。

## 啟用會議的外部參加功能

您可以開放讓外部使用者受邀參與會議的功能，有效提高 Lync Server 2013 會議功能的投資報酬率。外部使用者包括：

  - **遠端使用者**   組織所屬的使用者，這些使用者位於組織防火牆外，並使用自己的筆記型電腦或其他 Lync Server 2013 裝置工作。

  - **同盟使用者**   來自您合作的公司，並且同樣執行 Lync Server 2013 的使用者。為了方便您的使用者輕鬆連絡這些使用者，您可以和這些公司建立同盟關係。

  - **匿名使用者**   由您的使用者特別邀請加入特定會議的其他所有外部使用者。公司裡的會議召集人可以將會議的電子郵件邀請寄送給外部使用者。該電子郵件內含一則連結，外部使用者只需要點選一下即可加入會議。

若要讓以上任一或全部案例成真，您必須部署 Edge Server，以協助在 Lync Server 2013 部署與外部使用者之間啟用安全通訊。使用 Edge Server 的 Lync Server 2013 解決方案所提供的媒體品質，高於虛擬私人網路 (VPN) 之類的解決方案。如需詳細資訊，請參閱＜[在 Lync Server 2013 中規劃外部使用者存取](lync-server-2013-planning-for-external-user-access.md)＞。

此外，不管您是否部署 Edge Server，都可以讓使用者 (組織內部或外部皆可) 透過標準 PSTN 電話撥入，以加入內部音訊會議。您可以部署 Lync Server 2013 撥入會議功能來達到這個目的。

## 會議類型與用戶端版本的相容性

如果您希望 Lync Server 2013 可以和舊版的 Office Communications Server 及其用戶端互通，請務必注意以下問題：

  - 使用 Lync Server 2013 的使用者無法排定 Live Meeting 會議，或是修改任何此類型的移轉會議。

  - 使用 Lync Server 2013 且需要參加由執行 Office Communications Server 2007 R2 的伺服器所主控之 Live Meeting 會議的使用者，其電腦必須安裝 Live Meeting 用戶端 (除了 Lync Server 2013 之外) 才能參加這些會議。

  - 一旦 Live Meeting 會議移轉至 Lync Server 2013，會議內容將無法跟著移轉。若是此時需要這些內容，就必須重新上傳。

