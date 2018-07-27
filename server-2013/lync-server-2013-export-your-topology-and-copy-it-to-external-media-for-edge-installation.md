---
title: Lync Server 2013：匯出拓撲並將拓撲複製到 Edge 安裝的外部媒體
TOCTitle: 匯出拓撲並將拓撲複製到 Edge 安裝的外部媒體
ms:assetid: def9f416-c519-4a72-b242-7d3057d9c1fd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398983(v=OCS.15)
ms:contentKeyID: 49292547
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 匯出 Lync Server 2013 拓撲並將拓撲複製到 Edge 安裝的外部媒體

 

_**上次修改主題的時間：** 2012-09-08_

在您發行拓撲之後， Lync Server 部署精靈會需要存取 中央管理存放區資料，才能在伺服器上開始進行部署程序。在內部網路中，資料可直接從伺服器取得，但是不在內部網域中的 Edge Server 無法存取資料。若要將拓撲設定資料提供給 Edge Server 部署，您必須先將拓撲資料匯出為檔案，並且將它複製到外部媒體 (例如可從 Edge Server 使用的 USB 磁碟機或網路共用)，然後才在 Edge Server 上執行 Lync Server 部署精靈。利用下列程序將拓撲設定資料提供給您要部署的 Edge Server。

> [!NOTE]  
> 在 Edge Server 上安裝 Lync Server 2013 之後，可使用內部網路中的系統管理工具管理 Edge Server，這樣就會自動將設定複寫至部署中的任何 Edge Server。唯一的例外狀況是指派和安裝憑證以及停止和啟動服務，這兩者必須在 Edge Server 進行。



## 若要使用 Lync Server 管理命令介面將拓撲資料提供給 Edge Server

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  在 Lync Server 管理命令介面中執行下列 Cmdlet：
    
        Export-CsConfiguration -FileName <ConfigurationFilePath.zip>

3.  將匯出的檔案複製到外部媒體 (例如，在部署期間可從 Edge Server 使用的 USB 磁碟機或網路共用)。

