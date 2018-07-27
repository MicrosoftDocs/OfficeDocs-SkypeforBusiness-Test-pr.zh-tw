---
title: Lync Server 2013：SIP 主幹上的通話許可控制
TOCTitle: SIP 主幹上的通話許可控制
ms:assetid: 7eada098-3d47-4be2-839f-8f87d582efe8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398632(v=OCS.15)
ms:contentKeyID: 49291455
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 SIP 主幹上的通話許可控制

 

_**上次修改主題的時間：** 2012-09-22_

若要在 SIP 主幹上部署通話許可控制 (CAC)，您必須建立代表網際網路電話語音服務提供者 (ITSP) 的網路網站。若要在 SIP 主幹上套用頻寬原則值，您可以在企業中的網路網站與您建立以代表 ITSP 的網路網站之間，建立網站間原則。

下圖顯示在 SIP 主幹上部署 CAC 的範例。

**SIP 主幹上的 CAC 組態**

![通話許可控制 SIP 主幹圖表](images/Gg398632.276c0d8f-1dd5-4883-8499-c202399ddbe9(OCS.15).jpg "通話許可控制 SIP 主幹圖表")

若要在 SIP 主幹上設定 CAC，您必須在 CAC 部署期間執行下列工作：

1.  建立代表 ITSP 的網路網站。讓此網路網站與適當的網路地區相關聯，並為此網路網站的音訊與視訊功能配置零的頻寬。如需詳細資訊，請參閱部署文件中的＜ [在 Lync Server 2013 中設定 CAC 的網站](lync-server-2013-configure-network-sites-for-cac.md)＞。
    
    > [!NOTE]  
    > 對 ITSP 而言，此網路網站組態沒有作用。頻寬原則值實際是在步驟 2 套用。
    


2.  針對您在步驟 1 建立的網站使用相關的參數值，建立 SIP 主幹的網站間連結。例如，您可以使用企業中網路網站的名稱作為 NetworkSiteID1 參數的值，並以 ITSP 網路網站作為 NetworkSiteID2 參數的值。如需詳細資訊，請參閱部署文件中的＜ [在 Lync Server 2013 中建立網路站間原則](lync-server-2013-create-network-intersite-policies.md)＞。另請參閱 Lync Server 管理命令介面文件中有關 New-CsNetworkInterSitePolicy Cmdlet 的部分。

3.  從您的 ITSP 取得工作階段界限控制器 (SCB) 之媒體終端點的 IP 位址。將具有子網路遮罩 32 的 IP 位址新增至代表 ITSP 的網路網站。如需詳細資訊，請參閱＜ [在 Lync Server 2013 中建立子網路與網路站台的關聯](lync-server-2013-associate-a-subnet-with-a-network-site.md)＞。

