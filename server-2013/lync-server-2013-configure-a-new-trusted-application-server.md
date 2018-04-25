---
title: 在 Lync Server 2013 中設定新的受信任應用程式伺服器
TOCTitle: 在 Lync Server 2013 中設定新的受信任應用程式伺服器
ms:assetid: a7233db7-fac3-43ff-972e-3bc29a56adb3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg617964(v=OCS.15)
ms:contentKeyID: 49291922
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定新的受信任應用程式伺服器

 

_**上次修改主題的時間：** 2012-11-01_

信任的應用程式是指以 Microsoft Unified Communications Managed API (UCMA) 3.0 Core SDK 所信任的 Microsoft Lync Server 2013 為基礎的應用程式。如需有關 UCMA 應用程式的詳細資訊，請參閱＜Unified Communications Managed API 3.0 Core SDK 文件＞，網址為 [http://go.microsoft.com/fwlink/?linkid=210320\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=210320%26clcid=0x404)。

如需關於設定 Microsoft Outlook Web Access (OWA) 和 Lync Server 2013 的詳細資訊，請參閱 Microsoft Exchange Server 2013 文件中的＜設定 Outlook Web App 和 Lync Server 2010 整合＞。

您應以 RTCUniversalServerAdmins 及 Domain Admins 群組成員的身分登入，才能在加入或移除伺服器角色時，成功地發行、啟用或停用拓撲。 另外也可委派適當的系統管理員權限來加入伺服器角色。如需詳細資訊，請參閱部署文件中的[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)。若要進行其他組態變更，則僅需要 RTCUniversalServerAdmins 群組中的成員資格。

## 若要設定信任的應用程式伺服器

1.  以 Domain Admins 群組與 RTCUniversalServerAdmins 群組成員的身分，登入安裝了拓撲產生器的電腦。

2.  啟動拓撲產生器：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 拓撲產生器\]。

3.  選取 **\[從現有部署下載拓撲\]**，然後按一下 \[確定\] 。

4.  在 **\[另存拓撲\]** 對話方塊中，按一下您要使用的拓撲產生器檔案，然後按一下 **\[儲存\]**。

5.  在左側窗格中，以滑鼠右鍵按一下 \[信任的應用程式伺服器\]，然後按一下 \[新增信任的應用程式集區\]。

6.  輸入信任的應用程式集區的 **\[集區 FQDN\]**，選擇要讓它成為單一伺服器或多部伺服器，然後按 **\[下一步\]**。

7.  在 \[選取下一個躍點\] 頁面上，從清單中選取 \[Lync Server 2013 前端集區\]。

8.  按一下 \[完成\]。

9.  選取最上方的節點 \[Lync Server 2013\]，然後按一下 \[執行\] 功能表中的 \[發行拓撲\]。
    
    **\[信任的應用程式集區\]** 應該已經成功建立，並且與正確的前端集區產生關聯。

