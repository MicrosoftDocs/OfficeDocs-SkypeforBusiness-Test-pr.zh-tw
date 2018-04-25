---
title: 環境測試的問題
TOCTitle: 環境測試的問題
ms:assetid: ff1fe0d3-35b2-41ef-87e7-6a61e9e1d2ca
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205421(v=OCS.15)
ms:contentKeyID: 49292930
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 環境測試的問題

 

_**上次修改主題的時間：** 2012-09-21_

「最佳做法分析程式」是供您驗證 Lync Server 2013 環境設定是否受支援的方式 。「最佳做法分析程式」是「Active Directory 網域服務」檢查的一部份，會進行下列作業：

  - 驗證「Active Directory 網域服務」樹系與結構描述的準備。

  - 識別部署中「Active Directory 網域服務」網站與網域的數量。

  - 檢查樹系與網域層級。

  - 檢查網域控制器版本。

  - 識別網域、設定與結構描述命名內容。

  - 識別啟用的使用者數量。

  - 檢查儲存全域「Active Directory 網域服務」 設定值的位置。

  - 檢查 Lync Server 的服務連接點 (SCP)。

  - 識別資料庫版本。

## 解決環境問題。

如果環境測試發現您的環境有問題，這些問題可能是由 Active Directory 設定或特定伺服器上執行之軟體的層級所引起。例如，如果「最佳做法分析程式」識別出執行 Windows Server 2000 的環境中有任何網域控制器，即會發出警告，您就必須將這些網域控制器升級為 Windows Server 支援的版本。

