---
title: Lync Server 2013：使用 Lync Room System 系統管理 Web 入口網站
TOCTitle: 使用 Lync Room System 系統管理 Web 入口網站
ms:assetid: c387b2a3-3e42-4642-af72-88126ed2820f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn743660(v=OCS.15)
ms:contentKeyID: 62268983
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中使用 Lync Room System 系統管理 Web 入口網站

 

_**上次修改主題的時間：** 2014-11-10_

您在伺服器上部署 LRS 後，便可以從瀏覽器登入 LRS 系統管理 Web 入口網站，來檢查所有 LRS 會議室的狀態。

## 登入

1.  瀏覽到下列 URL：
    
    https://\<fe-server\>/lrs

2.  輸入 LRSSupport 帳戶或已新增至 LRSSupportAdminGroup 安全性群組之帳戶的認證。

![\[Lync Room System 管理入口網站登入\] 畫面](images/Dn436326.050bcf70-2f3b-46b2-9b96-ebd12679b713(OCS.15).png "[Lync Room System 管理入口網站登入] 畫面")

## LRS 系統管理 Web 入口網站摘要頁面

摘要頁面提供伺服器上已部署之所有 LRS 會議室的下列資訊：

  - **標籤**   系統管理員為會議室自訂的名稱。按一下會議室名稱，即可在入口網站中設定「標籤」。

  - **運作情況**   會議室的運作情況狀態衍生自會議室的 \[彙總運作情況\] 狀態 (此狀態顯示在 \[會議室設定\] 頁面的 \[運作情況\] 區段下)。

  - **下一次會議**   下一次會議排定的日期和時間。

  - **LRS 版本、製造商、型號**   這些值會顯示在 LRS 中。依製造商而定，這些欄位可能空白。

  - **上次重新整理**   顯示上次重新整理網頁的時間。

![Lync Room System 管理入口網站摘要檢視](images/Dn743660.f829ce90-dd95-4725-bd94-6870c5dcf046(OCS.15).png "Lync Room System 管理入口網站摘要檢視")

## LRS 會議室資訊

入口網站的 \[會議室資訊\] 區段能讓您檢視和設定個別 LRS 會議室。這包含四個區段：\[設定\]、\[詳細資料\]、\[記錄\] 和 \[運作情況\]。

## 設定

在 \[設定\] 區段中，您可以設定會議室的密碼、會議室標籤和預設音量。如果您進行這些設定，變更只會在重新啟動 LRS 主控台後複寫。

![Lync Room System 管理入口網站會議室設定](images/Dn743660.ab162e19-41ac-4991-9b2a-92575aa53eda(OCS.15).png "Lync Room System 管理入口網站會議室設定")

## 詳細資料

\[詳細資料\] 區段提供 LRS 會議室設定的唯讀摘要，包含：上次重新整理的時間；下一次會議；上次更新；維護和校準；預設喇叭、麥克風和響鈴設定；版本；SIP URI；畫面數和每個畫面的詳細資料；狀態和活動。

![Lync Room System 管理入口網站詳細資料檢視](images/Dn743660.2958bbba-db74-4670-a920-87fdfb2fc22d(OCS.15).png "Lync Room System 管理入口網站詳細資料檢視")

## 記錄

\[記錄\] 區段可用來遠端收集記錄並將記錄儲存到指定的位置。您也可以重新啟動 LRS 主控台 (LRS 使用者介面) 或重新啟動整個系統。

![Lync Room System 管理入口網站會議室登入](images/Dn743660.749aee71-deaa-4ace-a146-fe2b349f0f42(OCS.15).png "Lync Room System 管理入口網站會議室登入")

## 運作情況

\[運作情況\] 區段提供 Lync Server 連線、音訊裝置、視訊裝置、備援狀態和螢幕裝置之運作情況的視覺指示。

![Lync Room System 管理入口網站會議室健康情況](images/Dn743660.8cc644f8-8e3e-42d5-9079-045d8fe9daa7(OCS.15).png "Lync Room System 管理入口網站會議室健康情況")

## 系統管理 Web 入口網站的其他相關附註

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
<td><ul>
<li><p>基於安全性原因，系統管理 Web 入口網站每 15 分鐘會將您自動登出。</p></li>
<li><p>設定變更只有在重新啟動 LRS 系統後才會套用。</p></li>
<li><p>LRS 系統管理 Web 入口網站上的通知是固定的，換言之不會消失。</p></li>
<li><p>通知只有在重新整理頁面後才會出現。</p></li>
<li><p>重新整理頁面後會出現 LRS 會議室的狀態。</p></li>
<li><p>如果 LRSApp 帳戶密碼到期，您就無法看到會議室的狀態。請設定永不到期的 LRSAppuser 帳戶密碼，或務必在密碼即將到期時更新。</p></li>
<li><p>LRS 系統管理 Web 入口網站僅支援內部部署。</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 疑難排解

## 為什麼我無法登入系統管理 Web 入口網站？

  - 開啟 https://localhost/lrs 時有看到登入頁面，但輸入認證時無法登入。在此情況下，必須開啟 https://FQDNofFEserver/lrs，才能登入系統管理 Web 入口網站。

  - 如果您用來存取系統管理 Web 入口網站的電腦位於工作群組，"http://" 將無法運作。請改用 "https"。

## 為什麼我在系統管理 Web 入口網站中看不到 LRS？

  - 請確定您在部署中擁有 LRS 帳戶，而且帳戶是根據 LRS 系統管理 Web 入口網站部署建議而建立。確保在 Lync Server 上是使用 Enable-CsMeetingRoom (而非 Enable-CsUser) 佈建 LRS 帳戶。

  - 若已建立 LRS 帳戶，並且在系統管理 Web 入口網站中看不到帳戶，請選取 \[MeetingPortal\] 元件並使用 Lync Server 記錄工具來收集伺服器記錄，然後將記錄傳送給您的 LRS 支援連絡人。

## 為什麼我在系統管理 Web 入口網站中看不到 LRS 的狀態？

  - 確定 LRSApp 使用者帳戶已啟用 SIP。

  - 如果仍遇到問題，請在 LRS 系統中從 D:\\Tracing\\LRSAdminLogs\\ 收集 \[Trace.log\] 檔案，然後將檔案傳送給您的 LRS 支援連絡人。

