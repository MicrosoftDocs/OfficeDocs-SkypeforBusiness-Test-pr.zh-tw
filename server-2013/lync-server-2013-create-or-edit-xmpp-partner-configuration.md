---
title: Lync Server 2013：建立或編輯 XMPP 夥伴設定
TOCTitle: 建立或編輯 XMPP 夥伴設定
ms:assetid: 362dbe5e-8ee9-4aba-8c26-5907312b4a60
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ552447(v=OCS.15)
ms:contentKeyID: 49290575
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建立或編輯 XMPP 夥伴設定

 

_**上次修改主題的時間：** 2014-09-03_

Microsoft Lync Server 2013 會整合 Edge Server 上的 Extensible Messaging and Presence Protocol (XMPP) Proxy 和 前端伺服器或 前端集區上的 XMPP 閘道。若要允許來自其他 XMPP 部署的連線，您必須在 Lync Server 控制台中設定 XMPP。您可以根據 XMPP 網域進行設定。若要建立新的協力廠商關聯，您必須執行下列動作：

## 建立新的同盟協力廠商或編輯現有的設定

1.  使用 RTCUniversalServerAdmins 群組成員 (或具有相等使用者權限)，或指派給 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，按一下 **\[同盟和外部存取\]** ，然後按一下 **\[XMPP 同盟協力廠商\]** 。

4.  若要建立新設定，按一下 **\[新增\]**

5.  若要編輯現有的設定，可選取該設定，然後按一下 **\[編輯\]**

6.  若要建立或編輯 **\[XMPP 同盟協力廠商\]** 的設定，您要定義下列設定：

7.  **主要網域** (必要)。主要網域是 XMPP 協力廠商的基底網域。例如，您可以輸入 **fabrikam.com** 作為 XMPP 協力廠商網域名稱。此為必填項目。

8.  **描述**。描述是此特定組態的附註或其他識別資訊。此為選填項目。

9.  **其他網域**。其他網域為您 XMPP 協力廠商網域的一部分網域，應包含為允許之 XMPP 通訊的一部分。例如，如果主要網域為 **fabrikam.com**，則您會列出位於 fabrikam.com 下將經由 XMPP 通訊的所有其他網域。例如，您可以分別針對 fabrikam.com 的主要 XMPP 網域下的 Corporate XMPP 網域及 Information Technologies XMPP 網域輸入 **corp.fabrikam.com** 和 **it.fabrikam.com**。

10. **協力廠商類型**。**協力廠商類型**為必要設定，以下拉式功能表中的形式為您提供三個選項。您必須選擇下列其中一項，以描述和強制可新增哪些連絡人。您可以從下列項目中進行選取：
    
      - **同盟**。**同盟**協力廠商類型是 Lync Server 或 Office Communications Server 2007 R2 協力廠商部署之間信任的連線。
    
      - **公用已驗證**。**公用已驗證**協力廠商的使用時機是在將屬於提供者已驗證之部署一部分的連絡人新增至您使用者的連絡人清單時。邀請可以從 Lync 使用者進行傳送，或者 Lync 使用者可以接受來自協力廠商連絡人的邀請。
    
      - **公用未驗證**。**公用未驗證**關聯性意味著這兩個部署之間沒有已建立且可驗證的狀態。Lync 使用者必須邀請該連絡人的未驗證連絡人，才能將 Lync 使用者新增至連絡人清單。例如，雖然 Google GTalk 與 Lync Server 相關，但它不是一項公用已驗證的 XMPP 服務。除非有傳送自 Lync 使用者的明確邀請，否則 GTalk 使用者無法將 Lync 使用者新增為連絡人。

