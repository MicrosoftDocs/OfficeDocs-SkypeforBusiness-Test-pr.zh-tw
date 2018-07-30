---
title: 部署 Lync Server 2013 用戶端
TOCTitle: 部署 Lync Server 2013 用戶端
ms:assetid: 508e5dfa-588b-4289-81ce-2043c2d79e04
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204883(v=OCS.15)
ms:contentKeyID: 49290905
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 部署 Lync Server 2013 用戶端

 

_**上次修改主題的時間：** 2012-10-19_

在將使用者移轉至 Lync Server 2013 之後，請執行下列動作：

1.  在新的 Lync Server 2013 伺服器上使用「用戶端版本篩選器」，就只有已安裝最新版之更新的用戶端才可登入。

2.  如有需要，請設定用戶端開機所需的群組原則設定。如需詳細資訊，請參閱部署文件中的 [在 Lync Server 2013 中設定用戶端啟動程序原則](lync-server-2013-configuring-client-bootstrapping-policies.md)。只有當您需要變更現有用戶端的開機原則，或要設定新的用戶端開機原則時，才需要設定這些設定。若您無意設定用戶端開機原則，或是想要繼續使用舊版的用戶端開機原則，便無須採取任何動作。

3.  使用 Lync Server 2013 控制台、 Lync Server 2013 管理命令介面或同時使用兩者，為特定使用者或使用者群組設定其他使用者及用戶端原則。如需詳細資訊，請參閱規劃文件中的 [Lync 2013 新增及變更的設定](lync-server-2013-new-and-changed-settings-for-lync-2013.md)。

4.  部署最新版的 Lync Server 2013 用戶端以及最新版的累計更新。如需詳細資訊，請參閱部署文件中的 [在 Lync Server 2013 中部署用戶端和裝置](lync-server-2013-deploying-clients-and-devices.md)。

5.  (選用) 貴組織如有需要 Lync Server 2013 的增強目前狀態隱私權模式，可在移轉完成後定義用戶端版的原則規則，禁止舊版的用戶端登入，然後再啟用增強目前狀態隱私權模式。
    
    > [!IMPORTANT]  
    > 為每位使用者或指定的伺服器集區安裝最新版的用戶端版本之前，請勿啟用 Lync 2013 增強目前狀態隱私權模式。
    

