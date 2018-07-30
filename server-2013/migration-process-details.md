---
title: 移轉程序 - 詳細資料
TOCTitle: 移轉程序 - 詳細資料
ms:assetid: ca7e352c-9bde-47d9-8273-5cf2fdfdfe7e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205264(v=OCS.15)
ms:contentKeyID: 49292321
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移轉程序 - 詳細資料

 

_**上次修改主題的時間：** 2012-10-19_

請使用下列先決條件和詳細步驟，將 Lync Server 2010 群組聊天或 Office Communications Server 2007 R2  群組聊天移轉至 Lync Server 2013常設聊天室伺服器。

## 移轉的先決條件

在將 Lync Server 2010 群組聊天或 Office Communications Server 2007 R2  群組聊天移轉至 Lync Server 2013常設聊天室伺服器 前，您務必要先滿足下列先決條件。

1.  部署至少一個 Lync Server 2013 集區。如果您有多個 Lync Server 2013 集區，請決定哪個 Lync Server 2013 集區將為新 Lync Server 2013  Persistent Chat Server 集區的主集區。

2.  安裝 Lync Server 2013Persistent Chat Server 集區。它會是空的 (沒有類別、聊天室或增益集)。在您移轉舊版類別、聊天室或增益集之前，可以在 Lync Server 2013常設聊天室伺服器 部署中建立聊天室、類別或增益集。
    
    > [!IMPORTANT]  
    > 請注意，這些新建立的項目可能會與您移轉的舊版項目衝突。請避免任何命名衝突，否則它們會在移轉舊版資料時遭到覆寫。
    


## 準備要移轉的來源資料

請執行下列步驟，適當地準備要移轉的來源資料。

