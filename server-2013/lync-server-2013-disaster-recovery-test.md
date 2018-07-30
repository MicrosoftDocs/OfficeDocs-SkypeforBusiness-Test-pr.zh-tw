---
title: Lync Server 2013：災害復原測試
TOCTitle: 災害復原測試
ms:assetid: 04f5e747-d837-4350-9fc0-8605dbf025a7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn747887(v=OCS.15)
ms:contentKeyID: 62293606
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的災害復原測試

 

_**上次修改主題的時間：** 2015-01-26_

為 Lync Server 2013 集區伺服器執行系統復原以測試您記錄的災害復原程序。本測試將會模擬一台伺服器的完整硬體故障狀況，並將協助保證各項資源、計畫和資料都可復原。請嘗試每月變換測試重點，以便您組織每次都能測試不同伺服器的故障狀況或設備的其他部件。

請注意，組織執行災害復原測試的排程各不相同，切勿忽略或疏於進行災害復原測試。


將 Lync Server 2013 拓撲、原則和組態設定匯出至檔案。除此之外，在升級、發生硬體故障或某些其他問題而造成資料遺失之後，此檔案還可在用於將此資訊還原至中央管理存放區。

將 Lync Server 2013 拓撲、原則和組態設定匯入至中央管理存放區或本機電腦，如下列命令所示：

`Import-CsConfiguration -ByteInput <Byte[]> [-Force <SwitchParameter>] [-LocalStore <SwitchParameter>]`

`Import-CsConfiguration -FileName <String> [-Force <SwitchParameter>] [-LocalStore <SwitchParameter>]`

若要備份生產 Lync Server 2013 資料，請執行下列動作：

  - 使用標準 SQL Server 備份程序來備份 RTC 和 LCSLog 資料庫，以將該資料庫傾印至檔案或磁帶傾印裝置。

  - 使用協力廠商備份應用程式，將資料備份至檔案或磁帶。

  - 使用 Export-CsUserData cmdlet 來建立整個 RTC 資料庫的 XML 匯出。

  - 使用檔案系統備份或協力廠商來備份會議內容和規範記錄。

  - 使用 Export-CsConfiguration command-line 工具來備份 Lync Server 2013 設定。

容錯移轉程序的第一步驟包含將使用者從生產集區強制移至災害復原集區。

此一步驟將為強制移動，因為生產集區將無法接受使用者遷移。

除了在 RTC SQL 資料庫上更新記錄之外，該 Lync Server 2013 移動使用者程序也能有效變更使用者帳戶物件上的屬性。

這項資料可透過下列兩項程序還原：

  - 使用標準 SQL Server 還原程序或使用協力廠商備份/還原公用程式，可將 RTC 資料庫從生產 SQL Server 的原始備份傾印裝置中還原。

  - 使用從生產 SQL Server 匯出建立的 XML 檔案便可透過 DBIMPEXP.exe 公用程式還原使用者聯絡資料。

在還原這項資料之後，使用者便能有效連線至災害復原 Lync Server 2013 集區並如常運作。

若要讓使用者能連線至災害復原 Lync Server 2013 集區，必須要有 DNS 記錄變更。

生產 Lync Server 2013 集區將會由用戶端使用下列項目的自動組態和 DNS SRV 記錄來參考：

  - SRV: \_sip.\_tls.\<domain\> /CNAME: SIP.\<domain\>

  - CNAME: SIP.\<domain\> /cvc-pool-1.\<domain\>

若要輔助容錯移轉，必須更新這項 CNAME 記錄才能參考 DROCSPool FQDN：

  - CNAME: SIP.\<domain\> /DROCSPool.\<domain\>

  - Sip.\<domain\>

  - AV.\<domain\>

  - webconf.\<domain\>

  - OCSServices.\<domain\>

> [!IMPORTANT]  
> 如需詳細的系統管理和管理程序，請參閱 <a href="lync-server-2013-backing-up-and-restoring-lync-server.md">備份及還原 Lync Server 2013</a> (備份及還原 Lync Server 2013)。



## 請參閱

#### 概念

[在 Lync Server 2013 中規劃高可用性和災害復原](lync-server-2013-planning-for-high-availability-and-disaster-recovery.md)  
[Backup and High Availability Cmdlet](https://docs.microsoft.com/en-us/powershell/module/skype/?view=skype-ps)  

#### 其他資源

[Import-CsConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Import-CsConfiguration)  
[備份及還原 Lync Server 2013](lync-server-2013-backing-up-and-restoring-lync-server.md)  
[管理 Lync Server 2013 災害復原、高可用性及備份服務](lync-server-2013-managing-lync-server-disaster-recovery-high-availability-and-backup-service.md)

