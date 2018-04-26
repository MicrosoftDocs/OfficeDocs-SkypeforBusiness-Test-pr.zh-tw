---
title: 驗證 Lync Server 2010 環境
TOCTitle: 驗證 Lync Server 2010 環境
ms:assetid: bfc7c620-556a-43cd-b1ed-2c268ec2b5cc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205231(v=OCS.15)
ms:contentKeyID: 49292192
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 驗證 Lync Server 2010 環境

 

_**上次修改主題的時間：** 2012-10-19_

在與 Lync Server 2010 並存的狀態下部署 Lync Server 2013 之前，您必須先確認已設定並已啟動 Lync Server 2010 服務。在部署 Lync Server 2013 試驗集區前，務必要先識別舊版環境中存在的關鍵服務和功能。在與舊版 XMPP 部署並存的狀態下部署 Microsoft Lync Server 2013 XMPP 之前，您必須先確認已設定並已啟動舊版 XMPP 服務，並識別舊版 XMPP 設定支援哪些同盟協力廠商。確認舊版 Lync Server 2010 部署需要執行下列事項：

  - 確認 Lync Server 2010 服務已啟動

  - 審視 Lync Server 2010 中的拓撲和使用者。

  - 確認同盟和 Edge Server 設定。

  - 確認 XMPP 服務和同盟協力廠商。

**確認 Lync Server 2010 服務已啟動**

1.  從 Lync Server 2010 前端伺服器中瀏覽至：系統管理工具\\Services applet。

2.  驗證下列服務是否在前端伺服器中執行:
    
    ![在前端伺服器上執行的服務清單](images/JJ205231.639f2729-b759-4d8e-b4ad-59d7f68adcd2(OCS.15).jpg "在前端伺服器上執行的服務清單")

**在 Lync Server 控制台中審視 Lync Server 2010 拓撲**

1.  使用 RTCUniversalServerAdmins 群組的成員帳戶、CsAdministrator 成員帳戶或 CsUserAdministrator 系統管理角色的成員帳戶登入前端伺服器。

2.  開啟 Lync Server 控制台。

3.  選取 \[拓撲\]。 確認有列出您的 Lync Server 2010 部署中的各種伺服器。
    
    ![\[Lync Server 2010 控制台拓撲\] 頁面](images/JJ205231.338ce4fb-2162-4176-a249-ec4ae021fa6a(OCS.15).jpg "[Lync Server 2010 控制台拓撲] 頁面")

**若要在 Lync Server 控制台中審視 Lync Server 2010 使用者**

1.  開啟 Lync Server 控制台。

2.  選取 \[使用者\] ，然後按一下 \[尋找\] 。

3.  確認每位列出使用者的 \[登錄器集區\] 欄都指向 Lync Server 2010 集區。
    
    ![列出使用者的 Lync Server 2010 控制台](images/JJ205231.a9378c40-7a52-4c78-ad83-1463847c9edb(OCS.15).jpg "列出使用者的 Lync Server 2010 控制台")

**確認 Lync Server 2010 Edge 和同盟設定**

1.  啟動拓撲建置器。

2.  選擇 \[從現有部署下載拓撲\] 。

3.  選擇檔案名稱，然後依預設的 .tbxml 檔案類型儲存拓撲。

4.  展開 Lync Server 2010 節點，顯示部署中的各種伺服器角色。

5.  選取網站節點，確認是否有設定 \[網站同盟路由指派\] 值。
    
    ![拓撲產生器，網站同盟路由](images/JJ205231.87de3735-af7e-4280-8d72-c42cb0ea1c05(OCS.15).jpg "拓撲產生器，網站同盟路由")

6.  接下來，選取 Standard Edition Server 或 Enterprise Edition 前端集區。判斷 \[關聯\] 下方是否已為媒體設定 Edge 集區。
    
    ![顯示伺服器與集區的拓撲產生器](images/JJ205231.5ad5ea3b-b122-44dd-8968-f1147d6d45f1(OCS.15).jpg "顯示伺服器與集區的拓撲產生器")

7.  最後，選取 Edge 集區並識別 \[下一個躍點選取範圍\] 是否有設定下一個躍點集區。
    
    ![拓撲產生器，下一個躍點選取範圍](images/JJ205231.3121e723-fba7-498e-a786-bde7be1a55e2(OCS.15).jpg "拓撲產生器，下一個躍點選取範圍")

**確認舊版 XMPP 同盟合作夥伴設定**

1.  從舊版 XMPP 伺服器瀏覽到 \[系統管理工具\]\\\[服務\] Applet。

2.  確認 Office Communications Server XMPP 閘道服務已經啟動。
    
    ![Office Communications Server XMPP 閘道服務](images/JJ205231.23223724-3c4b-4cb9-ace2-1cab2c3c91c3(OCS.15).jpg "Office Communications Server XMPP 閘道服務")

