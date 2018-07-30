---
title: Lync Server 2013：設定公用提供者的媒體加密
TOCTitle: 設定公用提供者的媒體加密
ms:assetid: a95814cf-c5a9-4652-8ffc-c469a2653153
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205149(v=OCS.15)
ms:contentKeyID: 49291940
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定公用提供者的媒體加密

 

_**上次修改主題的時間：** 2014-12-12_

如需授權需求的詳細資訊以及如何完成佈建程序的詳細資訊，請參閱＜Microsoft Lync Server、Office Communications Server 和 Live Communications Server 的公用 IM 連線佈建指南＞，網址為： <http://go.microsoft.com/fwlink/?linkid=155970>。

如果您實作與 Windows Live Messenger 的音訊/視訊 (A/V) 同盟，還必須修改 Lync Server 加密層級和 EnablePublicCloudAccess 原則這兩個參數。根據預設，加密層級設定為 \[必要\]。您必須將此設定變更為 \[已支援\]。如果 EnablePublicCloudAccess 原則設定成 False，這就必須設定成「True」 。您可以從 Lync Server 管理命令介面執行此作業。

> [!IMPORTANT]  
> 更勝以往，Lync 成為連接全世界組織之間以及個人之間的強大工具。除了 Lync Standard Client Access License (CAL) 之外，與 Windows Live Messenger 同盟不需要其他使用者/裝置授權。明年，此清單更將加入 Skype 同盟，讓 Lync 使用者可透過 IM 和語音觸及數億位使用者。



## 設定 Windows Live 的同盟

1.  在前端伺服器上啟動 Lync Server 管理命令介面：依序按一下 \[開始\] 、\[所有程式\] 、\[ Microsoft Lync Server 2013\] 及 \[ Lync Server 管理命令介面\] 。

2.  在命令提示字元中輸入下列命令：
    
    ```
    Set-CsMediaConfiguration -EncryptionLevel SupportEncryption
    ```
    ```
    Set-CsExternalAccessPolicy Global -EnablePublicCloudAccess $true -EnablePublicCloudAudioVideoAccess $true
    ```
    
    > [!NOTE]  
    > 這是必要步驟，因為 Windows Live Messenger 不支援音訊/視訊的加密。此命令會將您的全域原則設定為支援加密設定，而非要求加密音訊/視訊資料。支援加密的用戶端仍將使用加密，例如 Lync 2013。
    

