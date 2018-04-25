---
title: Lync Server 2013：在前端伺服器上部署 IP 位址類型
TOCTitle: 在前端伺服器上部署 IP 位址類型
ms:assetid: b6c8e0f9-ec8e-4a4e-a525-756f9cd6b9d0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205191(v=OCS.15)
ms:contentKeyID: 49292079
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 針對 Lync Server 2013 在前端伺服器上部署 IP 位址類型

 

_**上次修改主題的時間：** 2012-06-14_

使用 拓撲產生器執行下列程序中的步驟，以在 前端伺服器上部署 IP 位址類型。

## 在前端伺服器上部署 IP 位址類型

1.  在 \[Enterprise Edition 前端集區\] 下，以滑鼠右鍵按一下集區中的某伺服器，然後選取 \[編輯內容\] 。(或者，選取伺服器後按一下 \[動作\] 功能表中的 \[編輯內容\] 。)

2.  在 \[編輯內容\] 對話方塊中，選取您要設定的 IP 位址類型。若為雙重堆疊設定，請選取 \[啟用IPv4\] 與 \[啟用 IPv6\] ，如下圖所示。
    
    **前端伺服器集區的 \[編輯內容\] 對話方塊**
    
    ![\[前端伺服器編輯內容\] 對話方塊](images/JJ205191.737a9d71-c0bc-4a54-9608-9e028dacc814(OCS.15).png "[前端伺服器編輯內容] 對話方塊")
    
      - **使用所有已設定的 IP 位址**。如果您想允許使用電腦上定義的所有 IP 位址，請選取此選項。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>這是 IP 版本 6 (IPv6) 設定的建議選項。</td>
        </tr>
        </tbody>
        </table>
    
      - **限制服務使用選取的 IP 位址**。選取此選項指定要在新伺服器上使用的位址。如果您選取此選項，您必須輸入 \[主要 IP 位址\] 值。
    
      - **主要 IP 位址**。輸入伺服器將在所有通訊中使用的 IP 位址，除了公開交換電話網路 (PSTN) 之外。輸入的 IP 位址必須符合選取位址類型的格式。
    
      - **PSTN IP 位址**。當中繼伺服器組合在前端伺服器上時，定義 PSTN IP 位址。此位址必須符合選取位址類型的格式。

