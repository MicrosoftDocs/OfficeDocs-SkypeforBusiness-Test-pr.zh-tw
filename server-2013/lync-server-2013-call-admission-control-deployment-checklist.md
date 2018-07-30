---
title: Lync Server 2013 中的通話許可控制部署檢查清單
TOCTitle: Lync Server 2013 中的通話許可控制部署檢查清單
ms:assetid: d56a525f-3da5-4ac0-a311-0c5efd98c9df
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398928(v=OCS.15)
ms:contentKeyID: 49292455
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的通話許可控制部署檢查清單

 

_**上次修改主題的時間：** 2012-10-22_

使用下列檢查清單來確認您已完成部署通話許可控制 (CAC) 的所有必要設定工作。

  - 如果已部署一個或多個 Edge Server，則必須將每個外部介面 IP 位址新增至網路組態設定中的子網路清單 (使用位元遮罩 32)。您也應該讓此子網路 (IP 位址) 與網站 ID 產生關聯，以供部署 A/V Edge 服務的地理位置使用。
    
    > [!NOTE]  
    > 實作 CAC 不需要 Edge Server。
    


  - 確認 CAC 已啟用 (透過 Lync Server 控制台或執行[在 Lync Server 2013 中啟用通話許可控制](lync-server-2013-enable-call-admission-control.md)中所指定的 Cmdlet 來啟用)。

  - 確認已在所有中央網站啟用 CAC。您可以透過拓撲產生器完成此作業。如果在發行時產生警告，請不要忽略該警告。

  - 確認已在網路組態設定中設定在企業網路中管理的所有子網路。此外，也務必要關聯每個子網路與網站，如[在 Lync Server 2013 中建立子網路與網路站台的關聯](lync-server-2013-associate-a-subnet-with-a-network-site.md)中所說明。

  - 確認已在網路組態設定中設定所有前端伺服器、Survivable Branch Appliance (SBA)、音訊/視訊會議伺服器 (如果位於不同集區中) 以及中繼伺服器的子網路或 IP 位址。

