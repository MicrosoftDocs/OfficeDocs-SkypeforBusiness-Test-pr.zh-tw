---
title: 設定高效能的 Mobility Service
TOCTitle: 設定高效能的 Mobility Service
ms:assetid: c2b8aadb-cffb-49f0-ba7a-e8541a1ff475
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690042(v=OCS.15)
ms:contentKeyID: 49292235
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定高效能的 Mobility Service

 

_**上次修改主題的時間：** 2013-02-17_

當您在 Internet Information Services (IIS) 7.5 上安裝 Lync Server 2013 Mobility Service 時，Mobility Service 安裝程式會在前端伺服器上設定一些效能設定。建議您針對行動功能使用 IIS 7.5。如果在 Windows Server 2008 上使用 IIS 7.0，您必須手動進行這些設定。這些設定會影響 Mobility Service 允許的最大同時使用者要求數目和最大執行緒數目。

效能設定如下：

  - **maxConcurrentThreadsPerCPU** 設為零 (0)。

  - **maxConcurrentRequestsPerCPU** 設為零 (0)。

  - ASP.NET 處理序模型設為 \[自動設定\] (僅適用於 IIS 7.5)。

  - HTTP.sys 佇列限制設為 1,000 (預設值)。

若是使用 IIS 7.0，建議您安裝下列 Microsoft 知識庫文章 2290617 中所提供的更新：＜修正：提供可以為 IIS 7.0 中之各應用程式集區啟用某些 ASP.NET 屬性的設定＞([http://go.microsoft.com/fwlink/?linkid=3052\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=3052%26clcid=0x404))，以只套用 Mobility Service 的變更，而不對其他 Web 服務造成影響。

如果您未安裝知識庫文章 2290617 所提供的更新，下列程序說明如何變更 IIS 7.0 上的 ASP.NET 同時並存要求和執行緒最大數目。不過，即使您未安裝知識庫文章 2290617，也應使用該文章所提供的文件，為 Mobility 內部和外部 IIS 應用程式集區套用相同的變更。在此情況下，請針對 ASP.NET 設定使用不同的設定檔。

> [!IMPORTANT]  
> 如果您使用下列程序變更最大值，此變更會影響所有 IIS 應用程式集區。



如需進行這些設定的詳細資訊，請參閱 [http://go.microsoft.com/fwlink/?linkid=234537\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=234537%26clcid=0x404)。

## 變更同時並存要求和執行緒最大數目

1.  按一下 \[開始\]，然後再按一下 \[執行\]。

2.  在 \[執行\] 方塊中，輸入：
    
        notepad %SystemRoot%\Microsoft.NET\Framework64\v2.0.50727\Aspnet.config

3.  按一下 \[確定\]。

4.  新增或取代下列 \<system.web\> 元素，以做為 Aspnet.config 檔案中 \<configuration\> 元素的子項：
    
        <system.web>
        <applicationPool maxConcurrentRequestsPerCPU="<#>" maxConcurrentThreadsPerCPU="0" requestQueueLimit="5000"/>
        </system.web>
    
    其中 \# 是 0 (若要移除限制) 或如本節稍早所述的新數字。

5.  儲存 Aspnet.config 檔案並關閉 \[記事本\]。

