---
title: 驗證位址
TOCTitle: 驗證位址
ms:assetid: aae557c9-e6f5-4d23-8af1-1d4cd7968c54
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412808(v=OCS.15)
ms:contentKeyID: 49291956
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 驗證位址

 

_**上次修改主題的時間：** 2012-09-17_

在發佈位置資料庫之前，您必須先對照 SIP 主幹或公用交換電話網路 (PSTN) E9-1-1 服務提供者所維護的主要街道地址指南 (MSAG) 驗證新位置。

如需 SIP 主幹 E9-1-1 服務提供者的詳細資訊，請參閱＜[為 Lync Server 2013 選擇 E9-1-1 服務提供者](lync-server-2013-choosing-an-e9-1-1-service-provider.md)＞。

如需關於驗證地址的詳細資訊，請參閱下列 Cmdlet 的 Lync Server 管理命令介面文件：

  - **Get-CsLisServiceProvider**

  - **Set-CsLisServiceProvider**

  - **Remove-CsLisServiceProvider**

  - **Get-CsLisCivicAddress**

  - **Test-CsLisCivicAddress**

## 若要驗證位於位置資料庫中的地址

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  執行下列 Cmdlet 設定緊急服務提供者連線。
    
        $pwd = Read-Host -AsSecureString <password>
        Set-CsLisServiceProvider -ServiceProviderName Provider1 -ValidationServiceUrl <URL provided by provider> -CertFileName <location of certificate provided by provider> -Password $pwd

3.  執行下列 Cmdlet 驗證位置資料庫中的地址。
    
        Get-CsLisCivicAddress | Test-CsLisCivicAddress -UpdateValidationStatus
    
    您也可以使用 **Test-CsLisCivicAddress** Cmdlet 驗證個別地址。

