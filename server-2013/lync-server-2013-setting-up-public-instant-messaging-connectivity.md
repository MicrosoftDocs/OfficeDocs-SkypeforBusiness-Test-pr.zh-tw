---
title: Lync Server 2013：設定 Public Instant Messaging Connectivity
TOCTitle: 設定 Public Instant Messaging Connectivity
ms:assetid: 816dea2a-96fa-4a36-b6c2-a9402675868b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205041(v=OCS.15)
ms:contentKeyID: 49291490
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定 Public Instant Messaging Connectivity

 

_**上次修改主題的時間：** 2012-09-08_

如果您的組織想要支援與 AOL 的公用立即訊息 (IM) 連線能力，您將無法使用 Lync Server 部署精靈要求憑證。請改為執行下列程序的步驟。

## 設定 Public Instant Messaging 連線

1.  在前端伺服器上，開啟 \[拓撲產生器\]。展開 Edge 集區，然後按一下您的 Edge Server 或 Edge Server 集區。選取 \[編輯內容\]。

2.  在 \[一般\] 下的 \[編輯內容\] 中，選取 \[啟用此 Edge 集區的同盟 (連接埠 5061)\]。按一下 \[確定\]。

3.  按一下 \[動作\]，然後依序選取 \[拓撲\] 和 \[發行\]。出現發行拓撲的提示時，按 \[下一步\]。完成發行時，按一下 \[完成\]。

4.  在 Edge Server 上，開啟 \[Lync Server 部署精靈\]。按一下 \[安裝或更新 Lync Server 系統\]，然後按一下 \[安裝或移除 Lync Server 元件\]。按一下 \[再執行一次\]。

5.  在 \[安裝 Lync Server 元件\] 上，按 \[下一步\]。摘要畫面將顯示它們執行的動作。部署完成之後，按一下 \[檢視記錄\] 以檢視可用的記錄檔。按一下 \[完成\] 以完成部署。

## 若要為 Edge Server 的外部介面建立憑證要求以支援對 AOL 的公用 IM 連線能力

1.  若有必要的範本可提供給 CA，請在 Edge Server 中使用下列 Windows PowerShell Cmdlet 以要求憑證：
    
        Request-CsCertificate -New -Type AccessEdgeExternal  -Output C:\ <certfilename.txt or certfilename.csr>  -ClientEku $true -Template <template name>
    
    用於 Lync Server 的預設範本憑證名稱為 Web Server。如果您需要使用不同於預設範本的其他範本，請僅指定「範本名稱」。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您的組織想要對 AOL 支援公用 IM 連線能力，您必須使用 Windows PowerShell (而非憑證精靈) 以要求要指定給 Access Edge Service 之外部邊緣的憑證。這是因為憑證精靈用來要求憑證的 Certificate Authority (CA) 伺服器範本不支援用戶端 EKU 組態。在您使用 Windows PowerShell 建立憑證之前，CA 管理員必須建立並部署支援用戶端 EKU 的新範本。</td>
    </tr>
    </tbody>
    </table>

