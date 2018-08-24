---
title: Lync Server 2013 中的主要安全性功能
TOCTitle: Lync Server 2013 中的主要安全性功能
ms:assetid: bf2a3b8f-73c6-47e1-8c9e-ca1dc1a502bf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn342829(v=OCS.15)
ms:contentKeyID: 56269150
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的主要安全性功能

 

_**上次修改主題的時間：** 2013-07-18_

Lync Server 2013 包含多項安全性功能，包括伺服器對伺服器的驗證、角色型存取控制，以及設定資料的集中式存放裝置。

本文提供 Lync Server 2013 安全性的高階概觀。

## Lync Server 2013 中的主要安全性功能

安全性是相當廣泛的主題，不僅是 Lync Server 2013 的所有功能，另外還有組成 Lync 生態系統的資料庫、服務以及硬體等，均是安全性所涉及的層面。本文概略說明 Lync Server 2013 中特別針對安全性所設計的部分功能。

## 規劃與設計工具

Lync Server 2013 提供兩項工具可加快 Lync Server 元件的規劃與設計並避免設定錯誤的可能性。

  - 「拓撲規劃工具」會將大部分的拓撲設計程序自動化。您可以將結果從規劃工具匯出至拓撲產生器；後者為安裝各個執行 Lync Server 2013 之伺服器的必要工具。

  - 「拓撲產生器」會將所有設定資訊儲存於中央管理存放區。

如需這類集區的詳細資訊，請參閱＜ [規劃 Lync Server 2013](lync-server-2013-planning.md)＞。

## 中央管理存放區

在 Lync Server 2013 中，有關伺服器與服務的設定資料會位於中央管理存放區。中央管理存放區提供在定義、設定、維護、管理、描述及運作 Lync Server 部署時所需要之穩固且結構描述化的資料儲存。中央管理存放區也會驗證資料以確保設定一致性。對於設定資料所做的任何變更，均是在中央管理存放區執行，可避免「不同步」的問題。

資料的唯讀複本會複寫到拓撲中的所有伺服器，包括 Edge Server 和 Survivable Branch Appliance。複寫預設由網路服務內容中所執行的服務所管理，可限制電腦上簡易使用者的權利與權限。

## 伺服器對伺服器的驗證

在 Lync Server 2013 中，伺服器之間可以使用開啟授權 (OAuth) 通訊協定設定驗證。例如，您可以設定 Lync Server 2013 以驗證執行 Exchange Server 2013 的伺服器。透過 OAuth 通訊協定，Lync 伺服器與 Exchange 伺服器可彼此信任，如此即可完美流暢地進行產品的整合。如需詳細資訊，請參閱＜[在 Lync Server 2013 中管理伺服器對伺服器驗證 (Oauth) 與夥伴應用程式](lync-server-2013-managing-server-to-server-authentication-oauth-and-partner-applications.md)＞。

## Windows PowerShell 型管理與 Web 型管理介面

Lync Server 2013 以 Windows PowerShell 命令列介面為基礎，提供功能強大的管理介面。介面包含可以用於管理安全性的 Cmdlet，而且預設會啟用 Windows PowerShell 安全性功能，讓使用者無法輕易地或在不知情的情況下執行指令碼。這表示此軟體預設會自動將安全性設在最高的程度，藉此減少攻擊的入侵管道。如需 Lync Server 2013 中 Windows PowerShell 管理支援的相關詳細資訊，請參閱＜[Lync Server 管理命令介面](lync-server-2013-lync-server-management-shell.md)＞。

## 角色型存取控制 (RBAC)

Microsoft Lync Server 2013 提供角色型存取控制 (RBAC)，可讓您委派系統管理工作，同時維護高標準的安全性。您可以利用 RBAC 遵循「最低權限」的原則，讓使用者只獲得其工作所需的系統管理權限。Lync Server 2013 提供建立新角色的功能以及修改既有角色的功能。如需詳細資訊，請參閱＜[在 Lync Server 2013 中規劃角色型存取控制](lync-server-2013-planning-for-role-based-access-control.md)＞。

## 網路位址轉譯 (NAT)

Lync Server 2013 並不支援在 Edge Server 的內部介面上使用網路位址轉譯 (NAT)，但支援將 Access Edge Service、Web Conferencing Edge Service 以及 A/V Edge Service 的外部介面置於針對單一與調整式合併 Edge Server 拓撲執行網路位址解析 (NAT) 的路由器或防火牆後面。硬體負載平衡器後方的多個 Edge Server 無法使用 NAT。如有多個 Edge Server 在其外部介面上使用 NAT，則需要網域名稱系統 (DNS) 負載平衡作業。使用 DNS 負載平衡可讓您減少 Edge Server 集區中各個 Edge Server 的公用 IP 位址數。如需詳細資訊，請參閱＜[在 Lync Server 2013 中規劃外部使用者存取](lync-server-2013-planning-for-external-user-access.md)＞。

> [!NOTE]  
> 若是您與部署 Microsoft Office Communications Server 2007 的企業建立同盟，並需要在企業和同盟企業之間使用音訊/視訊功能，則連接埠需求與所部署的舊版 Edge Server 相同。例如，在同盟夥伴將其 Edge Server 升級為 Lync Server 2013 之前，兩家企業皆必須開啟舊版所需的連接埠範圍。待同盟夥伴完成升級之後，即可根據新的設定重新檢視連接埠需求並予以減少。



## Edge Server 的簡化憑證

部署精靈可自動填入主體名稱 (SN) 與主體別名 (SAN)，藉此降低加入非必要或可能不安全之項目的機率。

## 高可信度電腦運算安全程式開發生命週期 (SDL)

Lync Server 2013 是根據 Microsoft 高可信度電腦運算安全程式開發生命週期 (SDL) 設計與開發，詳細說明位於：<http://go.microsoft.com/fwlink/?linkid=68761>。

  - **值得信任的設計**   建立更為安全之整合通訊系統的第一步，是設計威脅模型，並測試每一項功能是否如設計般地運作。此外，Microsoft 會在設計行為之外執行測試，藉此尋找由異常產品行為所引發的安全性弱點。編碼程序與實務中已加入了多項安全性相關的改良功能。建置時間工具會在程式碼簽入最終產品之前，偵測緩衝區溢位和其他可能的安全性威脅。當然，要針對所有未知的安全性威脅進行設計是天方夜譚。沒有任何系統能夠保證完全安全。然而，由於產品從開發之初便已決定要加入安全設計原則，因此 Lync Server 2013 在其基礎結構中整合了業界標準的安全性技術。

  - **值得信任的運作方式**   Lync Server 2013 中的網路通訊預設都會經過加密。由於所有伺服器均會使用憑證與 Kerberos 驗證、TLS、安全即時傳輸通訊協定 (SRTP)，以及其他業界標準的加密技術，包括 128 位元進階加密標準 (AES) 加密，因此幾乎網路上的所有 Lync Server 資料均已受到保護。此外，角色型存取控制可讓您部署執行 Lync Server 2013 的伺服器，如此每個伺服器角色將只會執行服務，並只具備伺服器角色所適用的服務相關權限。

  - **值得信任的部署**   所有 Lync Server 2013 文件皆會提供最佳做法與建議，協助您判斷及設定部署的最佳安全性層級，以及評估啟動非預設選項的風險。

