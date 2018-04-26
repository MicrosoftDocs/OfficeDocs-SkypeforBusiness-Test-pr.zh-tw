---
title: 設定監看員節點以使用認證驗證
TOCTitle: 設定監看員節點以使用認證驗證
ms:assetid: 032e33f3-9483-42e6-a33c-347eb6779597
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204632(v=OCS.15)
ms:contentKeyID: 49289921
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定監看員節點以使用認證驗證

 

_**上次修改主題的時間：** 2012-10-20_

如果您的監看員節點電腦位於周邊網路外部，則必須遵循稍微不同的程序，以設定監看員節點執行綜合交易。具體而言，您不應該建立信任的應用程式集區和信任的應用程式，且您必須安裝憑證，讓監看員節點能夠將通知傳送至周邊網路內的電腦。這表示您必須完成下列兩項工作：

  - 更新電腦之 RTC Local Read-only Administrators 群組中的成員資格

  - 安裝監看員節點設定檔案

## 更新 RTC Local Read-Only Administrators 群組中的成員資格

如果您的監看員節點電腦位於周邊網路外部，則必須將網路服務帳戶新增至監看員節點電腦上的 RTC Local Read-only Administrators 群組。若要執行這項操作，請在監看員節點上完成下列程序：

1.  按一下 \[開始\]，然後以滑鼠右鍵按一下 \[電腦\]，再按一下 \[管理\]。

2.  在伺服器管理員中，依序展開 \[設定\] 及 \[本機使用者和群組\]，然後按一下 \[群組\]。

3.  在 \[群組\] 窗格中，按兩下 \[RTC Local Read-only Administrators\]。

4.  在 \[RTC Local Read-only Administrators 內容\] 對話方塊中，按一下 \[新增\]。

5.  在 \[選取使用者、電腦、服務帳戶或群組\] 對話方塊中，按一下 \[位置\]。

6.  在 \[位置\] 對話方塊中，選取監看員節點電腦的名稱，然後按一下 \[確定\]。

7.  在 \[輸入物件名稱來選取\] 方塊中，輸入 \[網路服務\]，然後按一下 \[確定\]。

8.  在 \[RTC Local Read-only Administrators 內容\] 對話方塊中，按一下 \[確定\]，然後關閉 \[伺服器管理員\]。

重新啟動監看員節點電腦。

## 安裝監看員節點設定檔案

重新啟動監看員節點電腦之後，下一個步驟是執行 Watchernode.msi 檔案。若要執行此檔案，請依序按一下 \[開始\]、\[所有程式\]、\[Lync Server 2013\] 及 \[Lync Server 管理命令介面\]，來開啟 Lync Server 2013 管理命令介面。在 Lync Server 管理命令介面中，輸入下列命令，然後按 ENTER 鍵 (請確定並指定 Watchernode.msi 複本的實際路徑)：

    C:\Tools\Watchernode.msi Authentication=Negotiate

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如前所述，Watchernode.msi 也可以透過命令視窗來執行。若要開啟命令視窗，請按一下 [開始]，然後以滑鼠右鍵按一下 [命令提示字元]，再按一下 [以系統管理員身分執行]。開啟命令視窗時，輸入與稍早所示相同的命令。</td>
</tr>
</tbody>
</table>


您可以在無法將監看員節點設為信任的應用程式集區時，使用交涉模式。在此模式中，系統管理員必須在監看員節點上管理測試使用者密碼。

