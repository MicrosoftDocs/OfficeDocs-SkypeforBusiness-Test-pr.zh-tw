---
title: Lync Server 2013：將 Cmdlet 用於反向網域準備
TOCTitle: 將 Cmdlet 用於反向網域準備
ms:assetid: 014dba5d-fcb3-44c9-9d63-ae0755276dac
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398071(v=OCS.15)
ms:contentKeyID: 49289895
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 將 Cmdlet 用於 Lync Server 2013 的反向網域準備

 

_**上次修改主題的時間：** 2012-10-29_

使用 **Disable-CsAdDomain** Cmdlet 來反轉網域準備步驟。

## 若要使用 Cmdlet 來反轉網域準備

1.  以 Domain Admins 群組成員的身分登入網域中的任何伺服器。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  執行：
    
        Disable-CsAdDomain [-Domain <Fqdn>] [-DomainController <Fqdn>] [-Force <SwitchParameter>] 
        [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] 
    
    例如：
    
        Disable-CsAdDomain -Domain domain1.contoso.net -GlobalSettingsDomainController dc01.domain1.contoso.net -Force
    
    如果存在 Force 參數，即使已啟動網域中的一或多部 前端伺服器或 A/V 會議伺服器，也會回復網域準備工作。如果不存在 Force 參數，且已啟動網域中的任何 前端伺服器或 A/V 會議伺服器，則會終止網域準備的回復。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>GlobalSettingsDomainController 參數可讓您指出全域設定的存放位置。如果您的設定存放在 System 容器 (在升級部署作業期間，當全域設定尚未移轉到 Configuration 容器時的常見現象)，請將網域控制站定義到 Active Directory 樹系根目錄中。如果全域設定位於 Configuration 容器中 (在全新部署或升級部署作業期間，當設定已經移轉至 Configuration 容器時的常見現象)，您可以在樹系中定義任何網域控制站。如果您未指定此參數，則 Cmdlet 會認為設定儲存在 [設定] 容器中，並參考 AD DS 中的任何網域控制站。</td>
    </tr>
    </tbody>
    </table>


## 請參閱

#### 工作

[為 Lync Server 2013 執行網域準備](lync-server-2013-running-domain-preparation.md)  

#### 其他資源

[針對 Lync Server 2013 準備網域](lync-server-2013-preparing-domains.md)

