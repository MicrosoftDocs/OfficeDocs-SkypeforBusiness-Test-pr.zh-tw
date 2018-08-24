---
title: Lync Server 2013：監控網路效能
TOCTitle: 監控網路效能
ms:assetid: bc3a01da-91eb-4c0c-9598-35e5e46b00f6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn720923(v=OCS.15)
ms:contentKeyID: 62240028
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 監控 Lync Server 2013 中的網路效能

 

_**上次修改主題的時間：** 2015-08-17_

Lync Server 2013 是一種即時通訊技術，嚴重依賴網路來啟用使用者之間的通訊，可透過立即訊息 (IM)、語音通話或視訊通訊。因此對持續監控網路效能來說很重要，可協助保證使用者已選的通訊形式會提供盡可能最佳的體驗。

網路效能共用兩種測量等級：

  - **整體網路效能**   此效能測量等級將能讓組織建立其網路的「全面」檢視，通常可透過協力廠商網路監控系統來實作。這些系統將會從整個網路中的遠端網路裝置 (例如路由器和切換器) 接收效能和容量資料，讓系統管理員在當天任何時間都能判斷任何指定網路元件的狀況。

  - **個別伺服器效能**   這種效能測量等級限於特定伺服器，能協助系統管理員評估特定伺服器的網路效能，並能協助疑難排解特定效能問題，或評估個別伺服器經過一段指定期間的效能以作為容量規劃程序的一部分。

您可以使用下節所述的工具來監控網路。

## 整體網路效能監控的工具

## System Center Operations Manager 2012

System Center Operations Manager 會提供端對端服務管理，不僅易於自訂，還能針對 IT 環境中提升的服務等級延伸。這能讓作業和 IT 管理團隊找出和解決影響分散式 IT 服務狀況的問題。端對端服務管理不限於以 Microsoft 為主的環境。支援管理適用的 Web 服務 (WS 管理)、簡易網路管理通訊協定 (SNMP)，而且夥伴解決方案允許非執行 Microsoft 作業系統和硬體的系統納入 System Center Operations Manager 2012 內的服務監控中。

## System Center Operations Manager 2012 和協力廠商網路管理解決方案

**EMC Smarts**   作業管理員適用的 EMC 解決方案可協助您快速解決影響整體服務等級的問題。使用作業管理員適用的 EMC 解決方案之後，您就可以使用一個整合的自動化解決方案來管理和監控整個 IT 服務鏈。您將能輕鬆找出效能和可用性問題的根本原因，更快速地解決問題以降低影響和成本。主要效益包含下列項目：

  - 先進易用的管理   著重於提供策略商業價值，而非手動儲存和篩選令人困擾的警示。

  - **更快速的解析**   更快速地解決 IT 問題並回應商業需求，降低影響和成本。

  - **簡化的作業**   結合多個管理工具、應用程式和終端機，免除 IT 複雜性。

更多資訊請見此處：

[Microsoft System Center Operations Manager](http://go.microsoft.com/fwlink/p/?linkid=243651)

[Microsoft System Center Operations Manager 適用的解決方案](http://www.emc.com/collateral/software/data-sheet/h6135-server-manager-ds.pdf)

## 協力廠商解決方案

**HP 網路管理中心 (舊稱為 HP OpenView)**   [HP 網路管理中心](https://h10078.www1.hp.com/cda/hpms/display/main/hpms_content.jsp?zn=bto%26cp=1-11-15-119_4000_100__) 提供整合的錯誤和效能管理，以改善網路可用性和效能。網路管理中心是 HP 自動化網路管理解決方案的一部分，會整合錯誤、效能、組態和變更管理。

**Cisco 網路管理和自動化產品**   Cisco 針對企業提供數數種管理產品，包括 CiscoWorks LAN Management Solution 和 Cisco Network Analysis Module，以協助改善作業效率並降低網路停機時間。如需這些產品的額外資料，請參考 Cisco 網站，網址為 [http://www.cisco.com/en/US/products/sw/netmgtsw/index.html](http://www.cisco.com/en/us/products/sw/netmgtsw/index.html)。

簡易網路管理通訊協定 (SNMP)   簡易網路管理通訊協定 (SNMP) 是一種網路管理標準，可定義 TCP/IP 網路的管理策略。SNMP 可讓您擷取有關網路的設定和狀態資訊，並將資訊傳送至指定的電腦以供事件監控。這項基於網路管理通訊協定的標準會使用分散式架構，其中包括下列項目：

  - 多個受管理節點，每個節點都具備稱為代理的 SNMP 實體，其可讓您遠端存取管理檢測設備。

  - 至少有一個 SNMP 實體已知為執行管理應用程式以監控並控制受管理元素的管理員。受管理元素為像是主機、路由器等的裝置。透過存取其管理資訊可監控並控制這些裝置。

  - SNMP 這種管理通訊協定會用於在管理站和代理之間通訊管理資訊。管理資訊會參考位於虛擬資訊存放區 (稱為管理資訊基地，MIB) 的受管理物件集。

> [!NOTE]  
> 以上提供協力廠商網路監控解決方案的範例。此清單不具決定性，Microsoft 並未偏好任何特定的廠商解決方案。請向網路服務提供者和/或個別的技術提供者諮詢，以為組織決定最適合的網路監控解決方案。



## 監控個別伺服器網路效能的工具

## System Center Operations Manager 2012

System Center Operations Manager 2012 允許系統管理員透過 Windows Server 2012 管理套件來檢視個別伺服器的網路效能：Windows Server 作業系統管理套件包含「效能」管理套件，可讓系統管理員監控網路介面卡效能和介面卡狀況。

## Windows 網路監視器

收集、顯示、分析伺服器上的資源使用量，並測量網路流量。網路監視器會獨家監控網路活動。透過擷取並分析網路資料並使用這項具有效能記錄的資料，您就可以判斷網路使用量、找出網路問題，以及預測未來網路需求。

如需有關網路監視器 3.4 的詳細資訊，和欲瞭解如何安裝和設定網路監視器並擷取和分析資料，請參閱此節：網路監視器 3.3 概觀。此外，請參網路監視器部落格，網址為：<http://blogs.technet.com/b/netmon/>。

