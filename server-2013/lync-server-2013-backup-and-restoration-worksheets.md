---
title: 備份和還原工作表
TOCTitle: 備份和還原工作表
ms:assetid: 26c78155-0306-41ac-845b-7ad58000a1d6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh202169(v=OCS.15)
ms:contentKeyID: 52056074
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 備份和還原工作表

 

_**上次修改主題的時間：** 2015-03-09_

組織的備份和還原計劃應包含備份資料與設定的方式和時間等詳細資訊。您可以使用此處提供的工作表，協助您針對特定部署和組織的備份和還原需求，記載這些資訊。

請使用下列工作表來記錄備份和還原資料庫 (檔案存放區) 所需的資訊，以及 Lync Server 集區或 Standard Edition 伺服器的設定資訊。請將這些工作表的一或多份複本保存在安全的位置，以便當您需要還原 Lync Server 時可以隨時存取。

> [!NOTE]  
> 本節的工作表僅涵蓋還原 Lync Server 資料庫與伺服器之資料及設定所需的資訊。如果您需要記載其他還原資訊，例如重新安裝作業系統和其他軟體的相關資訊，請使用組織的部署計劃以及備份與還原計劃，以滿足這些需求。



## 資料庫備份及還原工作表

請使用下列表格來記錄備份及還原 Lync Server 資料庫所需的資訊。

### 用於備份及還原的資料庫資訊

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>資料庫</th>
<th>伺服器名稱 (FQDN)</th>
<th>備份排程</th>
<th>資料庫備份工具</th>
<th>備份組</th>
<th>備份目的地</th>
<th>附註</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>用於使用者資料之後端伺服器上的 RTC 資料庫</p></td>
<td><p>                    </p></td>
<td><p>                    </p></td>
<td><p><strong>Export-CsUserData</strong> Cmdlet</p></td>
<td><p>名稱：</p>
<p>到期日：</p>
<p>                   </p></td>
<td><p>                    </p></td>
<td><p>                    </p></td>
</tr>
<tr class="even">
<td><p>封存資料庫伺服器上的 LcsLog (預設名稱) 資料庫</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>SQL Server 管理工具</p></td>
<td><p>名稱：</p>
<p>到期日：</p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>用於詳細通話記錄 (CDR) 之監控資料庫伺服器上的 LcsCdr 資料庫</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>SQL Server 管理工具</p></td>
<td><p>名稱：</p>
<p>到期日：</p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>用於經驗品質 (QoE) 資料之監控資料庫伺服器上的 QoEMetrics 資料庫</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>SQL Server 管理工具</p></td>
<td><p>名稱：</p>
<p>到期日：</p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>常設聊天室資料庫</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>SQL Server 管理工具或 <strong>Export-CsPersistentChatData</strong> Cmdlet</p></td>
<td><p>名稱︰</p>
<p>到期日︰</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


下列資料庫不需要備份或還原：

  - Rtcdyn。在還原服務時，並不需要此資料庫中的暫時性使用者資料。

  - Rtcab。通訊錄資料庫會自動依據 Active Directory 網域服務中的全域通訊清單 (GAL) 來重新建立。

  - Rgsdyn。在還原服務時，並不需要此資料庫中的暫時性回應群組服務資料。

  - Cpsdyn。在還原服務時，並不需要通話駐留應用程式的動態資訊。

  - MgcComp。還原服務時，並不需要常設聊天室的規範資料庫。

## 檔案存放區備份及還原工作表

請使用下列表格來記錄備份及還原檔案存放區所需的資訊。檔案存放區中包含回應群組、通話駐留與宣告應用程式的會議內容中繼資料、會議規範記錄、裝置更新的更新記錄以及音訊檔等資料。

### 用於備份及還原的檔案存放區資訊

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>內容</th>
<th>伺服器名稱 (FQDN)</th>
<th>備份排程</th>
<th>檔案系統備份工具</th>
<th>要備份的檔案共用 *</th>
<th>備份目的地</th>
<th>附註</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Lync Server 檔案存放區</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>標準備份工具，如 Robocopy</p></td>
<td><p>若是 Enterprise Edition，則在檔案伺服器上。若是 Standard Edition 部署，則預設是在 Standard Edition 上。通常每個網站只會有一個。</p></td>
<td><p></p></td>
<td><p>名為 <strong>Meeting.Active</strong> 的檔案不應備份。這些檔案是在會議進行期間中使用並加以鎖定。</p></td>
</tr>
</tbody>
</table>


## 設定備份及還原工作表

請使用下列表格來記錄備份及還原設定所需的資訊。

### 用於備份及還原的設定資訊

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>資料庫</th>
<th>伺服器名稱 (FQDN)</th>
<th>備份排程</th>
<th>備份工具</th>
<th>組態檔 (.xml) 名稱</th>
<th>備份位置</th>
<th>附註</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>用於拓撲設定 (全域) 之中央管理存放區中的 Xds 資料庫</p></td>
<td><p>                    </p></td>
<td><p>                    </p></td>
<td><p><strong>Export-CsConfiguration</strong> Cmdlet</p></td>
<td><p>                   </p></td>
<td><p>                    </p></td>
<td><p>                   </p></td>
</tr>
<tr class="even">
<td><p>用於 E9-1-1 位置資訊 (全域) 之中央管理存放區 Lis 資料庫</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p><strong>Export-CsLisConfiguration</strong> Cmdlet</p></td>
<td><p></p></td>
<td><p> </p></td>
<td><p>                    </p></td>
</tr>
<tr class="odd">
<td><p>用於回應群組設定 (集區) 之後端伺服器上的 RgsConfig 資料庫</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p><strong>Export-CsRgsConfiguration</strong> Cmdlet</p></td>
<td><p></p></td>
<td><p> </p></td>
<td><p>                    </p></td>
</tr>
</tbody>
</table>

