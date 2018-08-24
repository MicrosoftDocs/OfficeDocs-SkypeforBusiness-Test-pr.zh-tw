---
title: Lync Server 2013：在 IIS 虛擬目錄上確認或設定驗證和憑證
TOCTitle: 在 IIS 虛擬目錄上確認或設定驗證和憑證
ms:assetid: 3ca90be0-1d64-447c-807a-3a2ee3bf625e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg429702(v=OCS.15)
ms:contentKeyID: 49290659
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中的 IIS 虛擬目錄上確認或設定驗證和憑證

 

_**上次修改主題的時間：** 2012-05-25_

請使用下列程序，在您的 Internet Information Services (IIS) 虛擬目錄上設定憑證，或者確認憑證已設定正確。在內部 Lync Server 集區，以及選用的 Director 或 Director 集區伺服器中每個執行 IIS 的伺服器上執行下列程序。

> [!NOTE]  
> 下列程序定義了要求組合憑證的程序，該憑證是用於 IIS 中所有目的 Lync Server Internal Web Site 及 External Web Site。 Lync Server 2010 推出一組 Lync Server 管理命令介面Windows PowerShell Cmdlet 以快速管理憑證要求、匯出及指派。程序中假設有內部部署的憑證授權單位 (CA) 可處理要求。如果針對 Lync Server 目的使用公用憑證，或 CA 需要離線要求，請參閱此主題中關於 –Output 參數詳細語法的資訊。 <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Request-CsCertificate">Request-CsCertificate</a>



## 設定 IIS 虛擬目錄上的驗證及憑證

1.  如要成功完成下列程序，必須以本機管理員身分登入 Web 服務安裝所在的電腦 ( 前端伺服器或 Director)。對於將向其要求憑證的憑證授權單位，您必須擁有該憑證授權單位的「讀取」 和「註冊」 權限。如果將設定並傳送離線憑證要求，則不需要對憑證授權單位的權限。

2.  按一下 **\[開始\]** ，選取 **\[所有程式\]** 、\[系統管理工具\] ，然後按一下 **\[Internet Information Services (IIS) 管理員\]** 。

3.  在 **\[Internet Information Services (IIS) 管理員\]** 中，選取 **\[伺服器名稱\]** 。在 **\[功能檢視\]** 中，選取 **\[伺服器憑證\]** ，按右鍵並選取 **\[開啟功能\]** 。
    
    > [!TIP]
    > 在 [伺服器憑證功能檢視] 中，如果有憑證指派給伺服器，將會在此顯示。如果有憑證符合 IIS 中 External Web Site 的要求，可以重複使用該憑證。要檢視憑證，在憑證按右鍵並選取 <strong>[檢視...]</strong> 。


4.  在為其要求憑證的 前端伺服器或 Director 上，按一下 **\[開始\]** ，選取 **\[所有程式\]** 、 **\[ Microsoft Lync Server 2013\]** ，然後按一下 **\[ Lync Server 管理命令介面\]** 。

5.  在 Lync Server 管理命令介面 中輸入：
    
        Get-CsCertificate
    
    輸出為目前在伺服器上電腦個人憑證存放區中的憑證清單。請注意：在組合憑證中 (亦即預設 Web 服務內部及 Web 服務外部使用相同的憑證)，「使用」屬性會填入 Default, WebServicesInternal 及 WebServicesExternal。每個「使用」類型也會有相同的「指紋」屬性。以下範例顯示 Get-CsCertificate 的輸出範例：
    
    ![目前 scert 狀態的 Get-CsCertificate 資訊](images/Gg429702.664f6326-6cd5-48e2-8235-fc3950ea43b4(OCS.15).jpg "目前 scert 狀態的 Get-CsCertificate 資訊")

6.  在 Lync Server 管理命令介面 中輸入：
    
        Request-CsCertificate -New -Type Default,WebServicesInternal,WebServicesExternal -CA <CA Server FQDN\CA Instance> -Verbose -DomainName "<FQDN entries to be added to the Subject Alternative Name>"
    
    完整命令將類似下列範例：
    
        Request-CsCertificate -New -Type Default,WebServicesInternal,WebServicesExternal -CA dc01.contoso.net\contoso-DC01-CA -Verbose -DomainName "LyncdiscoverInternal.Contoso.com,Lyncdiscover.Contoso.com"
    
    > [!TIP]
    > 依預設，Request-CsCertificate 會在主體名稱中填入伺服器或集區名稱，並且在主體替代名稱的項目中填入伺服器 FQDN、集區 FQDN、簡單 URL FQDN 以及內部與外部 Web 服務 FQDN。這是透過參考部署中的拓撲文件而成。如果缺少某個值，而且指定了 –Verbose 參數，將會通知您別名的計算值與實際值不同，但不會告知缺少哪些值，不過會提供您 Cmdlet 參考的整個計算值。可使用輸出中的計算別名稱串，重新要求會包含所有值的新憑證。
    
    ![使用 Request-CsCertifica 從 cert 要求輸出](images/Gg429702.9e59a657-fa75-4454-8fd3-57c81e829f7b(OCS.15).jpg "使用 Request-CsCertifica 從 cert 要求輸出")

7.  在 Lync Server 管理命令介面 中輸入：
    
        Set-CsCertificate -Type Default,WebServicesInternal,WebServicesExternal -Thumbprint <Thumbprint of certificate to use>
    
    完整命令將類似下列範例：
    
        Set-CsCertificate -Type Default,WebServicesInternal,WebServicesExternal -Thumbprint 466D9BB0E8B928B65AF38FA2D9F41E1B301ECE9D
    
    Set-CsCertificate Cmdlet 的輸出會顯示相同的憑證 (以憑證指紋識別) 已指派給 Default, WebServicesExternal 及 WebServicesInternal 使用。
    
    ![IIS WebExt 之 Set-CsCertificate 的輸出](images/Gg429702.dd451c9d-7b49-4408-8071-c868cb1e678c(OCS.15).jpg "IIS WebExt 之 Set-CsCertificate 的輸出")

## 確認或設定 IIS 虛擬目錄的驗證與憑證

1.  按一下 **\[開始\]** ，選取 **\[所有程式\]** 、\[系統管理工具\] ，然後按一下 **\[Internet Information Services (IIS) 管理員\]** 。

2.  在 **\[Internet Information Services (IIS) 管理員\]** 中，依序展開 **\[伺服器名稱\]** 和 **\[網站\]** 。

3.  用滑鼠右鍵按一下 **\[Lync Server External Web Site\]** ，然後按一下 **\[編輯繫結\]** 。

4.  確認 https 關聯至連接埠 4443，然後按一下 **\[https\]** 。

5.  選取 HTTPS 項目，按一下 **\[編輯\]** ，然後確認 Lync Server WebServicesExternalCertificate 繫結至此通訊協定。與來自 Set-CsCertificate Cmdlet 的指紋比較，確認預期的憑證已正確與 HTTPS 繫結關聯。

## 請參閱

#### 其他資源

[Get-CsCertificate](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsCertificate)  
[Set-CsCertificate](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsCertificate)

