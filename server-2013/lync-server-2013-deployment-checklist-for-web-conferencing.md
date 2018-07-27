---
title: Web 會議的部署檢查表
TOCTitle: Web 會議的部署檢查表
ms:assetid: 9908ebe0-e5d3-4920-b9b1-85021f7e69e9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205104(v=OCS.15)
ms:contentKeyID: 49291750
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Web 會議的部署檢查表

 

_**上次修改主題的時間：** 2015-03-09_

如同部署其他 Lync Server 2013 元件，部署 Web 會議需要使用拓撲產生器建立及發行包含會議功能的拓撲。

## 部署順序

您可以在部署初始拓撲時就部署會議功能，或是在部署至少一個前端集區或Standard Edition 伺服器後再部署會議功能。

## 會議功能部署程序

下表概述在現有拓撲中部署會議功能時所需的步驟。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>階段</th>
<th>步驟</th>
<th>角色與群組成員資格</th>
<th>文件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>安裝先決條件硬體與軟體</strong></p></td>
<td><p>會議會在前端集區中的前端伺服器上和 Standard Edition 伺服器上執行。除了必須安裝這些伺服器之外，並沒有其他的硬體或軟體需求。</p>
<div class="alert">
> [!NOTE]  
> Lync Server 2013 使用 Office Web Apps 和 Office Web Apps Server 處理 PowerPoint 簡報的共用和轉譯。如需關於安裝及設定 Office Web Apps Server 的詳細資訊，請參閱＜<a href="lync-server-2013-enabling-office-web-apps-server-and-lync-server-2013.md">設定 Office Web Apps Server 與 Lync Server 2013 的整合</a>＞。


</div></td>
<td><p>身為本機 Administrators 群組成員的網域使用者</p></td>
<td><p>支援文件中的<a href="lync-server-2013-supported-hardware.md">Lync Server 2013 的受支援硬體</a></p>
<p>支援文件中的<a href="lync-server-2013-server-software-and-infrastructure-support.md">Lync Server 2013 中的伺服器軟體和基礎結構支援</a></p>
<p>規劃文件中的<a href="lync-server-2013-determining-your-system-requirements.md">判定 Lync Server 2013 的系統需求</a>。</p>
<p>規劃文件中的<a href="lync-server-2013-technical-requirements-for-archiving.md">Lync Server 2013 中封存的技術需求</a>。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><strong>建立適當的內部拓撲以支援會議功能</strong></p></td>
<td><p>執行拓撲產生器將會議功能新增至拓撲，然後發行拓撲。</p></td>
<td><p>若要定義拓撲，則使用身為本機 Users 群組成員的帳戶</p>
<p>若要發行拓撲，則使用身為 Domain Admins 群組與 RTCUniversalServerAdmins 群組成員，且對於要用於 Lync Server 2013 檔案存放區的檔案共用具有完整控制權限 (讀取/寫入/修改) 的帳戶 (以便讓 拓撲產生器 設定必要的 DACL)</p></td>
<td><p>部署文件中的<a href="lync-server-2013-define-and-configure-a-topology-in-topology-builder.md">針對 Lync Server 2013 在拓撲建置器中定義和設定拓撲</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>設定會議原則與支援</strong></p></td>
<td><p>使用 Lync Server 2013 控制台或 Lync Server 管理命令介面設定會議設定。</p></td>
<td><p>RTCUniversalServerAdmins 群組 (僅限 Windows PowerShell) 或將使用者指派到 [] 或 CSAdministrator 角色</p></td>
<td><p>作業文件中的<a href="lync-server-2013-conferencing-policies.md">Lync Server 2013 中的會議原則</a>。</p></td>
</tr>
</tbody>
</table>


Lync Server 2013 現在包含 **MaxUploadFileSizeMb** 設定，該設定會限制會議期間可以上傳的檔案大小。此設定的預設值為 500 MB。您可以使用 **Set-CsConferencingConfiguration** Cmdlet 調整 **MaxUploadFileSizeMb**。

**MaxUploadFileSizeMb** 不會限制 Lync Web App 的檔案上傳設定。Lync Web App 的檔案大小上傳限制是設為大約 30MB，並且受 IIS web.config 檔：/DataCollabWeb/Int\[Ext\]/Handler/web.config 所控制。若要設定 Lync Web App 的檔案大小上傳限制，請更新 web.config 檔中的 `maxRequestLength` 和 `maxAllowedContentLength`，如下所示。

    <system.web>
        <!-- 
            Since this handler is used to upload files to DMCU the request size (in kilobytes) 
            has to fit max allowed file size uploaded by LWA client.
            The timeout has to reflect the min client bandwidth. Timeout of 600 secs 
            and 512 Kbits of *client* bandwidth would result into aproximately 30 Mbytes 
            for LWA upload size limit.
        -->
          <httpRuntime maxRequestLength="500000" executionTimeout="600" />
    
    
    
                    <security>
                    <requestFiltering>
                               <requestLimits maxAllowedContentLength="524288000" />
                    </requestFiltering>
                    </security>

您必須為每個前端伺服器更新 web.config 檔。