1.  備份 Lync Server 2010 群組聊天或 Office Communications Server 2007 R2  群組聊天的來源資料庫。如需關於備份 SQL Server 的詳細資訊，請參閱＜備份概觀 (SQL Server)＞，網址為 [http://go.microsoft.com/fwlink/?linkid=254851\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=254851%26clcid=0x404)。
    
    > [!IMPORTANT]  
    > Active Directory 網域服務 應該相同。移轉的一項條件是，您不能移轉至位於不同部署 (更明確地說，就是位於不同 Active Directory 樹系) 的集區。
    


2.  檢查您的 Lync Server 2010 群組聊天 或 Office Communications Server 2007 R2  群組聊天聊天室和類別組態。對您現有舊版部署中之類別、聊天室或增益集進行的任何變更，將是以 群組聊天管理工具執行。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>對您 Lync Server 2013常設聊天室伺服器 部署中之類別、聊天室或增益集所做的任何變更，是以 Lync Server 控制台 或 Windows PowerShell Cmdlet 執行。</td>
    </tr>
    </tbody>
    </table>
    
    請遵循這些步驟，準備要移轉的舊版系統。
    
    1.  常設聊天室伺服器 可支援單一層級的類別，不像一組階級很深的類別。移轉之後，子類別前面會加上完整的父類別名稱。建議您簡化並拉平現有的類別結構，讓產生的結構符合您的需求。
    
    2.  在根類別確認 **管理員**。如果在這個層級有任何管理員存在，這些使用者將會在移轉之後新增為 **所有聊天室的管理員**。如果貴組織並不需要此做法，您需要從根類別移除這些管理員。
    
    3.  確認聊天室名稱的長度。移轉之後，由於類別結構已簡化，聊天室如果存在於子類別底下，前面就會加上完整的父類別名稱。命名限制是 256 個字元 (包含父類別名稱)。您必須確認聊天室名稱的長度，甚至在名稱太長時縮短長度。
    
    4.  在 Lync Server 2013 中，如果類別 \[邀請\] 設定設為 true，您可以為該類別底下的聊天室邀請選擇 true 或 false。不過，如果類別 \[邀請\] 設定設為 false，該類別底下的聊天室的邀請會關閉。如果您要聊天室存在於特定類別底下，則在移轉之前，必須先在舊版 Lync Server  群組聊天伺服器中重設邀請設定。否則在移轉期間， Lync Server 2013 會顯示警告並將聊天室設為預設值 false。
    
    5.  如果您在聊天室中使用了檔案，必須在移轉之後手動將檔案 XCOPY 到新的 常設聊天室檔案存放區。工具並不會執行此動作。
    
    6.  如果您具有同盟使用者以及含同盟使用者的聊天室，請注意 常設聊天室伺服器 並不支援同盟。含同盟使用者的聊天室將會被移轉；不過，使用者本身將無法存取內容，因為系統並不支援同盟存取。
    
    7.  找出您不想要移轉的聊天室，將它們標成停用。
    
    8.  指出您想要移轉哪個日期以後的聊天室內容。例如，您可能不想移轉 2010 年 1 月 1 日以前的訊息，因為那些訊息太舊，或沒有進行移轉的必要。

## 執行移轉

請執行下列步驟，移轉您的舊版 群組聊天伺服器。

1.  關閉 Lync Server 2010 群組聊天、 Office Communications Server 2007 R2  群組聊天或 Lync Server 2013常設聊天室伺服器 服務。所有服務都必須停止，因此因此請規劃在有足夠停機時間的時候執行此動作。如前所述，請務必備份目前的 群組聊天資料庫。

2.  以 常設聊天室 系統管理員 RBAC 角色 (CsPersistentChatAdministrator) 的成員身分執行 Windows PowerShell**Export-CsPersistentChatData** Cmdlet。如需關於匯出/匯入 Cmdlet 的詳細資訊，請參閱 [在 Lync Server 2013 中使用 Windows PowerShell Cmdlet 疑難排解常設聊天室伺服器設定](lync-server-2013-troubleshooting-persistent-chat-server-configuration-using-windows-powershell-cmdlets.md)。
    
    檢查匯出的內容。

3.  在準備好進行匯入之前，請先關閉 Lync Server 2013常設聊天室伺服器 服務。所有服務都需要停止，因此請規劃在有足夠停機時間的時候執行此動作。

4.  如果您在移轉之前已於 Lync Server 2013 部署中建立任何類別、聊天室或增益集，請將 常設聊天室資料庫備份。匯出/匯入程序將能夠把舊版資料合併到 Lync Server 2013 部署中，但仍建議您備份資料庫，以防萬一不小心覆寫到內容 (例如，命名衝突仍然存在)。

5.  執行 Windows PowerShell**Import-CsPersistentChatData** Cmdlet (匯入工具)，並以 **WhatIf** 命令將移轉的資料填入 Persistent Chat Server 集區的 後端伺服器。在程序中會發生一些轉換，以配合簡化的系統管理模型。請修正出現的任何錯誤或警告。

6.  以 常設聊天室系統管理員 RBAC 角色 (CsPersistentChatAdministrator) 的成員身分執行 常設聊天室伺服器Windows PowerShell**Import-CsPersistentChatData** Cmdlet。如需關於匯出/匯入 Cmdlet 的詳細資訊，請參閱 [在 Lync Server 2013 中使用 Windows PowerShell Cmdlet 疑難排解常設聊天室伺服器設定](lync-server-2013-troubleshooting-persistent-chat-server-configuration-using-windows-powershell-cmdlets.md)。

7.  您必須將所有上傳的檔案 (整個資料夾) XCOPY 到新的 Lync Server 2013常設聊天室檔案存放區。
    
    > [!IMPORTANT]  
    > Lync 2013 (用戶端) 不支援在聊天室裡上傳或檢視檔案。您仍然可以使用舊版用戶端在聊天室裡張貼及檢視檔案。
    


8.  將 Lync Server 2010 群組聊天或 Office Communications Server 2007 R2  群組聊天查閱伺服器 URI 移植到 Lync Server 2013常設聊天室伺服器 連絡人物件。如果您的 Lync 2010 群組聊天或 Office Communicator 2007 R2  群組聊天 用戶端需要在移轉之後連線到最新的 Lync 2013常設聊天室 (用戶端)，而不進行任何用戶端組態變更，則需要執行下列步驟：
    
      - 刪除 ocschat@*\<domainName\>*.com 查詢伺服器使用者帳戶。這原本用來指向Lync Server 2010 群組聊天中的查閱服務。您可以稍後解除安裝集區並移除信任的項目。
    
      - 執行 **New-CsPersistentChatEndpoint** 這個 Windows PowerShell Cmdlet 並搭配相同的 SIP URI，建立舊版端點 ( 常設聊天室伺服器 連絡人物件)，以便在服務重新啟動時舊版用戶端可以有效地運作。
    
    目前已完成必要的移轉程序。 Lync 2010 群組聊天 (用戶端) 或 Office Communicator 2007 R2群組聊天 (用戶端) 現在可以在使用者察覺不到的情況下連線到新的 Persistent Chat Server 集區。
    
    請針對 Lync Server 2010 群組聊天 或 Office Communications Server 2007 R2群組聊天遵循這些額外的解除委任步驟。

9.  開啟新 Persistent Chat Server 集區中的所有電腦，以啟動 常設聊天室伺服器 服務。

10. 使用 Lync Server 控制台和 Windows PowerShell Cmdlet，確認資料已順利移轉。

11. 從 群組聊天伺服器集區中的電腦解除安裝 Lync 2010 群組聊天或 Office Communicator 2007 R2群組聊天。

12. 使用 Windows PowerShell Cmdlet 刪除信任的應用程式和信任的應用程式集區。如此會從 中央管理存放區刪除這些項目，並從 Active Directory 刪除相關的受信任服務項目 (TSE)。或者，也可以使用 拓撲產生器 (信任的應用程式/集區在該處也有專屬的節點) 完成此步驟。

13. 您現在可以開始透過新用戶端啟用 常設聊天室伺服器 功能。如需關於啟用 常設聊天室伺服器 的詳細資訊，請參閱 [在 Lync Server 2013 中部署常設聊天室伺服器](lync-server-2013-deploying-persistent-chat-server.md)。
    
    > [!IMPORTANT]  
    > Lync Server 2013 可支援多個 Persistent Chat Server 集區。不過，我們支援移轉 Lync 2010 群組聊天或 Office Communications Server 2007 R2  群組聊天集區到單一 Lync Server 2013Persistent Chat Server 集區。您可以在部署中加入其他新的 Persistent Chat Server 集區，以滿足法規需要 (例如，將資料保存在特定地區內)。
    

