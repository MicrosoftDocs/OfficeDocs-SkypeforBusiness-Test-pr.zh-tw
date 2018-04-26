---
title: Lync Server 2013：Lync VDI 外掛程式先決條件
TOCTitle: Lync VDI 外掛程式先決條件
ms:assetid: da25a976-7624-4dfc-b332-9c4db4ee78da
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205304(v=OCS.15)
ms:contentKeyID: 49292496
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Lync VDI 外掛程式先決條件

 

_**上次修改主題的時間：** 2015-07-20_

在虛擬桌面基礎結構 (VDI) 環境中，虛擬機器與使用者的本機電腦必須符合本節概述的需求。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如需如何安裝和部署虛擬環境的詳細資訊，請參閱虛擬解決方案提供者。如需以 Hyper-V 與遠端桌面服務為基礎部署虛擬環境的詳細資訊，請參閱下列的 Microsoft TechNet 文件庫文章：
<ul>
<li><p>＜Hyper-V＞，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=247514" class="uri">http://go.microsoft.com/fwlink/?linkid=247514</a></p></li>
<li><p>Windows Server 2008 R2 中的＜遠端桌面服務＞，網址為 <a href="http://go.microsoft.com/fwlink/?linkid=247513" class="uri">http://go.microsoft.com/fwlink/?linkid=247513</a></p></li>
</ul></td>
</tr>
</tbody>
</table>


下列是在資料中心電腦上執行虛擬機器的需求：

  - 虛擬機器必須使用含有最新的 Service Pack 的 Windows 8、 Windows 7 或 Windows Server 2008 R2 來設定。

下列是使用者及其本機電腦的需求：

  - 使用者必須裝載於 Lync Server 2013。

  - 本機電腦必須執行 Windows Embedded Standard 7 (含 SP1)、 Windows 7 (含 SP1) 或 Windows 8。

  - 如果您使用遠端桌面服務， Lync VDI 外掛程式位元 (亦即 32 位元或 64 位元應用程式) 必須符合本機電腦的作業系統位元。本機系統上的作業系統位元與虛擬機器上的作業系統位元不需要相符。如果您使用另一種虛擬解決方案或平台，請參閱虛擬解決方案提供者提供關於位元需求的指引。

  - 本機電腦必須執行最新的遠端桌面用戶端版本。請安裝 Microsoft 的最新遠端桌面服務用戶端更新，或是虛擬解決方案提供者的最新遠端桌面用戶端軟體。如需最新的遠端桌面服務更新，請參閱 <http://go.microsoft.com/fwlink/?linkid=268032>。

  - 在本機電腦上，您必須進行遠端桌面用戶端設定，以讓音訊可在本機電腦上播放，並停用遠端錄製功能。若要進行 Windows 中的這些遠端桌面連線設定，請參閱下一節＜設定遠端桌面連線設定＞。

## 設定遠端桌面連線設定

若要準備 Windows 中的遠端桌面連線，以供 Lync VDI 外掛程式使用，請遵循下列步驟。

1.  如果本機電腦執行 Windows 8，請略過此步驟。如果本機電腦執行 Windows 7 (含 SP1)，請安裝最新的 Windows 8 遠端桌面服務用戶端版本，網址為 <http://go.microsoft.com/fwlink/?linkid=268032>。

2.  按一下\[開始\] ，然後按一下 \[遠端桌面連線\] ，以啟動遠端桌面服務用戶端。

3.  按一下 \[選項\] 。

4.  按一下 \[本機資源\] 索引標籤。在 \[遠端音訊\] 之下，按一下 \[設定\] ，然後執行下列動作：
    
      - 在 \[遠端音效播放\] 之下，選取 \[在這部電腦上播放\] 。
    
      - 在 \[遠端音效錄製\] 之下，選取 \[不錄製\] 。
    
      - 按一下 \[確定\] 。

5.  按一下 \[效能體驗\] 索引標籤。在 \[效能\] 下，清除 \[持續性點陣圖快取\] 核取方塊。

6.  按一下 \[一般\] 索引標籤。在 \[電腦\] 中，輸入虛擬機器的名稱，然後按一下 \[連線\] 。

