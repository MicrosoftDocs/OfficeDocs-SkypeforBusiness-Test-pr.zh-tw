---
title: 備份和還原需求：資料
TOCTitle: 備份和還原需求：資料
ms:assetid: ecfb8e4d-cb4f-476d-9772-4486bd683c04
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh202194(v=OCS.15)
ms:contentKeyID: 52056252
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 備份和還原需求：資料

 

_**上次修改主題的時間：** 2013-03-26_

Lync Server 使用儲存於資料庫中的設定及組態資訊，以及儲存於資料庫與檔案存放區中的資料。本主題說明需要備份以於組織遭遇失敗或運作中斷時還原服務的資料，同時也指出需要個別備份之 Lync Server 所使用的資料與元件。

## 設定及組態需求

本主題包含備份及還原設定與組態資訊 (復原 Lync Server 服務時所需) 的程序。設定資訊位於中央管理存放區中，或位於其他後端資料庫或 Standard Edition 伺服器上。

下表列出備份與還原時所需的設定與組態資訊。

### 設定及組態資料

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>資料類型</th>
<th>存放位置</th>
<th>描述/備份時機</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>拓撲設定資訊</p></td>
<td><p>中央管理存放區 (資料庫：Xds.mdf)</p></td>
<td><p>拓撲、原則及組態設定。</p>
<p>使用 Lync Server 控制台或 Cmdlet 修改設定或原則之後，以定期備份方式進行備份。</p></td>
</tr>
<tr class="even">
<td><p>位置資訊</p></td>
<td><p>中央管理存放區 (資料庫：Lis.mdf)</p></td>
<td><p>加強版企業語音 9-1-1 (E9-1-1) 設定資訊。本資訊定期不會更動。</p>
<p>備份定期備份。</p></td>
</tr>
<tr class="odd">
<td><p>回應群組設定資訊</p></td>
<td><p>後端伺服器或 Standard Edition 伺服器 (資料庫：RgsConfig.mdf)</p></td>
<td><p>回應群組代理人群組、佇列和工作流程。</p>
<p>新增或變更代理人群組、佇列或工作流程之後，以定期備份方式進行備份。</p></td>
</tr>
</tbody>
</table>


## 資料需求

以下是您需要進行備份以便在失敗時還原 Lync Server 的 Lync Server 資料清單。

請注意，部分類型的資料不需要復原。本主題不包含備份下列資料類型的程序：

  - 暫時性的使用者資料，如端點與訂閱、作用中的會議伺服器，以及暫時性的會議狀態 (資料庫：RtcDyn.mdf)

  - 通訊錄資料 (資料庫：Rtcab.mdf 與 Rtcab1.mdf)。通訊錄資料庫會從 Active Directory 網域服務 自動重新產生。

  - 通話駐留應用程式的動態資料 (資料庫：CpsDyn.mdf)

  - 暫時性的回應群組資料，如代理人登入狀態以及插撥資訊 (資料庫：RgsDyn.mdf)

  - 常設聊天室 (資料庫：MgcComp.mdf) 的規範資料庫。如果您啟用常設聊天室規範，只要將配接器設定為從資料庫讀取資訊並加以轉換成替代格式，則常設聊天室規範資料庫中的資訊是暫時性的。因此，常設聊天室規範資料庫被視為是暫時性的。
    
    Lync Server 2013 常設聊天室伺服器 隨附 XML 配接器。您也可以安裝自訂配接器，將此資料移至其他來源，例如 Exchange 裝載的封存。

下表列出備份與還原所需的資料。

