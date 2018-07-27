---
title: Lync Server 2013 中的反向 Proxy 設定需求
TOCTitle: Lync Server 2013 中的反向 Proxy 設定需求
ms:assetid: c37d688a-28e4-4822-80cc-6add59c71052
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945651(v=OCS.15)
ms:contentKeyID: 52056194
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的反向 Proxy 設定需求

 

_**上次修改主題的時間：** 2013-03-05_

Lync Server 2013 從接著會傳遞給裝載於 Director、Director 集區、前端伺服器或前端集區之外部 Web 服務的外部用戶端加入一些通訊需求。如果您將會議提供給使用者，反向 Proxy 也會負責發行 Office Web Apps Server。

> [!NOTE]  
> Lync Server 2013 不會指定您必須使用的特定反向 Proxy。Lync Server 2013 只會定義反向 Proxy 必須能夠執行的作業需求。您已在基礎結構中部署的反向 Proxy 通常可符合這些需求。



## 反向 Proxy 需求

Lync Server 2013 預期反向 Proxy 執行的功能運作包括：

  - 透過從公用憑證授權單位取得之憑證使用實作安全通訊端層 (SSL) 和傳輸層安全性 (TLS) 以連線至 Director、Director 集區、前端伺服器或前端集區已發行之外部 Web 服務。可使用硬體負載平衡器讓 Director 和前端伺服器在負載平衡集區中。

  - 能夠使用加密憑證發行內部網站，或視需要透過未加密的方式加以發行。

  - 能夠使用完整網域名稱 (FQDN) 發行內部主控網站。

  - 能夠發行所有主控網站的內容。根據預設，您可使用 **/\*** 指示詞，大部分網頁伺服器會將其解讀為「發行網頁伺服器上的所有內容」。您也可以修改指示詞，例如 **/Uwca/\***，這表示「發行在虛擬目錄 Ucwa 下的所有內容」。

  - 必須可設定以要求安全通訊端層 (SSL) 及/或傳輸層安全性 (TLS) 與用戶端的連線可要求已發行網站的內容。

  - 必須使用主體別名 (SAN) 項目接受憑證。

  - 必須能夠將憑證繫結視為接聽程式或介面，因為外部 Web 服務 FQDN 會加以解析。接聽程式設定較介面更佳。許多接聽程式可設定在單一介面上。

  - 必須允許主機標頭處理的設定。通常，由要求用戶端傳送的原始主機標頭必須明確地傳遞，並非由反向 Proxy 加以修改。

  - 從一個外部定義連接埠 (例如 TCP 443) 到另一個定義連接埠 (例如 TCP 4443) 橋接 SSL 和 TLS 流量。反向 Proxy 可解密收到的封包，然後在傳送時重新加密封包。

  - 從一個連接埠 (例如 TCP 80) 到另一個 (例如 TCP 8080) 橋接未加密的 TCP 流量。

  - 允許或接受 NTLM 驗證、無驗證和通過驗證的組態。

