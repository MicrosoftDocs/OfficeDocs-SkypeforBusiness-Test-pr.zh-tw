---
title: 部署 Lync Windows 市集應用程式
TOCTitle: 部署 Lync Windows 市集應用程式
ms:assetid: 9e00aaf4-15f9-4356-9ed7-5a58a2bfa043
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ822971(v=OCS.15)
ms:contentKeyID: 52056198
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 部署 Lync Windows 市集應用程式

 

_**上次修改主題的時間：** 2013-12-03_

將 Lync Windows 市集應用程式提供給使用者之前，請確認您的部署符合 [Lync Windows 市集應用程式需求](lync-server-2013-lync-windows-store-app-requirements.md)。如需設定 Lync Server 2013 以支援 Lync Windows 市集應用程式的詳細資訊，請參閱 NextHop 部落格文章＜Lync Server 自動探索與 Lync Windows 市集應用程式＞：[http://go.microsoft.com/fwlink/?LinkId=271966](http://go.microsoft.com/fwlink/?linkid=271966) (英文)。在正確設定您的伺服器環境之後，即可引導使用者透過 Windows 市集搜尋 "Lync" 以下載 Lync 應用程式。

## 啟用 Lync Windows 市集應用程式的多重要素驗證

Lync Server 2013 的累計更新：2013 年 6 月新增對於 Lync Windows 市集應用程式用戶端的多重要素驗證支援。除了使用者名稱與密碼外，您可以要求其他驗證方式 (例如智慧卡或 PIN) 以在外部使用者登入 Lync 會議時進行驗證。若要啟用多重要素驗證，請在 Lync Server 2013 中部署 Active Directory Federation Service (AD FS) 同盟伺服器並啟用被動式驗證。AD FS 設定完成後，嘗試加入 Lync 會議的外部使用者將會看到 AD FS 多重要素驗證網頁，不僅包含使用者名稱與密碼問題，另外還有您所設定的任何額外驗證方法。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>以下為設定 AD FS 以進行 Lync Windows 市集應用程式的多重要素驗證時所要考量的重要事項：
<ul>
<li><p>至少要有 Lync Server 2013 搭配 Lync Server 2013 的累計更新：2013 年 6 月。Lync 2013 桌面用戶端並不需要 Lync Server 2013 的累計更新：2013 年 6 月，所以被動式驗證可能會因為 Lync 2013 用戶端能夠進行驗證而呈現正常運作的狀態。然而，Lync Windows 市集應用程式用戶端的驗證程序將無法完成，且畫面不會出現任何通知或錯誤訊息。</p></li>
<li><p>伺服器必須將被動式驗證設為唯一提供的驗證類型。</p></li>
<li><p>若您使用硬體負載平衡器，請在負載平衡器上啟用 Cookie 持續性，這樣來自 Lync Windows 市集應用程式 用戶端的所有要求才能由相同的前端伺服器處理。</p></li>
<li><p>當您在 Lync Server 與 AD FS 伺服器之間建立信賴憑證者信任時，請指定長度足夠的 Token 檔案，以擴展您 Lync 會議的長度上限。一般來說，240 分鐘的 Token 檔案即足夠。</p></li>
</ul></td>
</tr>
</tbody>
</table>


**設定多重因素驗證**

1.  安裝 AD FS 同盟伺服器角色。如需詳細資訊，請參閱 Active Directory Federation Services 2.0 部署指南：<http://go.microsoft.com/fwlink/p/?linkid=267511> (英文)。

2.  建立 AD FS 憑證。如需詳細資訊，請參閱與單一登入主題搭配使用之規劃與部署 AD FS 的＜同盟伺服器憑證＞一節，網址為 [http://go.microsoft.com/fwlink/?linkid=285376\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=285376%26clcid=0x404)。

3.  從 Windows PowerShell 命令列介面中，執行下列命令：
    
        add-pssnapin Microsoft.Adfs.powershell

4.  執行下列命令來建立合作關係：
    
        Add-ADFSRelyingPartyTrust -Name ContosoApp -MetadataURL https://lyncpool.contoso.com/passiveauth/federationmetadata/2007-06/federationmetadata.xml

5.  設定下列信賴憑證者規則：
    
        $IssuanceAuthorizationRules = '@RuleTemplate = "AllowAllAuthzRule" => issue(Type = "http://schemas.contoso.com/authorization/claims/permit", Value = "true");'$IssuanceTransformRules = '@RuleTemplate = "PassThroughClaims" @RuleName = "Sid" c:[Type == "http://schemas.contoso.com/ws/2008/06/identity/claims/primarysid"]=> issue(claim = c);'
    
        Set-ADFSRelyingPartyTrust -TargetName ContosoApp -IssuanceAuthorizationRules $IssuanceAuthorizationRules -IssuanceTransformRules $IssuanceTransformRules
    
        Set-CsWebServiceConfiguration -UseWsFedPassiveAuth $true -WsFedPassiveMetadataUri https://dc.contoso.com/federationmetadata/2007-06/federationmetadata.xml

## 可能會造成無法登入的已知問題

## 執行 Lync Windows 市集應用程式的裝置並未正確設定日期與時間

裝置的時間設定必須與伺服器的時間設定同步。對於 Microsoft Surface 等裝置以及其他未加入網域的 Windows RT 裝置來說，這點尤其重要。若要將這些裝置的時間設為自動從時間伺服器擷取，請在裝置上以較高權限透過命令提示字元執行下列命令：

    w32tm /resync

## Lync Windows 市集應用程式無法存取 Lync 伺服器或服務

Lync Windows 市集應用程式 可能無法透過沒有向 Windows 8 登錄為實體裝置的網路介面卡 (例如 4G LTE USB 數據機) 存取 Lync Server 或服務。即使桌面應用程式與瀏覽器能夠存取其他伺服器和網站，Lync Windows 市集應用程式仍可能會有此問題。

## Lync Windows 市集應用程式無法以 Lync Server 2010 與 Office Communications Server 2007 R2 Edge Server 登入

若是您的拓撲包含 Lync Server 2010 搭配 Office Communications Server 2007 R2 Edge Server，您將需要執行在 Lync Server 2010 的累計更新：2013 年 7 月中所提供的更新版拓撲產生器。舊版的拓撲產生器並不會建立與 Office Communications Server 2007 Edge Server 的所需對應，因此 Lync Windows 市集應用程式用戶端無法登入。以下為必要步驟：

1.  在 Lync Server 2010 集區與 Lync Server 2010 Director 上安裝 Lync Server 2010 的累計更新：2013 年 7 月。

2.  若要更新 Lync 自動探索設定以表示外部 SIP 進入點為 Edge 伺服器位址，請執行下列操作：
    
    1.  開啟 Lync Server 管理命令介面。
    
    2.  執行下列命令：
        
            Set-CsAutodiscoverConfiguration -ExternalSipClientAccessFqdn <FQDN of server used for external client access> -ExternalSipClientAccessPort 443

## Lync Windows 市集應用程式因憑證名稱驗證失敗而無法登入

使用者若未執行最新版 Lync Windows 市集應用程式，Office 365 可能會發生登入的問題。這個問題通常發生於使用多個網域 (例如當 SIP URI 是 **userA@domainZ.com** 但 Edge Server 是 **sip.domainX.com**) 的時候。如要修正問題，使用者應安裝最新版的 Lync Windows 市集應用程式 (也需要有 Windows 8.1)。

## 使用 Lync Windows 市集應用程式記錄以疑難排解問題

您可以利用裝置所建立的記錄來疑難排解問題。記錄儲存於下列資料夾：

%LocalAppData%\\Packages\\Microsoft.LyncMX\_8wekyb3d8bbwe\\LocalState\\Tracing

取得使用者的記錄之前，請確認記錄功能為開啟狀態，然後要求使用者儲存記錄，如此儲存於記憶體中的所有資訊也會儲存至硬碟的檔案中。

**若要開啟記錄**

1.  開啟裝置上的 Lync Windows 市集應用程式。

2.  從畫面右側撥動。如果您要使用滑鼠，請將滑鼠指向畫面右上角，再將滑鼠指標往畫面下方移動。

3.  依序選取 \[設定\] 與 \[選項\]，然後將 \[診斷記錄\] 設為 \[開啟\]。

4.  若是先前關閉 \[診斷記錄\]，您必須重新啟動 Lync。若要重新啟動 Lync，請執行下列其中一項操作：
    
      - 重新啟動裝置。
    
      - 結束 Lync 工作並再次啟動應用程式。若要結束工作，請開啟 \[Windows 工作管理員\]，選取 \[Lync\]，然後點選 \[結束工作\]。若是 Lync 並未列出，請點選 \[其他詳細資料\] 並在 \[背景處理程序\] 下搜尋 Lync 。

**若要儲存記錄**

1.  開啟裝置上的 Lync Windows 市集應用程式。

2.  嘗試登入。

3.  從畫面右側撥動。如果您要使用滑鼠，請將滑鼠指向畫面右上角，再將滑鼠指標往畫面下方移動。

4.  依序選取 \[設定\] 與 \[關於\]，然後選取 \[儲存記錄\]。

