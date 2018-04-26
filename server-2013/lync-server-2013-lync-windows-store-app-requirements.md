---
title: Lync Windows 市集應用程式需求
TOCTitle: Lync Windows 市集應用程式需求
ms:assetid: 5f2e0a40-8450-4f61-b6f6-913fc1906020
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ823129(v=OCS.15)
ms:contentKeyID: 52056114
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Windows 市集應用程式需求

 

_**上次修改主題的時間：** 2013-12-03_

具有 Lync Server 內部部署的組織必須符合下列需求，才能支援 Lync Windows 市集應用程式。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>針對 Lync Server 2010，請於所有伺服器上執行 Lync Server 2010 累計更新 (2012 年 2 月) (可於 <a href="http://go.microsoft.com/fwlink/?linkid=3052%26kbid=2670352" class="uri">http://go.microsoft.com/fwlink/?linkid=3052&amp;kbid=2670352</a> 取得) 或更新版本。若要讓使用者能夠加入會議，請於伺服器上執行 Lync Server 2010 累計更新 (2012 年 10 月) (可於 <a href="http://go.microsoft.com/fwlink/?linkid=3052%26kbid=2737915" class="uri">http://go.microsoft.com/fwlink/?linkid=3052&amp;kbid=2737915</a> 取得)。</td>
</tr>
</tbody>
</table>


  - 在伺服器上啟用自動探索、Lync Web App 和 Web 票證服務。

  - 在 前端伺服器 或 前端集區 上啟用憑證驗證 (前端伺服器 或 前端集區 上的使用者登錄程序通常是指登錄器)。如需詳細資訊，請參閱[建立登錄器組態設定](lync-server-2013-create-registrar-configuration-settings.md)。

  - 為自動探索服務發行 DNS 別名 (CNAME) 資源記錄。

  - 目前已不再需要確認發給 Lync 伺服器之憑證的憑證撤銷清單 (CRL) 發佈點 (CDP) 指向 HTTP 資源而非 LDAP 資源。然而，請確認用戶端電腦已安裝最新的 Windows 更新。

  - 設定企業的 HTTP Proxy 以允許與 Lync 伺服器相關的 HTTP 流量。 如有需要，請為自動探索、Lync Web App 和 Web 票證服務新增例外。

  - 在用戶端上安裝 Windows 8.1 和最新版 Lync Windows 市集應用程式，以修正使用多個網域時常發生的登入問題 (例如，若 SIP URI 為 **userA@domainZ.com** 但 Edge Server 為 **sip.domainX.com**)。

如果您的組織訂閱 Lync Online 或 Office 365，而您是使用自己的網域名稱，您必須進行額外步驟設定網路，以自動探索 Lync 伺服器。Lync Windows 市集應用程式 和行動裝置上的 Lync 網路組態需求是相同的。請遵循 Office 365 wiki 文章＜設定 Lync 行動裝置＞(英文) 中的「設定網路」指示進行，網址為：[http://go.microsoft.com/fwlink/?LinkId=271822](http://go.microsoft.com/fwlink/?linkid=271822)。

## 請參閱

#### 概念

[部署 Lync Windows 市集應用程式](lync-server-2013-deploying-lync-windows-store-app.md)

