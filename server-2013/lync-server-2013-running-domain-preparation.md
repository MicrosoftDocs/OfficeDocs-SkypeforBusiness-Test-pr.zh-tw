---
title: Lync Server 2013：執行網域準備
TOCTitle: 執行網域準備
ms:assetid: 95dab800-1f2c-4506-b36c-99986643b149
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398761(v=OCS.15)
ms:contentKeyID: 49291726
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 為 Lync Server 2013 執行網域準備

 

_**上次修改主題的時間：** 2013-04-16_

您可以使用安裝程式或 Lync Server 管理命令介面 Cmdlet 來準備網域。準備網域的 Cmdlet 為 **Enable-CsAdDomain**。

網域準備是為 Lync Server 2013 準備 Active Directory 網域服務 的最後一個步驟。

## 若要使用安裝程式來準備網域

1.  以 Domain Admins 群組成員的身分登入網域中的任何伺服器。

2.  從 Lync Server 2013 安裝資料夾或媒體，執行 Setup.exe 以啟動 Lync Server 部署精靈。

3.  按一下 **\[準備 Active Directory\]** ，然後等候決定部署狀態。

4.  在 **\[步驟 5：準備目前的網域\]** ，按一下 **\[執行\]** 。

5.  按一下 **\[準備網域\]** 頁面中的 **\[下一步\]** 。

6.  在 **\[執行命令\]** 頁面上，尋找 **\[工作狀態：完成\]** ，然後按一下 **\[檢視記錄檔\]** 。

7.  展開 **\[動作\]** 欄之下的 **\[網域準備\]** ，並尋找在每項工作結尾的 **\<成功\>** 執行結果，確認已順利完成網域準備，關閉記錄檔，然後按一下 \[完成\] 。

8.  等候 Active Directory 複寫完成，或是強制複寫到樹系根網域控制站 \[Active Directory 站台及服務\] 嵌入式管理單元中列出的所有網域控制站。

## 使用 Cmdlet 準備網域

1.  以 Domain Admins 群組成員的身分登入網域中的任何伺服器。

2.  如下所述安裝 Lync Server 核心元件：
    
    1.  從 Lync Server 2013 安裝資料夾或媒體，執行 Setup.exe 以啟動 Lync Server 部署精靈。
    
    2.  如果系統提示您安裝 Microsoft Visual C++ 可轉散發套件，請按一下 \[是\] 。
    
    3.  Lync Server 2013 安裝程式對話方塊會提示您指定安裝 Lync Server 檔案的位置。請選擇預設位置或 \[瀏覽\] 至您想要的位置，然後按一下 \[安裝\] 。
    
    4.  在 \[授權合約\] 頁面上，勾選 \[我接受授權合約中的條款\] ，然後按一下 \[確定\] 。安裝程式隨即安裝 Lync Server 2013 核心元件。

3.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

4.  執行：
    
        Enable-CsAdDomain [-Domain <DomainFQDN>] 
    
    例如：
    
        Enable-CsAdDomain -Domain domain1.contoso.net 
    
    如果不指定 Domain 參數，預設值為本機網域。

5.  確認網域準備工作順利完成。執行：
    
        Get-CsAdDomain [-Domain <Domain FQDN>] [-DomainController <Domain controller FQDN>] [-GlobalCatalog <Global catalog server FQDN>] [-GlobalSettingsDomainController <Domain controller FQDN where global settings are stored>] 
    
    例如：
    
        Get-CsAdDomain -Domain domain1.contoso.net -GlobalSettingsDomainController dc01.domain1.contoso.com
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>GlobalSettingsDomainController 參數可讓您指出全域設定的儲存位置。如果您的設定儲存在 System 容器 (在升級部署期間，當全域設定尚未移轉到 [設定] 容器時的常見現象)，請在 Active Directory 樹系的根目錄中定義網域控制站。如果全域設定位於 [設定] 容器中 (在全新部署或升級部署期間，當設定已經移轉至 Configuration 容器時的常見現象)，您可以在樹系中定義任何網域控制站。如果您未指定此參數，則 Cmdlet 會認為設定儲存在 [設定] 容器中，並參考 AD DS 中的任何網域控制站。</td>
    </tr>
    </tbody>
    </table>
    
    如果不指定 **Domain** 參數，預設值為本機網域。
    
    這個 Cmdlet 會在網域準備工作順利完成時，傳回值 **LC\_DOMAINSETTINGS\_STATE\_READY** 。

## 請參閱

#### 工作

[將 Cmdlet 用於 Lync Server 2013 的反向網域準備](lync-server-2013-using-cmdlets-to-reverse-domain-preparation.md)  

#### 其他資源

[針對 Lync Server 2013 準備網域](lync-server-2013-preparing-domains.md)

