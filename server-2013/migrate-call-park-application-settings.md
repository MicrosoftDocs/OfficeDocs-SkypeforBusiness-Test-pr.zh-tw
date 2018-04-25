---
title: 移轉通話駐留應用程式設定
TOCTitle: 移轉通話駐留應用程式設定
ms:assetid: 23b192d2-93ec-42a8-b175-b6ed502a2c35
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ687993(v=OCS.15)
ms:contentKeyID: 49889977
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 移轉通話駐留應用程式設定

 

_**上次修改主題的時間：** 2012-10-19_

將通話駐留應用程式從 Lync Server 2010 移轉至 Lync Server 2013 的作業包括：搭配任何已上傳至 Lync Server 2010 的自訂等候音樂檔案來佈建 Lync Server 2013 集區、還原服務層級設定並將所有通話駐留軌道重新鎖定至 Lync Server 2013 集區。若您已在 Lync Server 2010 集區中設定自訂的等候音樂檔案，就必須將這些檔案複製到新的 Lync Server 2013 集區。此外，建議您將任何通話駐留自訂等候音樂檔案從 Lync Server 2010 備份至其他目的地，以確保通話駐留用的任何已上傳自訂等候音樂檔案都有個別的備份複本。通話駐留應用程式的自訂等候音樂檔案會儲存在集區的檔案存放區中。若要將音訊檔從 Lync Server 2010 集區檔案存放區複製到 Lync Server 2013 檔案存放區，請使用 **Xcopy** 命令，搭配下列參數：

    Xcopy <Source: Lync Server 2010 Pool CPS File Store Path> <Destination: Lync Server 2013 Pool CPS File Store Path>

    Example usage:  Xcopy "<Lync Server 2010 File Store Path>\OcsFileStore\coX-ApplicationServer-X\AppServerFiles\CPS\"  "<Lync Server 2013 File Store Path>\OcsFileStore\coX-ApplicationServer-X\AppServerFiles\CPS\" 

將所有自訂音訊檔複製到 Lync Server 2013 檔案存放區之後，就必須設定 Lync Server 2013 集區的通話駐留應用程式設定，並將與 Lync Server 2010 集區相關聯的通話駐留軌道重新指派至 Lync Server 2013 集區。

通話駐留應用程式設定包括接聽逾時臨界值、啟用或停用等候音樂、通話接聽嘗試次數上限以及逾時要求。您必須使用 Lync Server 管理命令介面執行 **Set-CsCpsConfiguration** Cmdlet 以管理通話駐留應用程式設定，而無法使用 Lync Server 控制台來管理通話駐留應用程式設定。

**重新設定通話駐留應用程式設定**

1.  從 Lync Server 2013 前端伺服器開啟 Lync Server 管理命令介面。

2.  在命令列輸入下列命令：
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若您的 Lync Server 2013 通話駐留應用程式設定和舊版的 Lync Server 2010 設定相同，則可不用執行此步驟。若 Lync Server 2013 和 Lync Server 2010 環境的通話駐留應用程式設定不同，請使用下列的 Cmdlet 做為範本來更新這些變更。</td>
    </tr>
    </tbody>
    </table>
    
        Set-CsCpsConfiguration -Identity "<LS2013 Call Park Service ID>" -CallPickupTimeoutThreshold "<LS2010 CPS TimeSpan>" -EnableMusicOnHold "<LS2010 CPS value>" -MaxCallPickupAttempts "<LS2010 CPS pickup attempts>" -OnTimeoutURI "<LS2010 CPS timeout URI>"

若要將通話駐留軌道範圍從 Lync Server 2010 集區重新指派至 Lync Server 2013 集區，您必須使用 Lync Server 控制台或 Lync Server 管理命令介面。

**使用 Lync Server 控制台重新指派所有通話駐留軌道範圍**

1.  開啟 Lync Server 控制台。

2.  在左窗格中，選取 \[語音功能\] 。

3.  選取 \[通話駐留\] 索引標籤。

4.  針對每個指派給 Lync Server 2010集區的通話駐留軌道範圍，編輯 \[目的地伺服器的 FQDN\] 設定，並選取要處理通話駐留要求的 Lync Server 2013 集區。

5.  選取 \[認可\] 以儲存變更。

**使用 Lync Server 管理命令介面重新指派所有通話駐留軌道範圍**

1.  開啟 Lync Server 管理命令介面。

2.  在命令列輸入下列命令：
    
        Get-CsCallParkOrbit
    
    此 Cmdlet 會列出部署中的所有通話駐留軌道範圍。若通話駐留軌道範圍的 **CallParkServiceId** 和 **CallParkServerFqdn** 參數是設為 Lync Server 2010 集區，則這些通話駐留軌道範圍都必須重新指派。
    
    若要將 Lync Server 2010 通話駐留軌道範圍重新指派至 Lync Server 2013 集區，請在命令列輸入下列命令：
    
        Set-CsCallParkOrbit -Identity "<Call Park Orbit Identity>" -CallParkService "service:ApplicationServer:<Lync Server 2013 Pool FQDN>"

將通話駐留軌道範圍重新指派至 Lync Server 2013 集區之後，通話駐留應用程式的移轉程序隨即完成， Lync Server 2013 集區將會處理所有後續的通話駐留要求。

