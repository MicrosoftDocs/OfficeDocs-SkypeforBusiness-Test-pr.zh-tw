---
title: 從 Lync Server 2013 評估版更新
TOCTitle: 從 Lync Server 2013 評估版更新
ms:assetid: 62a88180-4289-4a2a-9cb9-1b9899344a63
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg521005(v=OCS.15)
ms:contentKeyID: 49291104
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 從 Lync Server 2013 評估版更新

 

_**上次修改主題的時間：** 2012-06-20_

如果您已安裝 Microsoft Lync Server 2013 的評估版本，則最後需要使用軟體授權版本更新該安裝；原因是評估版本會在安裝後 180 天到期。不過，您不需要完全解除安裝評估版本，然後再安裝授權版本。而是在取得有效授權金鑰之後，可以於每部作為 Lync Server 前端伺服器、Director 或 Edge Server 的電腦上執行下列程序，以更新 Lync Server 2013 的評估版本。請注意，您不需要更新執行其他伺服器角色 (如監控伺服器或封存伺服器) 的電腦。

## 從 Microsoft Lync Server 2013 的評估版本更新

若要將電腦從 Lync Server 2013 的評估版本更新為授權版本軟體：

**從 Microsoft Lync Server 2013 的評估版本更新**

1.  以本機系統管理員身分登入電腦。

2.  依序按一下 **\[開始\]**、**\[所有程式\]**、**\[Microsoft Lync Server 2013\]** 及 **\[Lync Server 管理命令介面\]**。

3.  在 Lync Server 管理命令介面中，輸入下列命令，然後按 ENTER 鍵：
    
        msiexec.exe /fvomus server.msi EVALTOFULL=1 /qb
    
    請注意，您可能需要指定檔案 server.msi 的完整路徑。此檔案位於 Lync Server 磁碟區媒體安裝檔案的 Setup 資料夾中。

4.  安裝程式完成執行之後，從命令提示字元中輸入下列命令，然後按 ENTER 鍵：
    
        Enable-CsComputer

5.  在執行 Lync Server 之評估版本的任何其他前端伺服器、Director 或 Edge Server 上，重複此程序。在使用 Lync Server 媒體安裝檔案所部署的任何分公司伺服器上，也應該執行此程序。

如果您不確定給定電腦上是否執行 Lync Server 的評估版本，則可以從 Lync Server 管理命令介面執行下列命令以進行驗證：

    Get-CsServerVersion

[Get-CsServerVersion](get-csserverversion.md) Cmdlet 會分析本機電腦，並回報下列其中一項：

  - Lync Server 大量授權金鑰已安裝在電腦上，表示不需要更新。

  - 已安裝 Lync Server 評估授權金鑰，表示必須更新電腦。

  - 電腦上不需要大量授權金鑰。只有在前端伺服器、Director 及 Edge Server 上才需要從評估版本更新為授權版本。