11. 關於資料流交涉與安全性方法傳輸層安全性 (TLS) 和軟體驗證及安全性階層 (SASL) 的附註：
    
    **XMPP Standards Foundation** (XSF) 和 **網際網路工程任務推動小組** (IETF) 會定義一組使用與管理 TLS 用戶端憑證、TLS 伺服器憑證及 SASL 機制的規則與標準。使用 TLS 和 SASL 是保護 XMPP 資料流安全的必要程序。從 XMPP Standards 文件 **XEP-0178**，「指定建議使用的通訊協定流程，將 SASL EXTERNAL 機制與 PKIX 憑證搭配使用，特別是在 XMPP 服務指出 TLS 為強制交涉時。」PKIX (如 XSF 文件中所述) 是指公用金鑰基礎結構，亦稱為 PKI。
    
    請參閱 XSF 文件 XEP-0178，以取得更多關於 XMPP 需求的詳細資訊。如需詳細資訊，請參閱＜XEP-0178：將 SASL EXTERNAL 與憑證搭配使用的最佳作法＞ <http://xmpp.org/extensions/xep-0178.html>。
    
    請參閱 IETF 文件＜Extensible Messaging and Presence Protocol (XMPP)：核心＞的第 5.0 節＜STARTTLS 交涉＞ <http://tools.ietf.org/html/rfc6120>。
    
      - **TLS 交涉**。定義 TLS 交涉規則。XMPP 服務可要求 TLS、將 TLS 設為選用，您也可以定義不支援 TLS。選擇 \[選用\] 可讓 XMPP 服務決定是否必須強制交涉。若要檢視 SASL、TLS 及回撥交涉的所有可能設定和詳細資料 (包含無效及未知錯誤設定)，請參閱＜[Lync Server 2013 中 XMPP 同盟夥伴的交涉設定](lync-server-2013-negotiation-settings-for-xmpp-federated-partners.md)＞。
        
           **需要**。XMPP 服務需要 TLS 交涉。
        
           **選擇性**。XMPP 服務指出必須交涉 TLS。
        
           **不支援**。XMPP 服務不支援 TLS。
    
      - **SASL 交涉** 。定義 SASL 交涉規則。XMPP 服務可以將 SASL 視為必要或選用，或者由您將 SASL 定義為不支援。選擇 \[選擇性\] 會將此需求留給協力廠商 XMPP 服務進行必須交涉的決定。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Hh202161.warning(OCS.15).gif" title="warning" alt="warning" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>SASL 要求 TLS。若要使用 SASL，TLS 必須是必要項目或選用項目。任何將 SASL 定義為必要或選用的設定都必須受到 TLS 支援。按一下 <strong>[認可]</strong> 以儲存您的變更時，如果您尚未將 TLS 設定為必要或選用，系統將會警告您，SASL 必須受到 TLS 支援，而您的變更將不會儲存。若要解決此錯誤，請將 TLS 設定為 <strong>[必要]</strong> 或 <strong>[選用]</strong> 。如果 SASL 的用法為選用且無法支援 TLS 交涉，則您必須將 SASL 交涉設定為 <strong>[不支援]</strong> 。利用 XMPP 服務來確認適用於 TLS 和 SASL 的正確交涉資料流必須是何種類型，或者將會發生服務中斷。</td>
        </tr>
        </tbody>
        </table>
        
           **必要**。XMPP 服務需要 SASL 交涉。
        
           **選擇性**。XMPP 服務指出必須交涉 SASL。
        
           **不支援**。XMPP 服務不支援 SASL。
    
      - **回撥交涉**。回撥交涉是由文件＜**XEP-220：伺服器回撥**＞[http://xmpp.org/extensions/xep-0220.htm](http://xmpp.org/extensions/xep-0220.html) 中的 XSF 所定義。伺服器回撥程序會使用網域名稱系統 (DNS) 和主伺服器，來確認要求是來自有效的 XMPP 協力廠商。若要執行此動作，原始伺服器會建立含有已產生回撥金鑰的特定類型訊息，並查閱 DNS 中的接收伺服器。原始伺服器會在 XML 資料流中將金鑰傳送給結果 DNS 查閱 (可能是接收伺服器)。透過 XML 資料流接收到金鑰時，接收伺服器不會回應原始伺服器，但會將該金鑰傳送到已知的主伺服器。主伺服器會確認金鑰是否有效。如果無效，接收伺服器便不會回應原始伺服器。如果金鑰有效，則接收伺服器會通知原始伺服器，身分識別與金鑰是有效的且可開始進行交談。
        
        **回撥交涉**有兩種有效狀態：
        
           **True**。如果必須接收來自原始伺服器的要求，則將 XMPP 伺服器設定為使用回撥交涉
        
           **False**。XMPP 伺服器不設定為使用回撥交涉；萬一從來源伺服器收到要求，將會忽略該要求

