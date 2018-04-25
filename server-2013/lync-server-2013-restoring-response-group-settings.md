---
title: 還原回應群組設定
TOCTitle: 還原回應群組設定
ms:assetid: 4f8e1949-925d-4538-be1d-9ac7c06b2aca
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh202174(v=OCS.15)
ms:contentKeyID: 52056107
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 還原回應群組設定

 

_**上次修改主題的時間：** 2013-02-18_

如果您部署了回應群組應用程式，而您需要還原後端伺服器或 Standard Edition 伺服器，則也需要還原回應群組組態設定。

## 還原回應群組組態設定

1.  在命令列中輸入：
    
        Import-CsRgsConfiguration -Destination "service:ApplicationServer:<pool FQDN>" -OverwriteOwner -FileName "<path and file name of the backed up file at $Backup>"
    
    例如：
    
        Import-CsRgsConfiguration -Destination "service: ApplicationServer:pool01.contoso.com" -OverwriteOwner -FileName "C:\RgsConfiguration.zip"

