---
title: 部署 SEFAUtil 工具
TOCTitle: 部署 SEFAUtil 工具
ms:assetid: fb556e50-88dd-4404-a3d5-be36f5ba41e6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945659(v=OCS.15)
ms:contentKeyID: 52056270
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 部署 SEFAUtil 工具

 

_**上次修改主題的時間：** 2013-01-30_

若要部署及管理群組來電接聽，您必須使用 SEFAUtil Resource Kit 工具。該項工具是 Lync Server 2013 Resource Kit 工具的組件。在您可安裝 SEFAUtil 之前，您的拓撲內必須先有信任的應用程式集區，並指定 SEFAUtil 為信任的應用程式，然後啟用該拓撲。

> [!IMPORTANT]  
> 如果您計劃執行 SEFAUtil 工具，則必須先在電腦安裝 Microsoft Unified Communications Managed API (UCMA) 3.0 Core SDK。



您可以在部署內的任何 前端集區 執行 SEFAUtil。

> [!NOTE]  
> 如需執行 SEFAUtil 的詳細資訊，請參閱 Technet 部落格文章＜如何執行 SEFAutil？＞，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=278940" class="uri">http://go.microsoft.com/fwlink/?linkid=278940</a>。



## 部署 SEFAUtil

1.  以 RTCUniversalServerAdmins 群組成員身分或使用[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)中描述的必要使用者權限，登入裝有 Lync Server 管理命令介面的電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  SEFAUtil 工具只能在信任應用程式集區組件內的電腦執行。請視需要，針對您計劃執行 SEFAUtil 的 前端集區 定義一個信任的應用程式集區。請在命令列執行：
    
        New-CsTrustedApplicationPool -id <Pool FQDN> -Registrar <Pool Registrar FQDN> -site Site:<Pool Site>

4.  定義 SEFAUtil 工具為信任的應用程式。請在命令列執行：
    
        New-CsTrustedApplication -ApplicationId sefautil -TrustedApplicationPoolFqdn <Pool FQDN>  -Port 7489
    
    > [!NOTE]  
    > 視需要，您可以使用不同的連接埠。
    


5.  使用您的變更啟用該拓撲。請在命令列執行：
    
        Enable-CsTopology

6.  在 前端伺服器 安裝 Lync Server 2013 Resource Kit 工具，且必須是您在步驟 3 建立的信任應用程式集區。

7.  確認 SEFAUtil 工具正確執行，如下所示：
    
    1.  以系統管理員權限從 Windows 命令提示字元執行工具，以在您的部署中顯示使用者的電話轉接設定。
        
        > [!NOTE]  
        > 該項工具位於 \Program Files\Microsoft Lync Server 2013\Reskit。
        
    
    2.  顯示使用者電話轉接設定。請在命令列執行：
        
            SEFAUtil.exe <user SIP address> /server:<Lync Server/Pool FQDN>
        
        隨即顯示使用者電話轉接設定。

