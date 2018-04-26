---
title: 在 Lync Server 2013 中設定次要位置資訊服務
TOCTitle: 在 Lync Server 2013 中設定次要位置資訊服務
ms:assetid: 083ffbc6-7c18-4141-85f9-8825b62c3d10
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398138(v=OCS.15)
ms:contentKeyID: 49290004
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定次要位置資訊服務

 

_**上次修改主題的時間：** 2012-10-30_

Lync Server 2013 提供的 Web 服務介面可讓您用來將位置資訊服務指向次要位置來源 (SLS) 資料庫。連線至 SLS 資料庫的 Web 服務介面必須符合位置資訊服務 WSDL。如果位置資料庫和次要位置資料庫都已設定，位置資訊服務會先查詢位置資料庫，若找不到相符項目，則會將用戶端的位置要求傳送至 SLS 資料庫。如果此位置是在 SLS 中，則位置資訊服務會將此位置傳送回用戶端。

如需詳細資訊，請參閱 Lync Server 管理命令介面 文件中的下列 Cmdlet：

  - **Set-CsWebServiceConfiguration**

## 若要設定次要位置資料庫

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  執行下列 Cmdlet 以設定次要位置資料庫的位置 URL。
    
        Set-CsWebServiceConfiguration -SecondaryLocationSourceURL "<web service url>"