### 儲存在資料庫中的資料

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>資料類型</th>
<th>存放位置</th>
<th>描述/備份時機</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>持續的使用者資料</p></td>
<td><p>後端伺服器或 Standard Edition 伺服器 (資料庫：RTCXDS.mdf)</p></td>
<td><p>使用者權限、使用者連絡人清單、伺服器或集區資料、排定的會議等等。此使用者資料不包括上傳至會議的內容。</p>
<p>備份定期備份。此資訊為動態資訊，但如果您需要還原至前次定期備份，那麼沒有進行更新對於 Lync Server 來說並不是件嚴重的事。如果連絡人清單對於組織而言相當重要，您可以更頻繁地備份此資料。</p></td>
</tr>
<tr class="even">
<td><p>封存資料</p></td>
<td><p>封存資料庫 (資料庫：LcsLog.mdf)</p>
<p>如果您啟用 Microsoft Exchange 整合選項，此資料可儲存於 Exchange 2013 上。否則，此資料會保留在與其他 Lync Server 資料庫組合在一起的 Lync Server 封存資料庫中，或是獨立於個別資料庫伺服器上。</p></td>
<td><p>立即訊息 (IM) 與會議內容。</p>
<p>此資料對 Lync Server 並不重要，但對於組織控管而言卻相當重要。請據此決定備份排程。</p>
<p>Lync Server 僅支援封存資料庫的「簡單復原」模式。透過簡單復原模式，可將資料庫復原至上次的完整備份點，表示您無法將資料庫還原至失敗點或特定時間點。</p></td>
</tr>
<tr class="odd">
<td><p>監控資料</p></td>
<td><p>監控資料庫 (LcsCDR.mdf and QoeMetrics.mdf)</p>
<p>這些資料庫可與其他 Lync Server 資料庫組合在一起，或是獨立於個別資料庫伺服器上。</p></td>
<td><p>通話詳細記錄 (LcsCDR.mdf) 及經驗品質 (QoE) 評量 (QoeMetrics.mdf)。</p>
<p>通話詳細記錄是動態記錄，而且對於業務而言可能很重要。請考量您是否需要這些記錄進行控管，並據此決定備份排程。</p>
<p>經驗品質資訊是動態資訊。遺失 QoE 資訊對於 Lync Server 運作並不重要，但對於業務而言可能很重要。請依據此資訊對於組織的重要性決定備份排程。</p>
<p>Lync Server 僅支援監控資料庫的簡單復原模式。透過簡單復原模式，可將資料庫復原至上次的完整備份點，表示您無法將資料庫還原至失敗點或特定時間點。</p></td>
</tr>
<tr class="even">
<td><p>常設聊天室資料</p></td>
<td><p>常設聊天室資料庫 (mgd.mdf)。</p>
<p>此資料庫可與其他 Lync Server 資料庫組合在一起，或獨立於個別資料庫伺服器上。</p></td>
<td><p>常設聊天室資料是發佈在聊天室的實際內容。此資料通常是重要商業資料。</p>
<p>您可以選擇使用 SQL Server 備份，或使用 Lync Server 所提供的 <strong>Export-CsPersistentChatData</strong> Cmdlet 匯出資料庫。若要復原資料，您可以匯入並將資料庫還原至上一次完整備份點，這表示您無法將資料庫還原至失敗點。</p></td>
</tr>
</tbody>
</table>


## 檔案存放區資料需求

在 Enterprise Edition 部署中，Lync Server 檔案存放區一般位於檔案伺服器上；在 Standard Edition 部署中，Lync Server 檔案存放區預設位於 Standard Edition 伺服器 上。一般來說，會有一個 Lync Server 檔案存放區會供網站共用。常設聊天室檔案存放區會使用與 Lync Server 檔案存放區相同的檔案共用。

檔案存放區位置以 \\\\server\\share 名稱的形式表示。若要尋找您檔案存放區的特定位置，請開啟拓撲產生器並查看 \[檔案存放區\] 節點。

下表列出備份與還原所需的檔案存放區。

### 檔案存放區

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>資料類型</th>
<th>存放位置</th>
<th>描述 / 備份時間</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Lync Server 檔案存放區</p></td>
<td><p>一般位於檔案伺服器、檔案叢集或 Standard Edition 伺服器 上。</p></td>
<td><p>會議內容、會議內容中繼資料、會議規範記錄、應用程式資料檔、裝置更新的更新檔、回應群組、通話駐留以及宣告應用程式的音訊檔，以及發佈至常設聊天室的檔案。</p>
<p>備份定期備份。</p></td>
</tr>
</tbody>
</table>


## 其他份備需求

