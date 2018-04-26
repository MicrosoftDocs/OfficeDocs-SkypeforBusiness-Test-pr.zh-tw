---
title: Lync Server 2013 中的 Web 會議需求
TOCTitle: Lync Server 2013 中的 Web 會議需求
ms:assetid: 125f847c-58ab-450f-ae43-41219fd38477
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ619171(v=OCS.15)
ms:contentKeyID: 49290151
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Web 會議需求

 

_**上次修改主題的時間：** 2013-01-30_

如果您已選擇要啟用 Web 會議，則需規劃下列事項：

  -   
    存取檔案存放區，以用來儲存 Web 會議內容。

  -   
    與 Office Web Apps Server 整合，在會議期間共用 PowerPoint 檔案時所需。

## 檔案存放區

Lync Server 2013 Web 會議服務會將會議期間共用的內容儲存在檔案存放區中。在部署過程中，您必須指定要用來做為 Standard Edition Server 或 Enterprise Edition前端集區檔案存放區的檔案共用。您可以使用現有的檔案共用做為檔案存放區，也可以指定新的檔案共用。若要指定新的檔案共用，請指定檔案共用將位於的檔案伺服器之完整網域名稱 (FQDN)，以及要做為新檔案共用的資料夾名稱。如需詳細資訊，請參閱＜拓撲產生器 – 定義前端的檔案存放區＞。Web 會議服務會先將內容加密，再將內容儲存在檔案存放區中。

Lync Server 2013 支援在直接連結存放裝置 (DAS) 或存放區域網路 (SAN) 上 (包括分散式檔案系統 (DFS)) 使用檔案共用，以及在獨立磁碟容錯陣列 (RAID) 上進行檔案儲存。在 Lync Server 部署精靈定義檔案共用的位置之後，Lync Server 會在檔案共用中建立資料夾結構，類似下方：

  - 1-ApplicationServer-1

  - 1-CentralMgmt-1

  - 1-WebServices-1
    
      - CollabContent
    
      - CollabMetadata
    
      - DataConf

然後 Web 會議服務會將 PowerPoint 投影片、白板、輪詢及附件之類的內容，儲存在 CollabContent 和 CollabMetadata 資料夾中 (位在 WebServices 資料夾中)。

系統管理員必須設定檔案共用的權限，讓 RTC 群組擁有所需的讀取及寫入存取權。

<table>
<thead>
<tr class="header">
<th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果發生任何與權限相關的錯誤，請開啟拓撲產生器，下載並重新發行現有的拓撲。發行拓撲可驗證檔案共用權限，並依需要重設。</td>
</tr>
</tbody>
</table>


您可以使用下列設定來管理儲存會議內容的方式：

  - **ContentGracePeriod** (位在＜[Set-CsConferencingConfiguration](set-csconferencingconfiguration.md)＞中) 可設定會議結束後，將 Web 會議內容保留在伺服器上的時間。

  - **MaxContentStorageMb** (位在＜[Set-CsConferencingConfiguration](set-csconferencingconfiguration.md)＞中) 可設定單一會議期間，可用來儲存內容的檔案空間量上限。

**MaxUploadFileSizeMb** 不會限制 Lync Web App 的檔案上傳設定。Lync Web App 的檔案大小上傳限制設為大約 30MB，並由 IIS web.config 檔案控制：/DataCollabWeb/Int\[Ext\]/Handler/web.config。若要設定 Lync Web App 的檔案大小上傳限制，請更新 web.config 檔案中的 `maxRequestLength` 及 `maxAllowedContentLength`，如下所示。

    <system.web>
        <!-- 
            Since this handler is used to upload files to DMCU the request size (in kilobytes) 
            has to fit max allowed file size uploaded by Lync Web App client.
            The timeout has to reflect the min client bandwidth. Timeout of 600 secs 
            and 512 Kbits of *client* bandwidth would result into aproximately 30 Mbytes 
            for Lync Web App upload size limit.
        -->
          <httpRuntime maxRequestLength="500000" executionTimeout="600" />
    
    
    
                    <security>
                    <requestFiltering>
                               <requestLimits maxAllowedContentLength="524288000" />
                    </requestFiltering>
                    </security>

您必須更新每個前端伺服器的 web.config 檔案。

## Office Web Apps Server

為了使用這些新功能，系統管理員必須安裝 Office Web Apps Server，而且必須設定 Lync Server 2013 來與 Office Web Apps Server 通訊。本文件提供如何設定 Lync Server 2013 來使用 Office Web Apps Server 的相關資訊。但本文件沒有提供如何安裝 Office Web Apps Server 的相關資訊。如需安裝的詳細資訊，請參閱 Microsoft Office Web Apps 部署網站，網址為 <http://go.microsoft.com/fwlink/?linkid=257525>。該指南包含 Office Web Apps Server 的完整先決條件資訊。請注意，Office Web Apps Server 應安裝在非執行 Lync Server、SQL Server 或任何其他伺服器應用程式的獨立電腦上 (該電腦上絕不能安裝任何版本的 Office)。用來執行 Office Web Apps Server 的任何電腦也必須安裝一組特定的軟體 (包括 .NET Framework 4.5 和 Windows PowerShell 3.0)。Microsoft Office Web Apps 部署網站中有這些需求以及設定憑證和 Internet Information Services (IIS) 相關資訊的詳細討論，網址為 <http://go.microsoft.com/fwlink/?linkid=257525>。

## 請參閱

#### 概念

[Lync Server 2013 中的 Web 會議概觀](lync-server-2013-web-conferencing-overview.md)  
[Web 會議的部署檢查表](lync-server-2013-deployment-checklist-for-web-conferencing.md)

