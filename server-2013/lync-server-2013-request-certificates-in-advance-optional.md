---
title: Lync Server 2013：預先要求憑證 (選用)
TOCTitle: 預先要求憑證 (選用)
ms:assetid: 9d6d7de6-ff2a-46da-b1b7-a354c8e383e4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412733(v=OCS.15)
ms:contentKeyID: 49291825
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 針對 Lync Server 2013 預先要求憑證 (選用)

 

_**上次修改主題的時間：** 2013-02-21_

所有執行 Lync Server 2013 的內部伺服器都需要憑證，包括每部 Enterprise Edition前端伺服器、 Standard Edition 伺服器、 Director、 Edge Server 及獨立 中繼伺服器。雖然建議內部伺服器使用內部企業憑證授權單位 (CA)，但您也可以使用公用 CA。如需憑證需求和公用 CA 之用法的詳細資訊，請參閱規劃文件中的 [Lync Server 2013 中內部伺服器的憑證需求](lync-server-2013-certificate-requirements-for-internal-servers.md)。

Lync Server 2013 安裝程式中包含憑證精靈，可在部署期間簡化要求、指派及安裝憑證等工作。若要在安裝伺服器前要求憑證 (例如，藉此節省實際部署伺服器的時間)，可以使用安裝 Lync Server 2013 系統管理工具的電腦或組織定義的憑證要求程序提出要求，只要確定憑證可匯出且含有所有必要的主體別名即可。預先要求憑證是選用作業。如果您未預先要求憑證，必須在安裝每部需要憑證的伺服器時提出要求。

本部署文件提供在安裝程序中使用憑證精靈來要求憑證的程序，如本部署文件之 [在 Lync Server 2013 中設定伺服器憑證](lync-server-2013-configure-certificates-for-servers.md)、 [在 Lync Server 2013 中設定 Director 的憑證](lync-server-2013-configure-certificates-for-the-director.md)及 [在 Lync Server 2013 中安裝中繼伺服器的檔案](lync-server-2013-install-the-files-for-mediation-server.md)等小節所述。如果您預先要求憑證，必須適度修改上述各小節所記載的憑證部署程序才能匯入及指派憑證，而非在部署時要求憑證。

> [!NOTE]  
> Lync Server 2013 含有 SHA-256 憑證的支援，可供從執行 Windows Vista、 Windows Server 2008、 Windows Server 2008 R2 及 Windows 7 等作業系統和 Lync Phone Edition 的用戶端進行連線。為了支援使用 SHA-256 的外部存取，外部憑證由公用 CA 使用 SHA-256 發行。