為了確保您在失敗時還原 Lync Server 服務的能力，您必須備份一些所需的元件 (不屬於 Lync Server 本身)。本文件中所述之 Lync Server 備份或還原處理程序，並不會備份下列元件：

  - **Active Directory 網域服務**   在備份 Lync Server 的同時，您需要使用 Active Directory 工具備份 AD DS。將 AD DS 與 Lync Server 保持同步處理，以及在 Lync Server 預期不符合 AD DS 中的連絡人物件時，避免發生問題是極為重要的。AD DS 可儲存下列 Lync Server 所使用的設定：
    
      - 使用者 SIP URI 及其他使用者設定。
    
      - 回應群組與會議服務員等應用程式的連絡人物件。
    
      - 指向中央管理存放區的指標。
    
      - Kerberos 驗證帳戶 (選用的電腦物件) 以及 Lync Server 安全性群組。
    
    如需在 Windows Server 2008 中備份及還原 AD DS 的詳細資訊，請參閱＜AD DS 備份及復原逐步指南＞，網址為 <http://go.microsoft.com/fwlink/?linkid=209105>。

  - **憑證授權單位與憑證**   請使用組織的原則備份憑證授權單位 (CA) 與憑證。若您使用可匯出的私密金鑰，可以備份憑證與私密金鑰，然後在使用本文件中的程序還原 Lync Server 時將其匯出。若您使用內部 CA，在需要還原 Lync Server 時，可以重新註冊。將私密金鑰保留在安全之處以便在電腦發生問題時加以使用很重要。

  - **System Center Operations Manager**   若您使用 Microsoft System Center Operations Manager (舊名為 Microsoft Operations Manager) 監控您的 Lync Server 部署，可以選擇性地備份其在監控 Lync Server 時所建立的資料。使用標準 SQL Server 備份處理程序備份 System Center Operations Manager 檔案。這些檔案在復原期間不會加以還原。

  - **公用交換電話網路 (PSTN) 閘道設定**   若您使用企業語音或 Survivable Branch Appliance，您需要備份 PSTN 閘道設定。請與廠商連絡以取得備份及還原 PSTN 閘道設定的詳細資訊。

  - **Lync Server 或 Office Communications Server 的共存版本**   若您的 Lync Server 2013 部署與 Lync Server 2010 或舊版 Office Communications Server 共存，您將無法使用文件中的程序來備份或還原舊版。而是必須使用專供舊版所用的備份與還原程序。如需備份與還原 Lync Server 2010 的詳細資訊，請參閱 <http://go.microsoft.com/fwlink/?linkid=265417>；如需備份與還原 Microsoft Office Communications Server 2007 R2 的詳細資訊，請參閱 <http://go.microsoft.com/fwlink/?linkid=168162>。

  - **基礎結構資訊**   您必須備份有關基礎結構的資訊，如防火牆設定、負載平衡設定、網際網路資訊服務 (IIS) 設定、網域名稱系統 (DNS) 記錄與 IP 位址，以及動態主機設定通訊協定 (DHCP) 設定。如需備份這些元件的詳細資訊，請連絡各元件的廠商。

  - **Microsoft Exchange 及 Exchange 整合通訊 (UM)**   備份和還原 Microsoft Exchange 及 Exchange UM (如 Microsoft Exchange 文件中所述)。如需備份及還原 Exchange Server 2013 的詳細資訊，請參閱 <http://go.microsoft.com/fwlink/?linkid=285384>；如需備份及還原 Exchange Server 2010 的詳細資訊，請參閱 <http://go.microsoft.com/fwlink/?linkid=209179>。
    
    請注意，Lync Server 2013 引進聯絡人清單、高畫質使用者相片，以及在 Exchange 2013 儲存封存資料的功能。請參閱下列清單，了解如何備份這些資料類型：
    
      - **高畫質相片**會備份為 Exchange Server 備份的一部分。
    
      - **整合連絡人存放區**是 Lync Server 2013 所導入的功能。整合連絡人存放區可讓使用者將其所有連絡人資訊保存在 Exchange 2013 中。
        
        您應該確定備份對使用者而言是最新狀態，無論其使用者連絡人是儲存於整合連絡人存放區還是 Lync 後端伺服器中。下列案例說明在何處將使用者連絡人移轉至整合連絡人存放區會導致備份及還原程序發生問題。
        
        **案例 1：**將使用者連絡人移轉至整合連絡人存放區，在移轉使用者連絡人之前從 Lync Server 備份執行復原。在此案例中，使用者將有「逾期」狀態的連絡人 (最多一天)，直到 Lync Server Migration Task 開始將使用者連絡人移轉至 Exchange。(請注意，由於先前已將使用者連絡人移轉至整合連絡人存放區，系統將會使用 Exchange 連絡人資訊)。在本案例中不需要系統管理員進行操作。
        
        **案例 2：**先前將使用者連絡人儲存在整合連絡人存放區，但後來又回復。當使用者儲存在整合連絡人存放區時從 Lync Server 備份執行還原。在此案例中，用戶端或 Lyss 伺服器記錄中的 `Error: Incorrect Exchange Version` 錯誤訊息表示發生問題。使用者將能夠直接從 Exchange 在 Lync 2013 中存取其連絡人清單，但是用戶端的狀態不會與 Lync Server 狀態相符。若要修正此問題，需要系統管理員為受影響的使用者執行 **Invoke-CsUCSRollback** Cmdlet。
    
      - **封存資料**可儲存在 Exchange 2013 中。此資料對 Lync Server 不重要，但是可能對您組織的管理相當重要。如果封存資料儲存在 Exchange 中，而且對您的組織相當重要，則請遵循 Exchange 備份及還原程序。請注意，將封存資料儲存在 Exchange 中無法移回至 Lync Server。此外，無法將已儲存在 Lync 封存資料庫的資料移至 Exchange。

