---
title: 移動 Exchange 整合通訊連絡人物件
TOCTitle: 移動 Exchange 整合通訊連絡人物件
ms:assetid: 35c7e987-41b5-4798-b617-3303f20e52e3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688022(v=OCS.15)
ms:contentKeyID: 49890020
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移動 Exchange 整合通訊連絡人物件

 

_**上次修改主題的時間：** 2012-10-19_

若要將自動語音應答 (AA) 和訂閱者存取 (SA) 連絡人物件移轉至新的 Lync Server 2013 部署，請先使用 **Get-CsExUmContact** 和 **Move-CsExUmContact** Cmdlet，將物件從舊版 Office Communications Server 2007 R2 部署移至新的 Lync Server 2013 部署。在 Exchange Server 上，則請執行 **ExchUCUtil**Windows PowerShell 指令碼，針對最新部署的 Lync 集區執行下列動作：

  - 將其新增至整合通訊 IP 閘道。

  - 將其新增至整合通訊群組搜尋。

> [!NOTE]  
> 若要使用 <strong>Get-CsExUmContact</strong> 和 <strong>Move-CsExUmContact</strong> Cmdlet，您必須是 RTCUniversalUserAdmins 群組的成員，且具備連絡人物件存放所在的組織單位 (OU) 權限。使用 <strong>Grant-OUPermission</strong> Cmdlet，即可授與此 OU 權限。



## 使用 Lync Server 管理命令介面移動連絡人物件

1.  開啟 Lync Server 管理命令介面。

2.  針對每個登錄至 Exchange UM 的集區 (其中 pool1.contoso.net 是 Office Communications Server 2007 R2 部署的集區，而 pool2.contoso.net 是 Lync Server 2013 部署的集區)，在命令列輸入下列命令：
    
        Get-CsExUmContact -Filter {RegistrarPool -eq "pool01.contoso.net"} | Move-CsExUmContact -Target pool02.contoso.net
    
    若要確認連絡人物件是否移動，請執行 **Get-CsExumContact** Cmdlet 並確認 **\[RegistrarPool\]** 現在已指向新集區。

## 執行 ExchUCUtil Windows PowerShell 指令碼

1.  以具備 Exchange 組織系統管理員權限的使用者登入 Exchange UM Server。

2.  瀏覽至 ExchUCUtil Windows PowerShell 指令碼。
    
    在 Exchange 2007 中，ExchUCUtil.ps1 位於： **%Program Files%\\Microsoft\\Exchange Server\\Scripts\\ExchUCUtil.ps1**
    
    在 Exchange 2010 中，ExchUCUtil.ps1 位於： **%Program Files%\\Microsoft\\Exchange Server\\V14\\Scripts\\ExchUCUtil.ps1**

3.  如果 Exchange 部署在單一樹系中，請輸入：
    
        exchucutil.ps1
    
    或者，如果 Exchange 部署在多個樹系中，請輸入：
    
        exchucutil.ps1 -Forest:" <forest FQDN>"
    
    其中 *forest FQDN* 是指已部署 Lync Server 2013 的樹系。
    
    > [!IMPORTANT]  
    > 請務必在執行 exchucutil.ps1 之後 ，重新啟動 <strong>[Lync Server 前端]</strong> 服務 (rtcsrv.exe)。 否則， Lync Server 2013 將偵測不到拓撲中的整合通訊。
    

