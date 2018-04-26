---
title: Lync Server 2013：驗證拓撲設計
TOCTitle: 驗證拓撲設計
ms:assetid: c1b61814-239e-4101-aab0-de3db1d8793c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412951(v=OCS.15)
ms:contentKeyID: 49292215
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中驗證拓撲設計

 

_**上次修改主題的時間：** 2012-01-02_

拓撲產生器 會自動驗證拓撲。任何拓撲錯誤都會被識別為驗證錯誤，並以伺服器角色旁的驗證錯誤圖示表示。此外，驗證此拓撲是否正確表示您的部署拓撲也很重要。

## 若要在發行之前驗證拓撲

1.  檢查所有簡單 URL 皆已設定正確。

2.  確認以 SQL Server 為基礎的伺服器在線上並可供已安裝 拓撲產生器 的電腦使用 (包含任何必要的防火牆規則)。

3.  確認檔案共用可供使用且已定義適當的權限。

4.  確認拓撲中已定義符合部署需求的正確伺服器角色。

5.  驗證伺服器是否存在於 Active Directory 網域服務 中。如果您已將伺服器加入至網域，則會自動發生這種情形。

當您已驗證拓撲且沒有驗證錯誤時，您應可準備發行拓撲。 如果有驗證錯誤，您必須先更正錯誤，才可以發行拓撲。如需發行拓撲的詳細資訊，請參閱 [在 Lync Server 2013 中發行拓撲](lync-server-2013-publish-the-topology.md)。

