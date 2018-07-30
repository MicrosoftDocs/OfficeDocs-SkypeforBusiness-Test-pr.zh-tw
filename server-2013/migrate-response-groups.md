---
title: 移轉回應群組
TOCTitle: 移轉回應群組
ms:assetid: 43741ae7-c871-4573-b660-f2f5febc0856
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204854(v=OCS.15)
ms:contentKeyID: 49290747
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移轉回應群組

 

_**上次修改主題的時間：** 2013-09-23_

當使用者移動到 Lync Server 2013 集區後，便可移轉回應群組。移轉回應群組包括複製代理人群組、佇列、工作流程、音訊檔案，並將舊版部署的 回應群組 連絡人物件移動到 Lync Server 2013 集區。移轉舊版回應群組後， Lync Server 2013 集區中的 回應群組應用程式會處理回應群組的呼叫，而不再由舊版集區處理。

> [!NOTE]  
> 雖然可以先移轉回應群組後再將所有使用者移動至 Lync Server 2013 集區，但仍建議先移動所有使用者。尤其是屬於回應群組代理人的使用者必須移動至 Lync Server 2013 集區後才能完整運用全新功能。


您移轉回應群組前，必須已部署 Lync Server 2013 集區，並且其中內含 回應群組應用程式。回應群組應用程式 預設在您部署企業語音時已安裝且啟動。您可以執行 **Get-CsService –ApplicationServer** Cmdlet，確保有安裝 回應群組應用程式。

> [!NOTE]  
> 移轉舊版回應群組前，可以先在 Lync Server 2013 集區建立新的 Lync Server 2013 回應群組。


若要從舊版集區將回應群組移轉至 Lync Server 2013，可以執行 **Move-CsRgsConfiguration** Cmdlet。

> [!IMPORTANT]  
> 回應群組移轉 Cmdlet 會移動整個集區的 回應群組設定。您無法選取要移轉的特定群組、佇列或工作流程。

在移轉回應群組之後，必須使用 Lync Server 控制台或 Lync Server 管理命令介面 Cmdlet 驗證所有代理人群組、佇列及工作流程都已順利移動。

移轉回應群組時，不會刪除 Lync Server 2010 回應群組。移轉後使用When you manage response groups after migration by using either Lync Server 控制台或 Lync Server 管理命令介面管理回應群組時，會看到 Lync Server 2010 回應群組和 Lync Server 2013 回應群組，但只應該將更新套用到 Lync Server 2013 回應群組。 Lync Server 2010 回應群組會保留，僅供復原之用。

> [!CAUTION]  
> 完成移轉並建立新的回應群組後，Lync Server 控制台和 Lync Server 管理命令介面命令將顯示每個回應群組的 Lync Server 2010 和 Lync Server 2013 版本。請勿使用 Lync Server 控制台 或 Lync Server 管理命令介面 來移除 Lync Server 2010 回應群組。如果您移除一個回應群組，在移轉期間建立的對應回應群組將停止運作。淘汰 Lync Server 2010 集區時將移除 Lync Server 2010 回應群組。


> [!IMPORTANT]  
> 建議集區解除委任之後，再移除先前部署的各項資料。此外，強烈建議移轉後立即匯出回應群組。若不慎移除 Lync Server 2010 回應群組，可利用此項備份還原回應群組，即可重新執行 Lync Server 2013 回應群組。


Lync Server 2013 配備一項全新 回應群組功能，稱為 **\[工作流程類型\]** 。 **\[工作流程類型\]** 可以是 **\[已管理\]** 或 **\[未管理\]** 。移轉後的所有回應群組 **\[工作流程類型\]** 都會設為 **\[未管理\]** ，並附有一份空白的管理員清單。

執行 **Move-CsRgsConfiguration** Cmdlet 時，代理人群組、佇列、工作流程及音訊檔案都會保留在舊版集區供復原作業使用。如果確實有必要復原舊版集區，必須執行 **Move-CsApplicationEndpoint** Cmdlet 才能將連絡人物件移動到舊版集區。

下列的移轉 回應群組設定程序，會假設您已具備舊版集區和 Lync Server 2013 集區的一對一關係。若在移轉和部署期間，您計劃要合併或分割集區，就需要規劃舊版集區與 Lync Server 2013 集區的對應關係。

## 移轉 回應群組設定

1.  使用 RTCUniversalServerAdmins 群組的成員帳戶，或具有等同於系統管理員權限的帳戶登入電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  執行：
    
        Move-CsRgsConfiguration -Source <source pool FQDN> -Destination <destination pool FQDN>
    
    例如：
    
        Move-CsRgsConfiguration -Source lync-old.contoso.net -Destination lync-new.contoso.net

4.  將回應群組和代理人移轉至 Lync Server 2013 集區後，代理人登入/登出所使用的 URL 為 Lync Server 2013 URL，可從 **\[工具\]** 功能表中取得。請提醒代理人將書籤等任何參照更新到新的 URL。

## 使用 Lync Server 控制台驗證回應群組移轉

1.  使用 RTCUniversalReadOnlyAdmins 群組的成員帳戶，或至少必須是 CsViewOnlyAdministrator 角色之成員的帳戶登入電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[回應群組\]** 。

4.  在 \[工作流程\] 索引標籤中，確認清單中包括 Lync Server 2010 環境中的所有工作流程。

5.  按一下 \[佇列\] 索引標籤，確認清單中包括 Lync Server 2010 環境中的所有佇列。

6.  按一下 **\[群組\]** 索引標籤，確認清單中包括 Lync Server 2010 環境中的所有代理人群組。

## 使用 Lync Server 管理命令介面 驗證回應群組移轉

1.  使用 RTCUniversalReadOnlyAdmins 群組的成員帳戶，或至少必須是 CsViewOnlyAdministrator 角色之成員的帳戶登入電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。
    
    如需下列 Cmdlet 的詳細資料，請執行：
    
        Get-Help <cmdlet name> -Detailed

3.  執行：
    
        Get-CsRgsAgentGroup

4.  確認清單中包括 Lync Server 2010 環境中的所有代理人群組。

5.  執行：
    
        Get-CsRgsQueue

6.  確認清單中包括 Lync Server 2010 環境中的所有佇列。

7.  執行：
    
        Get-CsRgsWorkflow

8.  確認清單中包括 Lync Server 2010 環境中的所有工作流程。

