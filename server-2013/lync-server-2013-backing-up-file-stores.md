---
title: 備份檔案存放區
TOCTitle: 備份檔案存放區
ms:assetid: 1a7f4e93-aa3d-461e-878e-2c572baa1293
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh202167(v=OCS.15)
ms:contentKeyID: 52056062
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 備份檔案存放區

 

_**上次修改主題的時間：** 2013-02-17_

備份 Lync Server 檔案存放區，包括 Lync Server 元件所使用的所有檔案和資料夾。

## 若要備份檔案存放區

1.  若要尋找 Lync Server 檔案存放區的特定位置，請開啟拓撲產生器，然後查看 \[檔案存放區\] 節點。

2.  使用 Robocopy 或其他檔案系統管理工具，將每個檔案存放區複製到 $Backup\\filestore。

