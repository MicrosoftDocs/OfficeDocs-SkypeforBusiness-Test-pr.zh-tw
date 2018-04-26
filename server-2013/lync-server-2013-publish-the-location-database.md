---
title: 在 Lync Server 2013 中發佈位置資料庫
TOCTitle: 在 Lync Server 2013 中發佈位置資料庫
ms:assetid: dd032b5b-df0e-4017-ac46-e17570c1ab1e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398974(v=OCS.15)
ms:contentKeyID: 49292536
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中發佈位置資料庫

 

_**上次修改主題的時間：** 2012-10-30_

新增至位置資料庫的新位置必須等到發佈之後，才可供用戶端使用。

如需詳細資訊，請參閱 Lync Server 管理命令介面 文件中的下列 Cmdlet：

  - **Publish-CsLisConfiguration**

如果您使用「緊急位置識別碼」(ELIN) 道，也必須將 ELIN 上傳至公用交換電話網路 (PSTN) 電訊廠商的「自動位置識別」(ALI) 資料庫。PSTN 電訊廠商可能會要求您使用特定的 ELIN 記錄格式。如需詳細資訊，請連絡 PSTN 電訊廠商。您可以匯出位置資訊服務資料庫中的資料並視需要加以格式化。

## 若要發佈位置資料庫

  - 啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

  - 執行下列 Cmdlet 以發佈位置資料庫。
    
        Publish-CsLisConfiguration

