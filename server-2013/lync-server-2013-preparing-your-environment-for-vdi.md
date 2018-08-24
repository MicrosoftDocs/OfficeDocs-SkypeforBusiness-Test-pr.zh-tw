---
title: Lync Server 2013：針對 VDI 準備環境
TOCTitle: 針對 VDI 準備環境
ms:assetid: a3ec2e13-1a73-4b1c-a54a-8db7d4cd50f9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205154(v=OCS.15)
ms:contentKeyID: 49291872
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 針對 VDI 準備 Lync Server 2013 環境

 

_**上次修改主題的時間：** 2013-02-22_

若要準備 Lync VDI 外掛程式的環境，系統管理員必須執行下列步驟。

1.  在 Lync Server 2013 中，確定所有 VDI 使用者的 EnableMediaRedirection 均設定為 TRUE。如需詳細資訊，請參閱 [New-CsClientPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsClientPolicy) Cmdlet 與 [Set-CsClientPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClientPolicy) Cmdlet 的說明主題。

2.  在資料中心電腦上，將 Lync 2013 用戶端安裝於所有虛擬機器。

3.  在本機電腦上，安裝 Lync VDI 外掛程式。

