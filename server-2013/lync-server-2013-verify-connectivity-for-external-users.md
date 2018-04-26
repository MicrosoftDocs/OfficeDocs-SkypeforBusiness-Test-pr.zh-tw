---
title: Lync Server 2013：驗證外部使用者的連線能力
TOCTitle: 驗證外部使用者的連線能力
ms:assetid: 5c02bd6e-1c96-448a-a21d-58c9961c6640
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398402(v=OCS.15)
ms:contentKeyID: 49291033
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中驗證外部使用者的連線能力

 

_**上次修改主題的時間：** 2012-10-19_

要驗證外部使用者連線能力，必須先確保從使用者至伺服器，以及 Access Edge Service 連接埠的連線能力。

一個非常有用的資源可以針對需要外部使用者存取的情況下，確認您設定以及連線、傳送與接收正確訊息的能力：遠端連線分析程式網站 ( <https://www.testocsconnectivity.com/>)。該網站由 Microsoft 支援服務所管理及維護。如要瀏覽遠端連線分析程式，請在瀏覽器中開啟該網站，然後遵循指示來選取案例。

## 測試外部使用者與外部存取連線能力

測試外部使用者存取時，必須包括組織支援的每一種外部使用者類型，包含下列任一或全部項目：

  - 來自至少一個同盟網路、測試 IM、目前狀態、A/V 與桌面共用的使用者。

  - 組織所支援的每個公用 IM 服務提供者 (以及已經完成佈建作業) 的使用者。

  - 匿名使用者。

  - 從遠端登入 Lync (但不是透過 VPN) 的組織內使用者。

這些測試決定了您的 Edge Server 是否：

  - 使用網路外部的 telnet 用戶端聆聽必要的連接埠。
    
      - 範例：telnet sip.contoso.com 443
    
      - 依據您的部署，透過 Edge Server 或 Edge Server 集區對您使用的連接埠執行先前測試。

  - 執行準確的外部 DNS 解析。
    
      - 從網路外部偵測 (ping) Edge 或 Edge 集區的個別外部 FQDN。即使偵測 (ping) 作業失敗，您還是會看到 IP 位址，方便您與指派的 IP 位址進行比較。

