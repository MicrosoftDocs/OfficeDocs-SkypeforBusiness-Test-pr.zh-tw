---
title: 建立裝置以測試更新功能
TOCTitle: 建立裝置以測試更新功能
ms:assetid: ce509fd1-17b3-4b78-b269-fe5d06fe2e1d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg182587(v=OCS.15)
ms:contentKeyID: 49292350
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 建立裝置以測試更新功能

 

_**上次修改主題的時間：** 2013-02-23_

您可以將測試裝置新增至 \[測試裝置\] 頁面，然後先使用此裝置來確認新更新的功能，再將更新部署至生產裝置。您可以在全域 (在整個 Lync Server 環境中) 測試裝置，或在單一網站內測試裝置。您是以裝置的媒體存取控制 (MAC) 位址或序號來識別測試裝置。當您新增裝置時，它會顯示在 Lync Server 控制台之 \[測試裝置\] 頁面上的清單中。

## 若要新增測試裝置

1.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

2.  在左導覽列中，按一下 **\[用戶端\]**，然後按一下 **\[測試裝置\]**。

3.  按一下 **\[新增\]**，然後按一下 **\[全域測試裝置\]** 或 **\[網站測試裝置\]**。

4.  執行下列其中一項作業：
    
      - 如果您是按一下 **\[全域測試裝置\]**，則跳至下一步驟。
    
      - 如果您是按一下 **\[網站測試裝置\]**，請從可用網站清單中選取網站，然後按一下 \[確定\] 。

5.  在 **\[新增測試裝置\]** 中，將裝置的名稱輸入 **\[裝置名稱\]** 中。

6.  在 **\[識別元類型\]** 下，按一下 **\[MAC 位址\]** 或 **\[序號\]**。

7.  在 **\[唯一識別碼\]** 方塊中，輸入裝置的 MAC 位址或序號。

8.  按一下 \[認可\]。

## 使用 Windows PowerShell Cmdlet 建立測試裝置

您可以使用 Windows PowerShell 和 New-CsTestDevice Cmdlet 建立測試裝置。可從 Lync Server 2013 管理命令介面或 Windows PowerShell 遠端工作階段執行此 Cmdlet。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

使用此 Cmdlet 建立測試裝置時，您必須執行兩個動作：

  - 指定 MACAddress 或 SerialNumber 做為 IdentifierType。

  - 在指定裝置 Identity 時包含範圍。若要在全域範圍建立新的裝置，請使用類似如下的語法：
    
        -Identity "global/WindowsPhone"
    
    若要在網站範圍建立測試裝置，請使用類似如下的語法：
    
        -Identity "site:Redmond/WindowsPhone"

## 使用 MAC 位址建立測試裝置

  - 此命令會在全域範圍建立測試裝置，並使用 MAC 地址做為 IdentifierType：
    
        New-CsTestDevice -Identity "global/WindowsPhone" -IdentifierType "MACAddress" -Identifier "01:02:03:04:05:06"

## 使用序號建立測試裝置

  - 此命令會在 (Redmond 網站的) 網站範圍建立測試裝置，並使用序號做為 IdentifierType：
    
        New-CsTestDevice -Identity "site:Redmond/WindowsPhone" -IdentifierType "SerialNumber" -Identifier "01ABC5419JKR55T"

如需詳細資訊，請參閱 [New-CsTestDevice](new-cstestdevice.md) Cmdlet 的說明主題。

