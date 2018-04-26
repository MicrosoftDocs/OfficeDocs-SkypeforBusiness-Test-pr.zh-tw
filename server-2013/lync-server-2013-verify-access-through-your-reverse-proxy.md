---
title: Lync Server 2013：確認透過您的反向 Proxy 進行存取
TOCTitle: 確認透過您的反向 Proxy 進行存取
ms:assetid: 3076a786-e022-4d41-91ec-1bf252b2a468
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg429697(v=OCS.15)
ms:contentKeyID: 49290492
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中確認透過您的反向 Proxy 進行存取

 

_**上次修改主題的時間：** 2013-03-29_

請使用下列程序，確認您的使用者可以存取反向 Proxy 的資訊。您可能必須先完成防火牆設定與網域名稱系統 (DNS) 設定，存取才能正常運作。

## 若要確認您可以透過網際網路存取網站

  - 開啟網頁瀏覽器，依照下列方式在 **\[網址\]** 列輸入用戶端用來存取通訊錄檔案與網站以進行會議的 URL：
    
      - 如果是 Address Book Server，請輸入類似下面的 URL：**https://*externalwebfarmFQDN*/abs**，其中 *externalwebfarmFQDN* 是裝載 Address Book 服務之外部 Web 服務的外部 FQDN。使用者應該會收到 HTTP 挑戰，因為 Address Book Server 資料夾的目錄安全性預設是設定為 Windows 驗證。
    
      - 如果是會議，請輸入類似下面的 URL：**https://*externalwebfarmFQDN*/meet**，其中 *externalwebfarmFQDN* 是裝載會議內容之 Web 伺服器陣列的外部 FQDN。此 URL 應該會顯示會議的疑難排解網頁。或者請確認您會議的簡單 URL 是否可正確運作。會議加入的簡單 URL 範例可能為 https://meet.contoso.com
    
      - 如果是通訊群組擴充，請輸入類似下面的 URL：**https:// *externalwebfarmFQDN*/GroupExpansion/service.svc**。使用者應該會收到 HTTP 挑戰，因為通訊群組擴充服務上的目錄安全性預設是設定為 Windows 驗證。
    
      - 如果是電話撥入，請輸入類似下面的 URL：**https://*externalwebfarmFQDN*/dialin**，其中 *externalwebfarmFQDN* 是 Web 伺服器陣列的外部 FQDN，該伺服器陣列裝載電話撥入會議的電話撥入頁面。使用者應該會被導向至撥入頁面。或者請確認您會議的簡單 URL 是否可正確運作。電話撥入的簡單 URL 範例可能為 https://dialin.contoso.com
    
      - 若要確認自動探索 URL 是否正常運作，請輸入 https://lyncdiscover.*externaldomainFQDN*。瀏覽器應會提示您開啟檔案。選取「記事本」以開啟檔案。典型的回應會類似這樣：
        
            {"AccessLocation":"External","Root":{"Links":[{"href":"https:\/\/extweb.contoso.com\/Autodiscover\/AutodiscoverService.svc\/root\/domain","token":"Domain"},
            {"href":"https:\/\/extweb.contoso.com\/Autodiscover\/AutodiscoverService.svc\/root\/user","token":"User"},
            {"href":"https:\/\/lyncweb.contoso.com\/Autodiscover\/AutodiscoverService.svc\/root\/oauth\/user","token":"OAuth"}]}}

