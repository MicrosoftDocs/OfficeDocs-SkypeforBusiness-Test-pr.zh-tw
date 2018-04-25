---
title: 監控 IIS 要求的追蹤記錄檔
TOCTitle: 監控 IIS 要求的追蹤記錄檔
ms:assetid: b6730e92-6d74-4fa7-a83f-50b7bdadbffa
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690034(v=OCS.15)
ms:contentKeyID: 49292082
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 監控 IIS 要求的追蹤記錄檔

 

_**上次修改主題的時間：** 2013-02-14_

當您針對 Lync Server Mobility Service 啟用 Internet Information Services (IIS) 要求的追蹤時，產生的記錄檔每天最多可使用 3 GB 的磁碟空間。預設會啟用 IIS 追蹤記錄。您應該監控前端伺服器以確定未用盡磁碟空間

IIS 預設會在 %SystemDrive%\\inetpub\\logs\\LogFiles 中儲存記錄檔。

若要關閉整部伺服器之 IIS 要求的追蹤，請在命令列輸入下列命令：

    %SystemDrive%\Windows\System32\inetsrv\appcmd set config /section:httpLogging /dontLog:True

如需 **httpLogging** 命令的詳細資訊，請參閱 [http://go.microsoft.com/fwlink/?linkid=234927\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=234927%26clcid=0x404)。

