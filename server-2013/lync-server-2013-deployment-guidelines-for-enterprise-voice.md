---
title: Lync Server 2013：Enterprise Voice 的部署指導方針
TOCTitle: Enterprise Voice 的部署指導方針
ms:assetid: 8985bd93-7613-4cef-9c89-51df6049ed9b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398694(v=OCS.15)
ms:contentKeyID: 49291584
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中 Enterprise Voice 的部署指導方針

 

_**上次修改主題的時間：** 2012-09-21_

本主題說明在規劃部署 Lync Server 2013 和 企業語音工作負載時應考量的先決條件和其他指導方針。

## 部署先決條件

若要在部署 企業語音 時有最佳的經驗，請確定您的 IT 基礎結構、網路和系統都符合下列先決條件：

  - 網路上已安裝 Lync Server 2013 Standard Edition 或 Enterprise Edition，而且運作正常。

  - 所有 Edge Server 都已部署在周邊網路中，而且運作正常，包括搭配 Access Edge Service、 A/V Edge 服務、 Web Conferencing Edge Service 及反向 Proxy 的 Edge Server。

  - 已為 Lync Server 建立並啟用一個或多個使用者。

  - 已安裝 Microsoft Exchange Server 2007 Service Pack 1 (SP1)、最新的 Service Pack 或 Microsoft Exchange Server 2010。需有上述其中一項才能整合 Exchange 整合通訊 (UM) 和 Lync Server，為用戶端端點提供豐富的通知及電話記錄資訊。

  - 已經針對每一個要啟用 企業語音的使用者指定和正規化唯一的主要電話號碼，並將它複製到 **msRTCSIP-line** 屬性。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Lync Server 支援 E.164 號碼和非直接向內撥號 (DID) 號碼。非 DID 號碼可以用 <strong>&lt;E.164&gt;;ext=&lt;extension&gt;</strong> 格式或數字字串表示，條件是私人分機號碼在企業中是唯一的。例如，1001 這個私人號碼就可以用 <strong>+1425550100;ext=1001</strong> 或 <strong>1001</strong> 表示。以 <strong>1001</strong> 表示時，此私人號碼在整個企業中應該要是唯一的。</td>
    </tr>
    </tbody>
    </table>


  - 部署 企業語音的系統管理員應該是 RTCUniversalServerAdmins 群組的成員。

  - 至少已成功部署 Office Communicator 2007。若要使用此版本的新功能，必須部署 Lync 2013。

  - 已經使用 Microsoft 或協力廠商憑證授權單位 (CA) 的基礎結構，完成 Managed 金鑰基礎結構 (MKI) 的部署和設定。

  - 安裝中繼伺服器的每一部電腦都必須：
    
      - 是某個網域的成員伺服器，且已準備好用於 Active Directory 網域服務。如需 Active Directory 網域服務 準備程序，請參閱部署文件中的 [為 Lync Server 2013 準備 Active Directory 網域服務](lync-server-2013-preparing-active-directory-domain-services.md)。
    
      - 執行下列其中一個作業系統：
        
          -   
            64 位元版本的 Windows Server 2008 Standard 作業系統
        
          -   
            64 位元版本的 Windows Server 2008 Enterprise 作業系統

  - 如果公用交換電話網路 (PSTN) 或專用交換機 (PBX) 連線是藉由分時多工 (TDM) 連線而建立，則可以部署一個或多個 PSTN 閘道 (如果連線是藉由 SIP 主幹建立，則不需要 PSTN 閘道)。

## 電力、網路或電話服務中斷

如果您所在位置出現電力、網路或電話服務中斷、干擾或其他品質降低的情形，語音、立即訊息、顯示狀態和 Lync Server 的其他功能，以及連接至 Lync Server 的任何裝置都可能無法正常運作。

## Enterprise Voice 的運作有賴於伺服器的可用性和 VoIP 用戶端與硬體的可操作性

透過 Lync Server 的語音通訊依賴伺服器軟體的可用性，以及連接到伺服器軟體之語音用戶端或硬體電話裝置的正常運作。

## 連絡緊急服務的替代方法

針對您安裝語音用戶端的位置 (例如，執行 Lync 用戶端的電腦或 Lync Phone Edition 裝置)，建議您保留一個備用方法，當發生電力故障、網路連線能力變低、電話服務中斷或可能妨礙 Lync Server、 Lync 或 Lync Phone Edition 裝置的作業等其他問題時，能讓使用者撥打緊急服務 (如 911 或 999)。這類替代選項可以包含連接至標準公用交換電話網路線路的電話或行動電話。 UNRESOLVED\_TOKEN\_VAL()

## 緊急救援電話與多線路電話系統

使用多線路電話系統 (MLTS) 可能會受到美國境內各州或聯邦法律和其他國家/地區法律的管制，要求 MLTS 在撥號者請求緊急服務時 (例如，撥打 911 或 999 等緊急聯絡號碼時)，提供撥號者的電話號碼、分機及/或實際位置給適當的緊急服務。在此版本中，您可以設定 Lync Server 以將撥號者的實際位置提供給緊急服務提供者，如＜ [在 Lync Server 2013 中規劃緊急服務 (E9-1-1)](lync-server-2013-planning-for-emergency-services-e9-1-1.md)＞所述。 Lync Server、 Lync 及 Lync Phone Edition 裝置的購買者必須自行負責遵守這些 MLTS 法律的事宜。

