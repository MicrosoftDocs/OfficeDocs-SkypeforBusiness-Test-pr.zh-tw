---
title: 設定 SCOM 監控
TOCTitle: 設定 SCOM 監控
ms:assetid: 4003d225-2a33-448c-abd9-571750661140
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688033(v=OCS.15)
ms:contentKeyID: 49890034
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定 SCOM 監控

 

_**上次修改主題的時間：** 2012-10-04_

移轉至 Microsoft Lync Server 2013 之後，必須完成幾項工作來設定 Lync Server 2013，才能與 System Center Operations Manager 共同運作。

  - 套用 Lync Server 2010 更新至選取來管理集中探索邏輯的伺服器。

  - 更新集中探索候選伺服器登錄機碼。

  - 設定主要的 System Center Operations Manager 管理伺服器以覆寫候選集中探索節點。

執行各項工作的指示提供於下。

**套用 Lync Server 2010 更新至選取來管理集中探索邏輯的伺服器。**

1.  選取安裝有 System Center Operations Manager 代理程式檔案，並設定為候選探索節點的伺服器。

2.  套用 Lync Server 2010 更新至此伺服器。請參閱＜ [套用 Lync Server 2010 更新](apply-lync-server-2010-updates.md)＞主題。

**更新集中探索候選伺服器登錄機碼。**

1.  在選取來管理集中探索邏輯的伺服器上，開啟 Windows PowerShell 命令視窗。

2.  在命令列輸入下列命令：
    
        New-Item -Path "HKLM:\Software\Microsoft\Real-Time Communications\Health"
    
        New-Item -Path "HKLM:\Software\Microsoft\Real-Time Communications\Health\CentralDiscoveryCandidate"
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>編輯登錄時，如果登錄機碼已經存在，可能會顯示命令失敗的錯誤。如果您遇到這個問題，可以安心忽略錯誤。</td>
    </tr>
    </tbody>
    </table>


**設定主要的 System Center Operations Manager 管理伺服器以覆寫候選集中探索監看員節點。**

1.  在已安裝 System Center Operations Manager 主控台的電腦上，展開 **\[管理組件物件\]**，然後選取 **\[物件探索\]**。

2.  按一下 **\[變更領域...\]**。

3.  從 **\[管理組件物件領域\]** 頁面，選取 **\[LS 探索候選\]**。

4.  將 **\[LS 探索候選有效值\]** 覆寫為先前程序中選取的候選伺服器名稱。

最後，為了完成變更，請重新啟動 System Center Operations Manager Root Management Server 上的健全狀況服務。

