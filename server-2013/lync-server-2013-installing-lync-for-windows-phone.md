---
title: 安裝 Lync for Windows Phone
TOCTitle: 安裝 Lync for Windows Phone
ms:assetid: bf502546-ff69-489f-a92e-a78b58803d53
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690996(v=OCS.15)
ms:contentKeyID: 52056190
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 安裝 Lync for Windows Phone

 

_**上次修改主題的時間：** 2014-02-03_

Lync 2013 for Windows Phone 是 Windows Phone 市集中可供使用者安裝的應用程式。

## 安裝 Lync for Windows Mobile

您可以將使用者導向至 Windows Phone 市集 (<http://go.microsoft.com/fwlink/?linkid=231901>)，以指示使用者在其裝置上安裝 Lync 2013 for Windows Phone。

## 如果您使用 DNS SRV 記錄發佈 Exchange Web 服務

為了針對 Lync 用戶端啟用 Exchange 整合，某些組織會使用 DNS SRV 記錄發佈 Exchange Web 服務 URL。位於 Microsoft 下載中心的「了解及疑難排解 Exchange 整合」文件 (網址為 [http://go.microsoft.com/fwlink/?LinkID=391095](http://go.microsoft.com/fwlink/?linkid=391095))，描述了需要這樣做的案例。但是，針對 Windows Phone 使用者的 Exchange 整合不適用於此案例，因為 Windows Phone 平台並不支援 SRV 查閱。您需要指示 Windows Phone 使用者指定 Exchange Web 服務 URL，而非允許電話自動偵測伺服器。

指示您的使用者在其 Windows Phone 上設定 Lync 設定，方法如下：

1.  在 Windows Phone 的 Lync 設定中，選取 **\[Exchange\]** 畫面。

2.  將 **\[自動偵測伺服器\]** 移至 **\[關閉\]**。

3.  點選空白欄為並輸入 Exchange Web 服務的完整網域名稱 (FQDN) 或 URL。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您可以指定 Exchange Web 服務伺服器的完整網域名稱 (FQDN) 或完整 URL。如果您指定 FQDN，會自動新增通訊協定 (https://) 與 Exchange Web 服務路徑 (/ews/exchange.asmx)。如果您的 Exchange Web 服務路徑不同，您可以指定完整 URL。</td>
    </tr>
    </tbody>
    </table>


4.  關閉畫面。

## 確認行動用戶端安裝

在成功地設定用戶端及登入後，請使用下列測試來確認 Lync 2013 的安裝能在行動裝置上正確運作。

**在公司目錄中搜尋連絡人**

1.  在連絡人清單中，點選底部的 \[搜尋\]。

2.  搜尋只存在於全域通訊清單 (GAL) 中的連絡人。

3.  確認連絡人名稱出現在搜尋結果中。

**測試立即訊息和目前狀態**

1.  在 \[連絡人\] 清單中，點選連絡人。

2.  在連絡人卡片中點選 IM 圖示。

3.  確認顯示立即訊息 (IM) 視窗，且您可以輸入及傳送 IM。

**測試電話撥出式會議**

1.  在 Outlook 中，排程 Lync 會議。

2.  在行動裝置上，開啟會議邀請。

3.  按一下會議中的連結以加入。

4.  從會議服務接聽來電，並確認您已連線至會議音訊。

**測試推入通知**

1.  在使用者 A 的行動裝置上，以使用者 A 的帳戶登入 Lync。

2.  在行動裝置上開啟其他應用程式。

3.  在不同的用戶端上，以使用者 B 的帳戶登入 Lync。

4.  從使用者 B 傳送 IM 給使用者 A。

5.  確認 IM 通知出現在使用者 A 的行動裝置上。

