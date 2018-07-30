---
title: Lync Server 2013：安裝中繼伺服器的檔案
TOCTitle: 安裝中繼伺服器的檔案
ms:assetid: f0f7dd15-58e1-40fd-aa7e-6db50ceafacd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412998(v=OCS.15)
ms:contentKeyID: 49292768
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中安裝中繼伺服器的檔案

 

_**上次修改主題的時間：** 2012-08-06_

若要成功完成此程序，您至少應該以本機系統管理員的身分，以及至少擁有 RTCUniversalReadOnlyAdmins 群組成員資格的網域使用者身分，登入伺服器。

請使用本主題中的步驟執行 Lync Server 2013 部署精靈，在您使用拓撲產生器定義與發佈 中繼伺服器集區 時新增至該集區的電腦上，安裝 中繼伺服器 的檔案。安裝 中繼伺服器 的檔案時，也會安裝與指派 中繼伺服器集區 中每一部電腦需要的憑證。

在此站上，如果您已部署配置在 前端集區 或 Standard Edition 伺服器 上的 中繼伺服器，則可以略過此主題，繼續進行 [在 Lync Server 2013 中設定主幹](lync-server-2013-configuring-trunks.md)。

> [!NOTE]  
> 本主題假設您已定義和發佈獨立 中繼伺服器集區，如部署文件中的 <a href="lync-server-2013-define-a-mediation-server-in-topology-builder.md">在 Lync Server 2013 的拓撲產生器中定義中繼伺服器</a>與 <a href="lync-server-2013-publish-the-topology.md">在 Lync Server 2013 中發行拓撲</a>所述，而且您已確認 中繼伺服器集區 中的電腦符合 <a href="lync-server-2013-software-prerequisites-for-enterprise-voice.md">Lync Server 2013 中 Enterprise Voice 的軟體先決條件</a>與 <a href="lync-server-2013-security-and-configuration-prerequisites-for-enterprise-voice.md">Lync Server 2013 中 Enterprise Voice 的安全性和組態先決條件</a>中所述的先決條件。



## 若要安裝獨立中繼伺服器集區的檔案

1.  在安裝媒體中，以滑鼠右鍵按一下 *\<installation media\>***\\Setup\\amd64\\Setup.exe**，然後按一下 \[以系統管理員身分執行\]。

2.  在 \[安裝位置\] 頁面上，按一下 \[確定\] 。

3.  在 \[使用者授權合約\] 頁面上，按一下 \[我接受\] ，然後按一下 \[確定\] (必須執行才能繼續作業)。

4.  在 \[Lync Server 2010 部署精靈\] 頁面上，按一下 \[安裝或更新 Lync Server 系統\] 。

5.  在 \[步驟 1: 安裝本機設定存放區\] 旁邊，按一下 \[執行\] ，然後依照畫面上的指示執行。

6.  在 \[設定中央管理存放區的本機複本\] 頁面上，接受預設的 \[直接從中央管理存放區擷取\] ，然後按 \[下一步\] 。

7.  在 \[執行命令\] 頁面上，當工作狀態顯示為 \[已完成\] 時，按一下 \[完成\] 。

8.  在 \[步驟 2: 安裝或移除 Lync Server 元件\] 旁邊，依序按一下 \[執行\] \[下一步\] 。

9.  在 \[執行命令\] 頁面上，當工作狀態顯示為 \[已完成\] 時，按一下 \[完成\] 。

10. 在 \[步驟 3: 要求、安裝或指派憑證\] ，按一下 \[執行\] 。依照畫面上的指示，接受預設設定。中繼伺服器需要一個憑證，因此您將執行 \[步驟 3\] 兩次：一次發出必要的憑證，另一次指派憑證。

11. 正確發出並指派憑證之後，在 \[步驟 4:啟動服務\] 旁邊按一下 \[執行\] ，然後依照畫面上的指示執行。

12. 當 \[步驟 4\] 成功完成時，重新啟動伺服器，然後以 DomainAdmins 群組成員的身分登入伺服器。

13. 在執行 Lync Server 控制台 的電腦上，確認在 Lync Server 控制台 的 \[拓撲\] 頁面中，中繼伺服器的服務狀態顯示綠色的核取記號。如果是出現紅色的 X，請選取中繼伺服器。在 \[執行\] 功能表上，按一下 \[啟動所有服務\] 。

如果您在中繼伺服器集區中加入了多部電腦，請在 中繼伺服器集區 中的所有其他電腦上執行此程序中的步驟。如果您不需要為任何其他電腦安裝 中繼伺服器 的檔案，則依照 [在 Lync Server 2013 中設定主幹](lync-server-2013-configuring-trunks.md)中的程序設定此 中繼伺服器集區 (或網站上的所有中繼伺服器) 與其對等之間的主幹連接設定。

## 請參閱

#### 概念

[Lync Server 2013 中內部伺服器的憑證需求](lync-server-2013-certificate-requirements-for-internal-servers.md)

