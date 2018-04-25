---
title: 針對常設聊天室伺服器執行回溯相容性
TOCTitle: 針對常設聊天室伺服器執行回溯相容性
ms:assetid: 53f1a706-3104-4a94-8b4e-8badd9a066d6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204901(v=OCS.15)
ms:contentKeyID: 49290933
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 針對常設聊天室伺服器執行回溯相容性

 

_**上次修改主題的時間：** 2013-02-21_

Lync Server 2013常設聊天室伺服器 端點提供一種方式來建立簡單 URL 以指向 Persistent Chat Server 集區。這對舊版用戶端 ( Microsoft Office Communications Server 2007 R2群組聊天伺服器或 Lync Server 2010 群組聊天) 而言非常有用，因為使用者可以在嘗試將舊版用戶端指向執行 Lync 2013 的 常設聊天室的電腦時，在手動設定中輸入簡單 URL。此端點無法供 常設聊天室使用，而且只有舊版用戶端才需要此端點。這對於可能要移轉聊天室，但尚未於整個組織中部署 Lync 2013 用戶端的過度時期而言非常有用。執行 Lync 2010群組聊天 (用戶端) 的使用者之後仍能連線至 常設聊天室伺服器後端伺服器。

您不需要建立多個 常設聊天室伺服器 端點；只需為每個 Persistent Chat Server 集區建立一個端點。系統管理員可以建立多個端點 (每個集區一個)，但可將舊版用戶端設定為一次只能連線至一個集區。在一般或主流案例中，舊版部署只是一個集區。新的部署通常會將該集區移轉至新的 Lync Server 2013，而且可能會新增一些新的其他 Persistent Chat Server 集區。

此主流案例通常會遵循下列模式：

  - 您會管理具有一個 Lync Server 2010 群組聊天 集區的使用者，而您的 Lync 2010 群組聊天 用戶端會使用一些已知的使用者 (可能是預設值 sip:ocschat@ *\<domainName\>*.com 或類似的項目)，連線到該集區。使用者是已啟用 SIP 的 Active Directory 網域服務，而且查閱服務會利用它們來登錄以接收輸入要求。

  - 接著安裝 Lync Server 2013常設聊天室伺服器 和 Persistent Chat Server 集區。

  - 在使用者通常是離線狀態的期間 (例如週末)：
    
      - 關閉 Lync Server 2010 群組聊天。
    
      - 將資料從 Lync Server 2010 群組聊天集區移轉至 Lync Server 2013Persistent Chat Server 集區。
    
      - 從 Active Directory 網域服務 中刪除已知的使用者。
    
      - 利用與先前刪除之已知使用者相同的 SIP URI 來建立新的「舊版端點」 。
    
      - 啟動 Lync Server 2013常設聊天室伺服器。

  - 使用者使用他們的 Lync 2010 群組聊天 (用戶端) 重新登入，並連線至他們的資料，而不需變更任何設定。

  - 您稍後可以解除委任 Lync Server 2010 群組聊天。接著可以部署 Lync Server 2013常設聊天室伺服器，並安裝新的 Lync Server 2013Persistent Chat Server 集區。

如需有關從 Lync Server 2010 群組聊天移轉到 Lync Server 2013常設聊天室伺服器的詳細資訊，請參閱＜ [從 Lync Server 2010 群組聊天或 Office Communications Server 2007 R2 群組聊天移轉至 Lync Server 2013 常設聊天室伺服器](migration-from-lync-server-2010-group-chat-or-office-communications-server-2007-r2-group-chat-to-lync-server-2013-persistent-chat-server.md)＞。

若要執行回溯相容性 (以建立 常設聊天室伺服器 端點來指向 Persistent Chat Server 集區，這可以透過舊版 群組聊天集區用戶端來使用)：

    New-CsPersistentChatEndpoint -SipAddress <CO name, ex. persistentchat@contoso.com> -PersistentChatPoolFqdn <pool FQDN, like pcpool.contoso.com>

接著，設定 常設聊天室用戶端以使用該 SIP 位址作為其連絡人物件。此 SIP 位址是利用適用於特定 Persistent Chat Server 集區 的 **New-CsPersistentChatEndpoint** Cmdlet 來建立。

若要使用 Windows PowerShell 命令列介面 來新增 常設聊天室伺服器 端點，請考量下列範例。在此案例中，您是在 "contoso.com" 拓撲上設定連絡人物件，並將它命名為 "persistentchat"，其中集區的完整網域名稱 (FQDN) 為 "pcpool.contoso.com"：

    New-CsPersistentChatEndpoint -SipAddress sip:persistentchat@contoso.com -PersistentChatPoolFqdn pcpool.contoso.com

## 請參閱

#### 概念

[從 Lync Server 2010 群組聊天或 Office Communications Server 2007 R2 群組聊天移轉至 Lync Server 2013 常設聊天室伺服器](migration-from-lync-server-2010-group-chat-or-office-communications-server-2007-r2-group-chat-to-lync-server-2013-persistent-chat-server.md)

