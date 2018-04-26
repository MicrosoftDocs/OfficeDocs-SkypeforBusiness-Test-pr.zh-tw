---
title: 移轉回應群組
TOCTitle: 移轉回應群組
ms:assetid: 5c07bf4b-ad8a-4b83-b970-7d933bb7c4ef
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204931(v=OCS.15)
ms:contentKeyID: 49291036
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移轉回應群組

 

_**上次修改主題的時間：** 2012-10-19_

在將使用者移到 Lync Server 2013 集區之後，就可以移轉回應群組。移轉回應群組的程序包括複製代理程式群組、佇列、工作流程與音訊檔案，然後將 回應群組連絡人物件從舊版部署移到 Lync Server 2013 集區。在移轉舊版回應群組之後，對回應群組的通話會由 Lync Server 2013 集區中的 回應群組應用程式來處理。舊版集區不會再處理對回應群組的通話。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>雖然可以先移轉回應群組後再將所有使用者移動至 Lync Server 2013 集區，但仍建議先移動所有使用者。尤其是屬於回應群組代理人的使用者必須移動至 Lync Server 2013 集區後才能完整運用全新功能。</td>
</tr>
</tbody>
</table>


您移轉回應群組前，必須已部署 Lync Server 2013 集區，並且其中內含 回應群組應用程式。回應群組應用程式 預設在您部署企業語音時已安裝且啟動。您可以執行 **Get-CsService–ApplicationServer** Cmdlet，確保有安裝 回應群組應用程式。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>移轉舊版回應群組前，可以先在 Lync Server 2013 集區建立新的 Lync Server 2013 回應群組。</td>
</tr>
</tbody>
</table>


如要將回應群組從舊版集區移轉至 Lync Server 2013，請執行 **Move-CsRgsConfiguration** Cmdlet。在執行 **Move-CsRgsConfiguration** 之前，必須先安裝 Windows Management Instrumentation (WMI) 回溯相容性介面套件。執行 OCSWMIBC.msi 即可安裝此應用程式。您可在安裝媒體的安裝資料夾中找到 OCSWMIBC.msi。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>回應群組移轉 Cmdlet 會移動整個集區的 回應群組設定。您無法選取要移轉的特定群組、佇列或工作流程。</td>
</tr>
</tbody>
</table>


在移轉回應群組之後，需要更新正式代理程式登入登出回應群組所用的 URL，並使用 Lync Server 控制台或 Lync Server 管理命令介面 Cmdlet 來驗證已成功移動所有代理程式群組、佇列及工作流程。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ205186.Caution(OCS.15).gif" title="Caution" alt="Caution" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>移轉回應群組時，不會移除 Office Communications Server 2007 R2 回應群組。請勿移除 Office Communications Server 2007 R2 回應群組。如果移除 Office Communications Server 2007 R2 回應群組， Lync Server 2013 中的回應群組會停止運作。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>建議您在解除委任集區之後，才從先前的部署中移除任何資料。此外，強烈建議您在移轉之後，立即匯出回應群組。萬一 Office Communications Server 2007 R2 回應群組遭到移除，就可以從備份還原回應群組，讓 Lync Server 2013 回應群組再次運作。</td>
</tr>
</tbody>
</table>


執行 **Move-CsRgsConfiguration** Cmdlet 時，代理人群組、佇列、工作流程及音訊檔案都會保留在舊版集區供復原作業使用。如果確實有必要復原舊版集區，必須執行 **Move-CsApplicationEndpoint** Cmdlet 才能將連絡人物件移動到舊版集區。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>建議您在解除委任集區之後，才從舊版集區刪除任何回應群組資料。</td>
</tr>
</tbody>
</table>


下列移轉 回應群組設定的程序假設舊版集區和 Lync Server 2013 集區之間有著一對一的關係。如果計劃在移轉和部署期間合併或分割集區，則需要規劃舊版集區與 Lync Server 2013 集區的對應關係。

## 移轉 回應群組設定

1.  在安裝媒體的安裝資料夾中找到 OCSWMIBC.msi，然後執行安裝。

2.  使用 RTCUniversalServerAdmins 群組的成員帳戶，或具有等同於系統管理員權限的帳戶登入電腦。

3.  開啟 Lync Server 管理命令介面。

4.  在命令列輸入下列命令：
    
        Move-CsRgsConfiguration -Source <source pool FQDN> -Destination <destination pool FQDN>
    
    例如：
    
        Move-CsRgsConfiguration -Source pool01.contoso.net -Destination pool02.contoso.net

5.  如已在 Office Communications Server 2007 R2 環境中部署 Microsoft Office Communicator 2007 R2 的 \[回應群組\] 索引標籤，請從 Office Communicator 2007 R2 tabs.xml 檔案中移除該索引標籤。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>正式代理程式會先使用 [回應群組] 索引標籤來登入回應群組，之後才能接收通話。如果已部署 [回應群組] 索引標籤，則在部署時已選擇 Office Communicator 2007 R2 tabs.xml 檔案的位置。</td>
    </tr>
    </tbody>
    </table>


6.  提供使用者更新過的 URL，以讓代理程式用來登入與登出回應群組。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>此 URL 通常是 https://webpoolFQDN/RgsClients/Tab.aspx，其中 <em>webpoolFQDN</em> 是與剛移轉至 Lync Server 2013 之集區相關聯的 Web 集區完整網域名稱 (FQDN)。</td>
    </tr>
    </tbody>
    </table>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若使用者已升級至 Lync 2013 就不需要此步驟，因為您可從 Lync 中的 <strong>[工具]</strong> 功能表中取得 URL。</td>
    </tr>
    </tbody>
    </table>


## 使用 Lync Server 控制台驗證回應群組移轉

1.  開啟 Lync Server 控制台。

2.  在左導覽列中，按一下 **\[回應群組\]** 。

3.  在 **\[工作流程\]** 索引標籤中，確認清單中包括 Office Communications Server 2007 R2 環境中的所有工作流程。

4.  按一下 **\[佇列\]** 索引標籤，確認清單中包括 Office Communications Server 2007 R2 環境中的所有佇列。

5.  按一下 \[群組\] 索引標籤，確認清單中包括 Office Communications Server 2007 R2 環境中的所有代理人群組。

## 使用 Cmdlet 驗證回應群組移轉

1.  開啟 Lync Server 管理命令介面。
    
    如需下列 Cmdlet 的詳細資料，請執行：
    
        Get-Help <cmdlet name> -Detailed

2.  在命令列輸入下列命令：
    
        Get-CsRgsAgentGroup

3.  確認清單中包括 Office Communications Server 2007 R2 環境中的所有代理人群組。

4.  在命令列輸入下列命令：
    
        Get-CsRgsQueue

5.  確認清單中包括 Office Communications Server 2007 R2 環境中的所有佇列。

6.  在命令列輸入下列命令：
    
        Get-CsRgsWorkflow

7.  確認清單中包括 Office Communications Server 2007 R2 環境中的所有工作流程。

