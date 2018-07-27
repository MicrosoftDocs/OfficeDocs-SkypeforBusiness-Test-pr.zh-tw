---
title: 設定監看員節點以使用信任的伺服器驗證
TOCTitle: 設定監看員節點以使用信任的伺服器驗證
ms:assetid: 42d879ac-aa90-4ed6-b5e2-1e208711672a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204852(v=OCS.15)
ms:contentKeyID: 49290742
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定監看員節點以使用信任的伺服器驗證

 

_**上次修改主題的時間：** 2012-10-22_

如果您的監看員節點電腦位於周邊網路內，使用受信任的伺服器驗證可大幅減少管理負擔，僅需維護單一憑證即可，不必再維護許多使用者帳戶密碼。

若要設定受信任的伺服器驗證，首先必須建立信任的應用程式集區，以便管理監看員節點電腦。建立信任的應用程式集區後，必須在該監看員節點上設定綜合交易，當作是信任的應用程式來執行。

> [!NOTE]  
> 信任的應用程式係指取得信任狀態、並依附在 Lync Server 2013 上執行的應用程式，但不屬於產品內建的一部分。信任狀態表示每次執行應用程式時，其驗證不會受到質疑。



若要建立信任的應用程式集區，請開啟 Lync Server 2013 管理命令介面並執行與下列類似的命令：

    New-CsTrustedApplicationPool -Identity atl-watcher-001.litwareinc.com -Registrar atl-cs-001.litwareinc.com -ThrottleAsServer $True -TreatAsAuthenticated $True -OutboundOnly $False -RequiresReplication $True -ComputerFqdn atl-watcher-001.litwareinc.com -Site Redmond

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如需以上命令使用的參數相關詳細資料，請在 Lync Server 管理命令介面提示中鍵入下列內容：<br />
Get-Help New-CsTrustedApplicationPool -Full | more</td>
</tr>
</tbody>
</table>


建立信任的應用程式集區後，請將監看員節點電腦設為以信任的應用程式執行綜合交易。若要設定，可使用 **New-CsTrustedApplication** Cmdlet 以及與下列類似的命令進行：

    New-CsTrustedApplication -ApplicationId STWatcherNode -TrustedApplicationPoolFqdn atl-watcher-001.litwareinc.com -Port 5061

完成以上命令並建立信任的應用程式後請執行 Enable-CsTopology，確保變更生效：

    Enable-CsTopology

執行 Enable-CsTopology 後，建議重新啟動電腦。

若要確認是否已建立全新信任的應用程式，請在 Lync Server 管理命令介面提示中鍵入下列內容：

    Get-CsTrustedApplication -Identity "atl-watcher-001.litwareinc.com/urn:application:STWatcherNode"

## 在監看員節點上設定預設憑證

每個監看員節點都必須擁有使用 Lync Server 部署精靈指派的預設憑證。

**指派預設憑證**

1.  依序按一下 **\[開始\]**、**\[所有程式\]**、**\[Lync Server\]** 及 **\[Lync Server 部署精靈\]**。

2.  在 Lync Server 部署精靈中，按一下 **\[安裝或更新 Lync Server 系統\]**，然後再按一下 **\[要求、安裝或指派憑證\]** 標題下方的 **\[執行\]**。
    
    > [!NOTE]  
    > 如果 <strong>[執行]</strong> 按鈕停用，需先按一下 <strong>[安裝本機組態存放區]</strong> 下方的 <strong>[執行]</strong>。
    


3.  執行下列其中一項作業：
    
      - 如果您擁有的憑證可作為預設憑證，請按一下驗證精靈中的 **\[預設\]**，然後再按一下 **\[指派\]**，並遵照驗證指派精靈中的步驟指派該憑證。
    
      - 如果想要求提供憑證作為預設憑證，請按一下 **\[要求\]** 並遵照憑證要求精靈中的步驟要求提供憑證。如果使用網頁伺服器憑證的預設值，則可獲得一個憑證並將其指派為預設憑證。

## 安裝與設定監看員節點

重新啟動監看員節點電腦並設定憑證後，必須執行 Watchernode.msi 這個檔案 (必須在裝有 Operations Manager 代理程式檔案和 Lync Server 2013 核心元件的電腦上執行 Watchernode.msi)。

**安裝與設定監看員節點**

1.  開啟 Lync Server 管理命令介面：依序按一下 **\[開始\]**、**\[所有程式\]**、**\[Lync Server\]** 及 **\[Lync Server 管理命令介面\]**。

2.  在 Lync Server 管理命令介面中鍵入下列命令，然後按下 ENTER 鍵 (指定 Watchernode.msi 副本的確切路徑)：
    
        C:\Tools\Watchernode.msi Authentication=TrustedServer
    
    > [!NOTE]  
    > 您可以從命令視窗執行 Watchernode.msi。若要開啟命令視窗，請按一下 <strong>[開始]</strong>、在 <strong>[命令提示字元]</strong> 上按滑鼠右鍵，然後按一下 <strong>[以系統管理員身分執行]</strong>。待命令視窗開啟後，鍵入以上同一個命令。
    


請注意，以上命令 Authentication=TrustedServer 的名稱/值對區分大小寫。必須確實鍵入顯示的內容。下列命令因未使用正確的大小寫字母而導致失敗：

C:\\Tools\\Watchernode.msi authentication=trustedserver

只有在周邊網路內的電腦上才能使用 TrustedServer 模式。在 TrustedServer 模式下執行監看員節點時，系統管理員便無須維護電腦的測試使用者密碼。

