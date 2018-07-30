---
title: Lync Server 2013：設定電話撥入式會議存取號碼
TOCTitle: 設定電話撥入式會議存取號碼
ms:assetid: d8a18030-f318-43dd-834d-70e5014b5e8a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398952(v=OCS.15)
ms:contentKeyID: 49292476
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定電話撥入式會議存取號碼

 

_**上次修改主題的時間：** 2011-07-17_

當您部署電話撥入式會議時，需要設定可讓使用者從公用交換電話網路 (PSTN) 撥打的電話號碼，以便加入會議的音訊部分。這些撥入存取號碼會顯示在會議邀請中和電話撥入式會議設定網頁上。

在您可以建立撥入存取號碼之前，必須先規劃您的電話撥入式會議地區，然後使用這些地區來設定撥號對應表。如需有關地區的詳細資訊，請參閱規劃文件中的＜ [Lync Server 2013 中的電話撥入式會議需求](lync-server-2013-dial-in-conferencing-requirements.md)＞。如需設定電話撥入式會議之撥號對應表的詳細資訊，請參閱＜ [在 Lync Server 2013 中設定電話撥入式會議的撥號對應表](lync-server-2013-configure-dial-plans-for-dial-in-conferencing.md)＞。

> [!NOTE]  
> 在完成新撥入存取號碼的 Active Directory 網域服務 (AD DS) 複寫之前，您無法使用該存取號碼。複寫可能需要幾小時才完成。



> [!NOTE]  
> 建立撥入存取號碼之後，您可以修改 Active Directory 連絡人物件的顯示名稱，以便使用者可以更輕易地識別正確的存取號碼。使用 <strong>Set-CsDialInConferencingAccessNumber</strong> Cmdlet 來修改顯示名稱。您不應手動修改 Active Directory 物件。如需修改存取號碼的詳細資訊，請參閱 Lync Server 管理命令介面文件中的 <strong>Set-CsDialInConferencingAccessNumber</strong> Cmdlet。



## 本章節內容

[在 Lync Server 2013 中建立或修改電話撥入式會議存取號碼](lync-server-2013-create-or-modify-a-dial-in-conferencing-access-number.md)

## 請參閱

#### 概念

[Lync Server 2013 中的電話撥入式會議需求](lync-server-2013-dial-in-conferencing-requirements.md)  

#### 其他資源

[在 Lync Server 2013 中設定電話撥入式會議的撥號對應表](lync-server-2013-configure-dial-plans-for-dial-in-conferencing.md)

