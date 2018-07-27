---
title: Lync Server 2013：在中繼伺服器上部署 IP 位址類型
TOCTitle: 在中繼伺服器上部署 IP 位址類型
ms:assetid: 689ebed5-96ee-4cd4-b7ae-ee2a86a1d9b3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204964(v=OCS.15)
ms:contentKeyID: 49291190
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 針對 Lync Server 2013 在中繼伺服器上部署 IP 位址類型

 

_**上次修改主題的時間：** 2014-07-24_

使用 拓撲產生器執行下列程序中的步驟，以在 中繼伺服器上部署 IP 位址類型。

## 在中繼伺服器上部署 IP 位址類型

  - 在 拓撲產生器中的 **\[中繼集區\]** 下，以滑鼠右鍵按一下集區內的伺服器，然後選取 **\[編輯內容\]** (或是選取伺服器，然後在 **\[動作\]** 功能表中按一下 **\[編輯內容\]** )。

  - 在 \[編輯內容\] 對話方塊中，選取您要設定的 IP 位址類型。若為雙重堆疊設定，請選取 \[啟用IPv4\] 與 \[啟用 IPv6\] ，如下圖所示。
    
    **中繼伺服器集區的編輯內容對話方塊**
    
    ![具有 FQDN 的 \[Lync Server 一般內容\] 頁面](images/JJ204964.4e650aca-dbff-4a86-b10d-f0162c032539(OCS.15).png "具有 FQDN 的 [Lync Server 一般內容] 頁面")
    
      - **使用所有已設定的 IP 位址**。如果您想允許使用電腦上定義的所有 IP 位址，請選取此選項。
        
        > [!NOTE]  
        > 這是 IP 版本 6 (IPv6) 設定的建議選項。
        
    
      - **將服務使用方式限制為選取的 IP 位址**。選取此選項指定在新伺服器上使用的特定位址。如果您選取此選項，您必須輸入主要 IP 位址的值。
    
      - **主要 IP 位址**。輸入伺服器將在所有通訊中使用的 IP 位址，除了公開交換電話網路 (PSTN) 之外。輸入的 IP 位址必須符合選取位址類型的格式。
    
      - **PSTN IP 位址**。當中繼伺服器組合在前端伺服器上時，定義 PSTN IP 位址。此位址必須符合選取位址類型的格式。
        
        > [!NOTE]  
        > 不支援安裝額外的網路介面卡 (NIC) 來支援 Lync Server 2013 的 PSTN IP 位址設定。如需受支援 Lync Server 2013 的 NIC 設定詳細資訊，請參閱 <a href="lync-server-2013-server-hardware-platforms.md">Lync Server 2013 的伺服器硬體平台</a>。
        

