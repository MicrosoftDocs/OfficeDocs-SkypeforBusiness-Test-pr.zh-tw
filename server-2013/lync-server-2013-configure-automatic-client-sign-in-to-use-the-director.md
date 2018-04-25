---
title: Lync Server 2013：設定用戶端自動登入以使用 Director
TOCTitle: 設定用戶端自動登入以使用 Director
ms:assetid: 85369ffc-53ae-43be-8a23-84a094faecff
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398678(v=OCS.15)
ms:contentKeyID: 49291547
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定用戶端自動登入以使用 Director

 

_**上次修改主題的時間：** 2012-09-08_

部署 Lync Server 2013、Director 或 Director 集區時，建議您使用自動用戶端登入做為最佳作法。如需有關如何設定 DNS 伺服器提供自動用戶端登入功能的詳細資訊，請參閱規劃文件中的＜ [Lync Server 2013 中的自動用戶端登入的 DNS 需求](lync-server-2013-dns-requirements-for-automatic-client-sign-in.md)＞。

如果您已部署自動用戶端登入，請參閱以下小節以在您的 Director 上進行設定。

## 單一 Director 執行個體

如果您已部署自動用戶端登入且其指向 前端伺服器或 前端集區，需要變更 DNS SRV 記錄以使其指向 Director。

## Director 集區

如果您已部署自動用戶端登入且其指向 前端伺服器或 前端集區，需要變更 DNS SRV 記錄以使其指向 Director 集區。

