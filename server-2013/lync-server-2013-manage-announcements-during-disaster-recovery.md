---
title: Lync Server 2013：在災害復原期間管理宣告
TOCTitle: 在災害復原期間管理宣告
ms:assetid: c33e51ea-421f-42d2-826b-b73968f6bd5b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721874(v=OCS.15)
ms:contentKeyID: 49890295
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 使用 Lync Server 2013 在災害復原期間管理宣告

 

_**上次修改主題的時間：** 2013-02-23_

Lync Server 2013 可支援在系統中斷期間，對撥給未指派號碼的通話播放宣告。在系統中斷期間還原宣告功能是選用的。如果您選擇在系統中斷期間還原宣告，則需在備份集區中重新建立宣告設定。本節說明如果您選擇在災害復原期間還原宣告，需執行哪些步驟。

本節適用於使用 宣告應用程式的未指派號碼範圍。本節不適用使用 Exchange Unified Messaging (UM) 自動語音應答的未指派號碼範圍。

## 系統中斷前

無論您是否選擇在系統中斷期間使用宣告，都應對您為 宣告應用程式設定的所有自訂音訊檔分別進行備份。 Lync Server 災害復原程序並不會備份自訂宣告。如果您未對檔案進行個別備份，而上傳至伺服器或集區的檔案遭到破壞、損毀或清除，您就會遺失該檔案。

如果您沒有自訂音訊檔的備份複本，也找不到原始音訊檔了，可以查看當初匯入檔案之伺服器或集區的檔案存放區，應該可以找到您為 宣告應用程式設定的音訊檔。您可從檔案存放區複製您為 宣告應用程式設定的所有音訊檔。

**從檔案存放區複製音訊檔**

1.  在命令列中執行：
    
        Xcopy <Source: Pool Announcement Service File Store path> <Destination>
    
    例如：
    
        Xcopy "<Pool File Store Path>\X-ApplicationServer-X\AppServerFiles\RGS\AS" "<Destination: Backup location>"
    
    其中 X-ApplicationServer-X 代表集區應用程式伺服器的服務 ID (例如 1-ApplicationServer-1")


## 系統中斷期間

若要在系統中斷期間使用 宣告應用程式，您需要執行本節所述的工作，以在備份集區中重新建立宣告設定。

> [!NOTE]  
> 建議您在容錯移轉至備份集區後再執行這些工作，因為一旦執行步驟 2 後，備份集區就會獲得未指派號碼範圍的擁有權。



> [!NOTE]  
> 若是使用 Exchange UM 自動語音應答電話號碼的號碼範圍，則不必執行這些步驟。



**在備份集區重新建立宣告設定**

1.  執行下列步驟，以在備份集區中重新建立原本部署於主要集區中的宣告：
    
    1.  使用 **Import-CsAnnouncementFile** Cmdlet 並在 Parent 參數指定備份集區，以將主要集區使用的任何音訊檔匯入至備份集區。
    
    2.  使用 **New-CsAnnouncement** Cmdlet 並在 Parent 參數指定備份集區，以重新建立每個宣告。
    
    > [!NOTE]  
    > 如需關於使用這些參數在備份集區建立宣告的詳細資訊，請參閱 <a href="lync-server-2013-create-an-announcement.md">在 Lync Server 2013 中建立宣告</a>。
    


2.  在備份集區重新建立所有宣告後，將使用主要集區中之宣告的所有未指派號碼範圍，重新導向至備份集區中重新建立的宣告。
    
    針對使用主要集區中之宣告的每個未指派號碼範圍，執行下列命令：
    
        Set-CsUnassignedNumber -Identity "<name of number range>" -AnnouncementService "<FQDN of backup pool>" -AnnouncementName "<announcement name in backup pool>"

## 系統中斷後

主要集區恢復可用後，您需將因為系統中斷而做出變更的未指派號碼範圍重新導向回主要集區。

> [!NOTE]  
> 若是使用 Exchange UM 自動語音應答電話號碼的號碼範圍，則不必執行這些步驟。



**還原主要集區中的宣告**

1.  如果您已在復原期間重建主要集區，則需匯入音訊檔並建立宣告，以便在主要集區中重新建立宣告，此程序與對備份集區執行的程序相同，只是現在是在 Parent 參數指定主要集區。如需詳細資訊，請參閱本主題稍早的＜系統中斷期間＞。

2.  對於您因為系統中斷而做出變更的每個未指派號碼範圍，執行下列命令：
    
        Set-CsUnassignedNumber [-Identity "<name of number range>"] -AnnouncementService "<FQDN of primary pool>" -AnnouncementName "<announcement name in primary pool>"

3.  (選用) 移除備份集區中重新建立的宣告。取得備份集區 宣告應用程式使用的宣告清單，在命令列中執行：
    
        Get-CsAnnouncement -Identity "<Service:service ID>"
    
    例如：
    
        Get-CsAnnouncement -Identity "ApplicationServer:redmond.contoso.com
    
    在產生的清單中找出您要移除的宣告，並複製其 GUID。對於您要移除的每個宣告，執行：
    
        Remove-CsAnnouncement -Identity "<Service:service ID/guid>"
    
    例如：
    
        Remove-CsAnnouncement -Identity "ApplicationServer:redmond.contoso.com/1951f734-c80f-4fb2-965d-51807c792b90"


