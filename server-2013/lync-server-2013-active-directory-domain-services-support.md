---
title: Lync Server 2013：Active Directory 網域服務支援
TOCTitle: Active Directory 網域服務支援
ms:assetid: aeb62d5e-e424-473a-b795-9452150c98dd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412831(v=OCS.15)
ms:contentKeyID: 49291998
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的 Active Directory 網域服務支援

 

_**上次修改主題的時間：** 2013-11-07_

Lync Server 2013 會使用 中央管理存放區儲存伺服器和服務的設定資料，而不會如舊版中倚賴 Active Directory 網域服務 處理此資訊。 Lync Server 2013 仍然會將下列各項儲存在 AD DS 中：

  - **架構延伸**
    
      - 使用者物件延伸
    
      - Lync Server 2010 和 Office Communications Server 2007 R2 類別的延伸，是為了與之前支援的版本維持回溯相容性

  - **資料** (儲存在 Lync Server 2013 擴充架構和現有類別中)
    
      - 使用者 SIP URI 和其他使用者設定
    
      - 應用程式的連絡人物件 (例如 回應群組應用程式和 會議服務員應用程式)
    
      - 為了回溯相容性所發行的資料
    
      - 中央管理存放區的服務控制點 (SCP)
    
      - Kerberos 驗證帳戶 (選用的電腦物件)

本節描述 Lync Server 2013 的 AD DS 支援需求。如需關於拓撲支援的詳細資訊，請參閱支援文件中的 [Lync Server 2013 中支援的 Active Directory 拓撲](lync-server-2013-supported-active-directory-topologies.md)。

## 支援的網域控制站作業系統

Lync Server 2013 支援執行下列作業系統的網域控制站：

  - Windows Server 2012 R2 作業系統

  - Windows Server 2012 作業系統

  - Windows Server 2008 R2 作業系統

  - Windows Server 2008 作業系統

  - Windows Server 2008 Enterprise 32 位元

  - 32 位元或 64 位元版的 Window Server 2003 R2 作業系統

  - 32 位元或 64 位元版的 Windows Server 2003 作業系統

## 樹系和網域功能等級

您必須將 Lync Server 2013 部署所在的所有網域提升到 Windows Server 2012 R2、 Windows Server 2012、 Windows Server 2008 R2、 Windows Server 2008，或至少 Windows Server 2003 的網域功能等級。

Lync Server 2013 部署所在的所有樹系都必須提升到 Windows Server 2012 R2、 Windows Server 2012、 Windows Server 2008 R2、 Windows Server 2008，或至少 Windows Server 2003 的樹系功能等級。

## 支援唯讀網域控制站

Lync Server 2013 支援包含唯讀網域控制站或唯讀通用類別目錄伺服器的 Active Directory 網域服務 部署 (只要有可用的可寫入網域控制站即可)。

## 網域名稱

Lync Server 不支援單一標籤的網域。例如，根網域名稱為 **contoso.local** 的樹系是受支援的，名為 **local** 的根網域則不受支援。如需詳細資訊，請參閱 Microsoft 知識庫文章 300684＜為具有單一標籤 DNS 名稱之網域設定 Windows 的相關資訊＞，網址為 <http://go.microsoft.com/fwlink/?linkid=143752>。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lync Server 不支援重新命名的網域。如果您需要重新命名已部署 Lync Server 的網域，您必須先解除安裝 Lync Server，然後重新命名網域，接著重新安裝 Lync Server。</td>
</tr>
</tbody>
</table>


## 鎖定的 AD DS 環境

在鎖定的 AD DS 環境中，Users 及 Computer 物件經常會以停用權限繼承的方式置於特定的組織單位 (OU) 中，以保護系統管理委派的安全性，並允許使用群組原則物件 (GPO) 強制執行安全性原則。 Lync Server 2013 可以部署在鎖定的 Active Directory 環境中。如需關於在鎖定的環境中部署 Lync Server 所需項目的詳細資訊，請參閱部署文件中的 [在 Lync Server 2013 中準備鎖定的 Active Directory 網域服務](lync-server-2013-preparing-a-locked-down-active-directory-domain-services.md)。

