---
title: Lync Server 2013：為分支使用者建立 VoIP 路由原則
TOCTitle: 為分支使用者建立 VoIP 路由原則
ms:assetid: 10deca9f-f870-4a42-b25d-e4fc53108658
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398196(v=OCS.15)
ms:contentKeyID: 49290123
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中為分支使用者建立 VoIP 路由原則

 

_**上次修改主題的時間：** 2012-09-23_

我們建議您為分支網站的使用者建立個別的 VoIP 原則。此原則應該包含從 Survivable Branch Appliance 閘道或 Survivable Branch 伺服器 外部閘道撥出路由，以及從中央網站的閘道撥出的備用路由。不管使用者註冊所在位置是在 Survivable Branch Appliance 或 Survivable Branch 伺服器 的登錄器，或是中央網站的備用登錄器叢集，使用者的 VoIP 原則一律生效。

## 若要為分支使用者設定 VoIP 路由原則

1.  建立使用者層級的撥號對應表並將其指派給分支使用者 (請參閱操作文件中的＜ [在 Lync Server 2013 中建立撥號對應表](lync-server-2013-create-a-dial-plan.md)＞)。

2.  指派與該網站上使用者撥號習慣對應的正規化規則。如果 Survivable Branch Appliance 或 Survivable Branch 伺服器使用者容錯移轉至中央網站的備用登錄器集區，則相同的撥號對應表將會生效。 (請參閱操作文件中的＜ [在 Lync Server 2013 中建立撥號對應表](lync-server-2013-create-a-dial-plan.md)＞)。

3.  設定可從 Survivable Branch Appliance 閘道或 Survivable Branch 伺服器外部閘道撥出的語音路由 (請參閱操作文件中的＜ [在 Lync Server 2013 中建立語音路由](lync-server-2013-create-a-voice-route.md)＞)。

4.  設定 Survivable Branch Appliance 或 Survivable Branch 伺服器 閘道上的備用通話路由，以指向中央網站上的備用登錄器集區 (與中繼伺服器組合在一起)(請參閱您的 Survivable Branch Appliance 或 Survivable Branch 伺服器 廠商文件)。
    
    > [!NOTE]  
    > 此備用通話路由設定作業有助於在 Survivable Branch Appliance 或 Survivable Branch 伺服器 無法提供服務時 (例如，停機維護期間) 確保撥入給分支使用者的通話能夠暢通無阻。如果 Survivable Branch Appliance 或 Survivable Branch 伺服器 上的登錄器與中繼伺服器無法提供服務，且使用者已經註冊到中央網站的備用登錄器集區，則撥入的通話仍舊可以路由傳送給使用者。
    


下一步：[在 Lync Server 2013 中設定語音信箱重新路由設定](lync-server-2013-configure-voice-mail-rerouting-settings.md)

