---
title: Lync Server 2013 的公開金鑰基礎結構
TOCTitle: Lync Server 2013 的公開金鑰基礎結構
ms:assetid: 737c8a25-23e9-4494-ab76-5a7b729b44ca
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn481131(v=OCS.15)
ms:contentKeyID: 59679125
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 的公開金鑰基礎結構

 

_**上次修改主題的時間：** 2013-11-13_

Microsoft Lync Server 2013 仰賴憑證來進行伺服器驗證，並且在用戶端和伺服器之間及不同的伺服器角色之間建立信任鏈結。Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008 和 Windows Server 2003 公開金鑰基礎結構 (PKI) 提供了建立和驗證這個信任鏈結的基礎結構。

憑證是數位識別碼。其利用名稱識別伺服器與指定其屬性。為確保憑證的資訊有效，其必須由連接到伺服器的用戶端或其他伺服器所信任的CA 核發。若伺服器僅與私人網路上的其他用戶端和伺服器連線，則 CA 可以是企業 CA。若伺服器與私人網路外的實體互動，即可能需要公用 CA。

即使憑證的資訊有效，仍須透過其他方式驗證提供憑證的伺服器，確實是憑證所代表的伺服器。這就是 Windows PKI 的功能所在。

每一個憑證都會連結到公開金鑰。憑證上所指定的伺服器擁有只有本身知道的對應私密金鑰。連接的用戶端或伺服器會使用公開金鑰加密資訊的任意片段，並將其傳送到伺服器。若伺服器能夠解密該資訊，並以純文字回傳，則連接的實體便能確定該伺服器擁有憑證的私密金鑰，因此確實是憑證上署名的伺服器。

> [!NOTE]  
> 並非所有公用 CA 都符合 Lync Server 2013 憑證的需求。建議您參閱通過認證之公用 CA 廠商的清單，以取得您所需要的公用憑證。如需詳細資訊，請參閱＜整合通訊憑證合作夥伴＞(英文)：<a href="http://go.microsoft.com/fwlink/p/?linkid=140898">http://go.microsoft.com/fwlink/p/?LinkId=140898</a>。



## CRL 發佈點

Lync Server 2013 要求所有伺服器憑證應包含一或多個憑證撤銷清單 (CRL) 發佈點。CRL 發佈點 (CDP) 是 CRL 的下載位置，用於確認憑證自發出至今未被撤銷，且仍在有效期間內。CRL 發佈點會以 URL 的形式記錄在憑證屬性中，而且通常是安全的 HTTP。

## 增強金鑰使用方法

Lync Server 2013 要求所有伺服器憑證支援增強金鑰使用方法 (EKU)，以進行伺服器驗證。設定伺服器驗證的 EKU 欄位，即表示憑證可以用於驗證伺服器。EKU 是 MTLS 的必要項目。EKU 中可能會有一個以上的項目，讓憑證可以供多種用途使用。

> [!NOTE]  
> 針對 Live Communications Server 2003 和 Live Communications Server 2005 的輸出 MTLS 連線，用戶端驗證 EKU 是必要項目，但目前已不再需要。然而，以公開 IM 連線連線至 AOL 的 Edge Server 仍須具備此 EKU。


