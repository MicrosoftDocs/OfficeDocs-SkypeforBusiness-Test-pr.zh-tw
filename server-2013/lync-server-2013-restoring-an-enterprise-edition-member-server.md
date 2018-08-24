---
title: 還原 Enterprise Edition 成員伺服器
TOCTitle: 還原 Enterprise Edition 成員伺服器
ms:assetid: d960b19c-2104-4719-b736-0d940f254d42
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh202191(v=OCS.15)
ms:contentKeyID: 52056235
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 還原 Enterprise Edition 成員伺服器

 

_**上次修改主題的時間：** 2013-02-18_

若執行為下列伺服器角色之一的伺服器失敗，請遵循本主題中的程序還原該伺服器。若有多部伺服器各自失敗，請遵循各伺服器的程序還原。

  - 前端伺服器

  - 中繼伺服器

  - Director

  - Persistent Chat Server

  - Edge Server

> [!TIP]
> 建議您在還原之前，先擷取系統的影像複本，可以在還原出錯時利用此影像做為回復點。您可以在安裝作業系統及 SQL Server 之後擷取影像複本，然後再還原或重新註冊憑證。


## 還原成員伺服器

1.  準備一部完整網域名稱 (FQDN) 與失敗伺服器相同的乾淨或全新伺服器，然後安裝作業系統，再還原或重新註冊憑證。
    
    > [!NOTE]  
    > 遵循貴組織的伺服器部署程序執行此步驟。
    


2.  從 RTCUniversalServerAdmins 群組成員的使用者帳戶登入所要還原的伺服器。

3.  瀏覽至 Lync Server 安裝資料夾或媒體，並啟動位於 \\setup\\amd64\\Setup.exe 的 \[Lync Server 部署精靈\]。

4.  遵循 \[部署精靈\] 進行下列動作：
    
    1.  執行 \[步驟 1: 安裝本機組態存放區\]，以安裝本機設定檔。
    
    2.  執行 \[步驟 2: 設定或移除 Lync Server 元件\]，以安裝 Lync Server 伺服器角色。
    
    3.  執行 \[步驟 3: 要求、安裝或指派憑證\]，以指派憑證。
    
    4.  執行 \[步驟 4: 啟動服務\]，以啟動伺服器上的服務。
    
    如需執行 \[部署精靈\] 的詳細資訊，請參閱您要還原之伺服器角色的部署文件。

