---
title: Lync Server 2013：範例 XMPP 設定 – XMPP 與 Google Talk 的同盟
TOCTitle: 範例 XMPP 設定 – XMPP 與 Google Talk 的同盟
ms:assetid: 360a2f7b-015b-4e93-ac67-0f609c21f1a2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204807(v=OCS.15)
ms:contentKeyID: 49290573
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的範例 XMPP 設定 – XMPP 與 Google Talk 的同盟

 

_**上次修改主題的時間：** 2014-04-22_

用以部署 XMPP Proxy 的範例設定會定義與 Google Talk 的同盟。

## 範例 XMPP 設定 – XMPP 與 Google Talk 的同盟

1.  在 前端伺服器 上，開啟 \[Lync Server 部署精靈\]。按一下 \[安裝\] 或 \[更新 Lync Server 系統\]，然後按一下 \[安裝\] 或 \[移除 Lync Server 元件\]。按一下 \[再執行一次\]。

2.  在 **\[安裝 Lync Server 元件\]** 上，按 **\[下一步\]** 。摘要畫面將顯示它們執行的動作。完成部署之後，按一下 **\[檢視記錄\]** 以檢視可用的記錄檔。按一下 **\[完成\]** 以完成部署。

3.  在 Edge Server 上，開啟 \[ Lync Server 部署精靈\]。按一下 **\[安裝或更新 Lync Server 系統\]** ，然後按一下 **\[安裝或移除 Lync Server 元件\]** 。按一下 **\[再執行一次\]** 。

4.  新增 Google Talk 做為 XMPP 允許的協力廠商。針對伺服器對伺服器的 XMPP 同盟，Google Talk 目前僅支援未加密的 TCP 連線，並且僅支援 \[伺服器回撥\] 來進行身分識別驗證 (請參閱 <http://xmpp.org/extensions/xep-0220.html>)。
    
        New-CsXmppAllowedPartner gmail.com -TlsNegotiation NotSupported -SaslNegotiation NotSupported -EnableKeepAlive $false -SupportDialbackNegotiation $true

5.  若要啟用 Edge 同盟，請輸入下列項目：
    
        Set-CsAccessEdgeConfiguration -AllowFederatedUsers $true

6.  在 **\[安裝 Lync Server 元件\]** 上，按 **\[下一步\]** 。摘要畫面將顯示它們執行的動作。完成部署之後，按一下 **\[檢視記錄\]** 以檢視可用的記錄檔。按一下 **\[完成\]** 以完成部署。

7.  在 Edge Server 的 \[ Lync Server 部署精靈\] 中，按一下 **\[步驟3: 要求、安裝或指派憑證\]** 旁的 **\[再執行一次\]** 。
    
    > [!TIP]
    > 如果您是第一次部署 Edge Server，則會顯示 [執行]，而非 [再執行一次]。


8.  在 \[可用憑證工作\] 頁面上，按一下 \[建立新憑證要求\] 。

9.  在 \[憑證要求\] 頁面上，按一下 \[外部邊緣憑證\] 。

10. 在 \[延遲或立即要求\] 頁面上，選取 \[立即準備此要求，但稍後再傳送\] 核取方塊。

11. 在 \[憑證要求檔案\] 頁面上，輸入用來儲存此要求的檔案完整路徑和名稱 (例如，c:\\cert\_exernal\_edge.cer)。

12. 若要使用預設 WebServer 範本之外的其他範本，在 \[指定其他憑證範本\] 頁面上，選取 \[針對選取的憑證授權單位使用其他憑證範本\] 核取方塊。

13. 在 \[名稱和安全性設定\] 頁面上，執行下列動作：
    
    1.  在 **\[易記名稱\]** 中，輸入憑證的顯示名稱
    
    2.  在 **\[位元長度\]** 中，指定位元長度 (預設值通常為 **\[2048\]** )
    
    3.  確認已選取 **\[將憑證的私密金鑰標記為可匯出\]** 核取方塊

14. 在 **\[組織資訊\]** 頁面中，輸入組織的名稱和組織單位 (例如，事業處或部門)

15. 在 **\[地理資訊\]** 頁面上，指定位置資訊

16. 在 **\[主體名稱/主體替代名稱\]** 頁面上，會顯示精靈自動填入的資訊。如果您還需要其他主體替代名稱，請在後續兩個步驟中指定

17. 在 \[主體替代名稱 (SAN) 上的 SIP 網域設定\] 頁面上，選取網域核取方塊，將 sip.*\<sipdomain\>* 項目新增至主體替代名稱清單中。

18. 在 \[設定其他主體別名\] 頁面上，指定任何需要的其他主體別名。
    
    > [!TIP]
    > 如果有安裝 XMPP Proxy，預設會在 SAN 項目中填入網域名稱 (如 contoso.com)。如果您需要其他項目，請在此步驟中新增。


19. 在 \[要求摘要\] 頁面上，檢閱要用來產生要求的憑證資訊。

20. 當命令執行完畢之後，您可以 \[檢視記錄檔\] ，或按 \[下一步\] 繼續。

21. 在 \[憑證要求檔案\] 頁面上，可以按一下 \[檢視\] 檢視產生的憑證簽署要求 (CSR) 檔，或按一下 \[完成\] 結束憑證精靈。

22. 複製要求檔案並送出到您的公用憑證授權單位。

23. 接收、匯入和指派公用憑證之後，您必須停止並重新啟動 Edge Server 服務。 啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。。在 Lync Server 管理命令介面 中輸入：
    
    ```
    Stop-CsWindowsService
    ```
    ```
    Start-CsWindowsService
    ```

24. 若要設定 DNS 以用於 XMPP 同盟，您可以將下列 SRV 記錄新增至外部 DNS:\_xmpp-server.\_tcp.*\<domain name\>* SRV 記錄將解析至 Edge Server 的 Access Edge FQDN，且連接埠值為 5269

25. 在 前端伺服器上開啟 Lync Server 管理命令介面，然後輸入下列內容，藉以設定新的外部存取原則來啟用所有使用者：
    
        New-CsExternalAccessPolicy -Identity FedPic -EnableFederationAccess $true -EnablePublicCloudAccess $true
        Get-CsUser | Grant-CsExternalAccessPolicy -PolicyName FedPic

