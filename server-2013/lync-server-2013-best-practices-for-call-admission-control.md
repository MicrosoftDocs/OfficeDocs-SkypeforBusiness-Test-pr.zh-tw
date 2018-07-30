---
title: Lync Server 2013：通話許可控制的最佳做法
TOCTitle: 通話許可控制的最佳做法
ms:assetid: 97173cca-8175-4ae2-a247-eb7ef809da93
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398770(v=OCS.15)
ms:contentKeyID: 49291751
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中通話許可控制的最佳做法

 

_**上次修改主題的時間：** 2012-09-22_

為了提升效能及加快部署的速度，在部署通話許可控制時請套用下列最佳實務做法：

  - 確認已針對目前和預期的媒體流量適當地佈建 WAN。
    
    > [!NOTE]  
    > 我們建議您在規劃頻寬限制時將緩衝計算在內。某些諸如競速情況等案例會影響使用的頻寬總數，並且導致超出頻寬限制的情況。例如，如果有兩通電話嘗試在媒體流量逼近頻寬限制時啟動，率先啟動的電話將迫使另一通電話遭到拒絕。
    


  - 監控網路使用量和詳細通話記錄，以便選擇最合適的 CAC 設定，以及在網路使用量變更時更新 CAC 設定。

  - 使用 CAC 頻寬原則來補足 QoS 設定。

  - 如果您想要將封鎖的通話重新路由傳送至 PSTN，請驗證 PSTN 功能和能力。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中規劃撥出語音路由](lync-server-2013-planning-outbound-voice-routing.md)＞。
    
    > [!NOTE]  
    > 能力指的是需要為支援潛在 PSTN 重新路由而開啟的連接埠數量。
    

