---
title: Lync Server 2013：安裝本機設定存放區
TOCTitle: 安裝本機設定存放區
ms:assetid: b563030d-d338-411f-9611-28d5eb4b3238
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412874(v=OCS.15)
ms:contentKeyID: 49292076
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中安裝本機設定存放區

 

_**上次修改主題的時間：** 2014-06-27_

在遵循這些步驟操作前，請確認您已使用同時具備本機系統管理員與 RTCUniversalReadOnlyAdmin 群組成員身分的網域使用者帳戶登入伺服器。

為了能夠執行 Lync Server 部署精靈的所有操作，伺服器上必須具有本機設定存放區。本機設定存放區是在本機安裝 SQL Server Express 後所建立之中央管理存放區的唯讀複本。中央管理存放區本身則會新增至 Standard Edition 伺服器 或 SQL Server Express 型資料庫上所安裝的現有 SQL Server 資料庫。

> [!IMPORTANT]  
> 若您先前未在此伺服器上執行 Lync Server 2013 安裝程式，系統將提示您提供要安裝 Lync Server 2013 的目標磁碟機與路徑。如此您將得以在組織另有要求或有空間疑慮時將檔案安裝至系統磁碟機以外的磁碟機。您可以直接在安裝程式對話方塊中將 Lync Server 檔案的安裝位置路徑變更至新的可用磁碟機。包含 OCSCore.msi 在內的安裝程式檔案所安裝的路徑，將也會是其他 Lync Server 2013 檔案的部署位置。



## 若要安裝本機設定存放區

1.  從安裝媒體，瀏覽至 \\setup\\amd64\\Setup.exe，然後按一下 \[確定\]。

2.  如果系統提示您安裝 Microsoft Visual C++ 2012 可轉散發套件，請按一下 \[是\]。

3.  在 \[Lync Server 2013 安裝位置\] 頁面中，按一下 \[確定\]。

4.  在 \[使用者授權合約\] 頁面中，檢閱授權條款，然後選取 \[我接受授權合約中的條款\]，然後按一下 \[確定\] 以繼續操作。

5.  在 \[部署精靈\] 頁面上，按一下 **\[安裝或更新 Lync Server 系統\]** 。

6.  在 \[ Lync Server 2013\] 頁面上的 \[步驟 1：安裝本機設定存放區\] 旁邊，按一下 \[執行\] 。

7.  在 \[安裝本機設定存放區\] 頁面上，確定已選取 \[直接從中央管理存放區擷取\] 選項，然後按一下 \[下一步\]。

8.  當本機伺服器設定安裝完成時，按一下 \[完成\]。

