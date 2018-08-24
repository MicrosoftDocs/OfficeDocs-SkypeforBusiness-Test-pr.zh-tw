---
title: Lync Server 2013 會議元件與拓撲
TOCTitle: 會議元件與拓撲
ms:assetid: eb83052a-3360-4ba1-a6a0-6ee419942809
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399061(v=OCS.15)
ms:contentKeyID: 49292702
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的會議元件與拓撲

 

_**上次修改主題的時間：** 2013-02-04_

在 拓撲產生器中選擇會議時，會議會部署為 前端伺服器或 Standard Edition 伺服器的一部分。要使用電話撥入式會議與 PowerPoint 共用，需要其他元件與設定。下節說明支援 Web 會議、A/V 會議與撥入式會議的元件與拓撲。

## 支援的元件

Web 會議與 A/V 會議需要的唯一元件是貴公司的 前端伺服器或 Standard Edition 伺服器。如需 前端伺服器與 Standard Edition 伺服器的硬體與軟體需求清單，請參閱 [Lync Server 2013 的受支援硬體](lync-server-2013-supported-hardware.md) 與 [Lync Server 2013 中的伺服器軟體和基礎結構支援](lync-server-2013-server-software-and-infrastructure-support.md)。

Lync Server 2013 使用 Office Web Apps 與 Office Web Apps Server 處理 PowerPoint 簡報的共用與轉譯問題。如需安裝與安裝 Office Web Apps Server 的詳細資訊，請參閱＜ [設定 Office Web Apps Server 與 Lync Server 2013 的整合](lync-server-2013-enabling-office-web-apps-server-and-lync-server-2013.md)＞。

除了 Web 會議與 A/V 會議的需求，電話撥入式會議還使用下列 Lync Server 2013 元件：

  - **應用程式服務**    應用程式服務 提供部署、主控及管理整合通訊 (UC) 應用程式的平台。電話撥入式會議使用兩個需要 應用程式服務 的 UC 應用程式：會議服務員與會議宣告。部署會議工作負載並選擇電話撥入式會議選項時， 前端集區的每個 前端伺服器及 Standard Edition 伺服器依預設都會安裝並啟動 應用程式服務。

  - **會議服務員應用程式**    會議服務員應用程式是一款整合通訊應用程式，可接收公用交換電話網路 (PSTN) 通話、播放提示，以及將通話加入 A/V 會議。部署會議負載及選取電話撥入式會議選項時，系統即會依預設安裝及啟用 會議服務員應用程式。

  - **會議宣告應用程式**    會議宣告應用程式是一款整合通訊應用程式，它能根據某些動作播放音調和提示給 PSTN 參與者。例如參與者加入或離開會議時，參與者處於靜音或解除靜音狀態時，某人進入會議大廳時，或是會議遭到鎖定或解除鎖定時。 會議宣告應用程式也支援從電話按鍵執行複頻式訊號 (DTMF) 命令。部署會議負載及選取電話撥入式會議選項時，系統即會依預設自動安裝及啟用 會議宣告應用程式。

  - **電話撥入式會議設定頁面**    電話撥入式會議設定頁面顯示會議撥入號碼及其可用語言、指派的會議資訊 (即針對不需排程的會議所提供的資訊) 與會議中 DTMF 控制項，並可讓使用者管理其個人識別碼 (PIN) 與指派的會議資訊。 電話撥入式會議設定頁面會自動安裝成為 Web 服務的一部分。

  - **Lync Server 2013、 中繼伺服器與 PSTN 閘道**   電話撥入式會議需要 中繼伺服器 才能轉譯 Lync Server 2013 和 PSTN 閘道間的訊號 (在某些設定中為媒體)，同時也需要 PSTN 閘道才能轉譯 中繼伺服器 PSTN 閘道間的訊號和媒體。對於電話撥入式會議，您至少必須部署一部 中繼伺服器和以下任一項目：
    
      - PSTN 閘道
    
      - IP-PBX
    
      - 工作階段界限控制器 (SBC) (適用於藉由設定 SIP 主幹而連接的網際網路電話語音服務提供者)
    
    > [!NOTE]  
    > 如果您同時部署了 企業語音、 中繼伺服器與 PSTN 閘道均包含在 企業語音部署中。如果您未部署 企業語音，您必須至少部署一部 中繼伺服器，以及至少一個 PSTN 閘道、IP-PBX 或 SBC 才能進行電話撥入式會議。
    


  - **檔案存放區**   檔案存放區適用於記錄名稱音訊檔案。檔案存放區是每個 Enterprise Edition 或 Standard Edition 部署的標準元件。

  - **使用者存放區**   使用者存放區可用來存放使用者 Lync Server 2013 PIN。PIN 需經過雜湊處理。使用者存放區是每個 Enterprise Edition 或 Standard Edition 部署的標準元件。

  - **Lync Server 控制台**   某些撥號設定可藉由使用 Lync Server 控制台來設定。

  - **Lync Server 管理命令介面**   所有撥號設定均可藉由使用 Lync Server 管理命令介面 Cmdlet 來設定。 Lync Server 管理命令介面 Cmdlet 適用於部署、設定、執行、監控及疑難排解 會議服務員應用程式與 會議宣告應用程式。如需特定 Cmdlet 的詳細資訊，請參閱 Lync Server 管理命令介面 文件。

## 支援的拓撲

在 Lync Server 2013 中，執行會議的伺服器始終會與 前端伺服器或 Standard Edition 伺服器共置。第一次部署期間， 拓撲產生器會讓您選擇是否將會議納入拓撲。您也可使用 拓撲產生器將會議新增至現有的部署。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中定義和設定拓撲](lync-server-2013-defining-and-configuring-the-topology.md)＞。

## 電話撥入式會議拓撲

您可以在下列拓撲和組態中部署電話撥入式會議：

  - Lync Server 2013Standard Edition

  - Lync Server 2013Enterprise Edition

  - 包含或不包含 企業語音

您可以在中央網站部署 應用程式服務、 會議服務員應用程式和 會議宣告應用程式，但是不能在分支網站中部署。

> [!NOTE]  
> 如果您要部署電話撥入式會議，則在部署 Lync Server 2013 會議的每個集區中都要部署。您不需要在每個集區中指派存取號碼，但是必須在每個集區中部署電話撥入式會議功能。此需求的存在，是為了在使用者從其中一個集區撥打存取號碼以加入不同集區中的 Lync Server 2013 會議時，能夠支援記錄名稱功能。



## 支援 Lync Server 2013 與 Office Web Apps 的拓撲

Lync Server 2013 提供下列方式來設定 Office Web Apps Server。視需求而定，您可以執行下列作業：

  - **在內部、公司的防火牆後以及同一個網路區域內，同時安裝 Lync Server 2013 與 Office Web Apps Server。** 有了此拓撲，要從外部存取 Office Web Apps Server，將只能透過反向Proxy 伺服器進行。 Lync Server 2013 與 Office Web Apps Server (或 Office Web Apps Server 伺服器陣列) 會安裝在內部與公司的防火牆後。理想中，您應該能在與 Lync Server 同一個網路區域內安裝 Office Web Apps Server。
    
    要將外部 Lync 用戶端連線至 Lync Server 2013 與 Office Web Apps Server，可使用反向 Proxy 伺服器，此伺服器可接收網際網路的要求，然後轉傳到內部網路。(內部用戶端不需要使用反向 Proxy 伺服器，因為他們可以直接連接到 Office Web Apps Server。) 此拓撲在使用 Lync Server 2013 專用的 Office Web Apps Server 伺服器陣列時效果最好。

  - **使用外部部署的 Office Web Apps Server**
    
    在此拓撲中， Lync Server 2013 部署在內部，且使用部署在 Lync Server 網路區域外部的 Office Web Apps Server。若在公司多個應用程式間分享 Office Web Apps Server，且將其部署在需要 Lync Server 才能使用 Office Web Apps Server 外部介面的網路中 (反之亦然)，則可能發生此情況。
    
    您不需要安裝反向 Proxy 伺服器； Office Web Apps Server 到 Lync Server 2013 的所有要求會透過您的 Edge Server 傳閱。內部與外部 Lync 用戶端使用外部 URL 連接到 Office Web Apps Server。
    
    若 Office Web Apps Server 部署在內部防火牆外部，請在 拓撲產生器中選取 \[Office Web Apps Server 部署在外部網路 (也就是周邊/網際網路)\] 選項。如需詳細資訊，請參閱＜ [設定 Office Web Apps Server 與 Lync Server 2013 的整合](lync-server-2013-enabling-office-web-apps-server-and-lync-server-2013.md)＞。

不管選取的拓撲為何，重點是要開啟正確的防火牆連接埠。您必須確認 DNS 名稱、IP 位址與連接埠未被 Office Web Apps Server、負載平衡器或 Lync Server 的防火牆阻擋。

> [!NOTE]  
> 從外部存取 Office Web Apps Server 的其他選項，是在周邊網路部署伺服器。若您選取該選項，請記住，要安裝 Office Web Apps Server，伺服器電腦必須是 Active Directory 網域的成員。除非網路原則允許周邊網路的電腦成為 Active Directory 網域的成員，否則建議您不要在周邊網路安裝 Office Web Apps Server。請改在內部網路安裝 Office Web Apps Server，並讓外部使用者透過反向 Proxy 伺服器存取。


