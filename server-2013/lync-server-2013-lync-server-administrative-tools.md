---
title: Lync Server 2013：Lync Server 系統管理工具
TOCTitle: Lync Server 系統管理工具
ms:assetid: 9b006f93-4f3d-461d-89b8-e80a34fdb3c5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg195756(v=OCS.15)
ms:contentKeyID: 49291795
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 系統管理工具

 

_**上次修改主題的時間：** 2013-02-21_

本主題說明 Lync Server 2013 的系統管理工具。

根據預設值，這些系統管理工具會安裝到每一部 Lync Server 伺服器。另外，您可以在其他電腦上安裝系統管理工具，例如專用的系統管理主控台。如需系統管理工具的安裝程序，請參閱＜ [安裝 Lync Server 2013 系統管理工具](lync-server-2013-install-lync-server-administrative-tools.md)＞。如需如何開啟工具來執行管理工作的程序，請參閱＜ [開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)＞。

安裝或使用 Lync Server 系統管理工具之前，請先仔細閱讀基礎結構、作業系統、軟體以及系統管理員權限需求。如需基礎結構需求的詳細資訊，請參閱＜ [Lync Server 2013 中的系統管理工具基礎結構需求](lync-server-2013-administrative-tools-infrastructure-requirements.md)。如需安裝 Lync Server 系統管理工具的作業系統和軟體需求的詳細資訊，請參閱＜ [Lync Server 2013 中的伺服器及工具作業系統支援](lync-server-2013-server-and-tools-operating-system-support.md)＞、＜ [Lync Server 2013 的其他軟體需求](lync-server-2013-additional-software-requirements.md)＞及＜ [Lync Server 2013 中的其他伺服器支援和需求](lync-server-2013-additional-server-support-and-requirements.md)＞。＜ [設定和管理 Lync Server 2013 所需的系統管理員權限](lync-server-2013-administrator-rights-and-permissions-required-for-setup-and-administration.md)＞提供安裝及使用工具時所需的使用者權利和權限描述。

系統管理工具包含下列工具：

  - **Lync Server 部署精靈**   用來部署 Lync Server 以及安裝所有系統管理工具。

  - **Lync Server拓撲產生器**   用來定義部署的元件。

  - **Lync Server 控制台**   用於使用網頁介面持續管理您的部署。

  - **Lync Server 管理命令介面**   用於使用命令列持續管理您的部署。

  - **Lync Server 記錄工具**   用來疑難排解部署的問題。

  - **集中記錄服務**   收集來自一部電腦、集區、網站或全域的記錄檔和追蹤檔案。選取並定義包含提供者、旗標和追蹤層級的案例。透過文字工具或 Snooper.exe 等工具來收集、彙總與顯示記錄。

您可以主要使用 拓撲產生器和 Lync Server 控制台管理自己的部署。

## 部署精靈

您必須使用安裝媒體中包含的 Lync Server 部署精靈，將所有系統管理工具安裝至您尚未安裝 Lync Server 的電腦上。安裝系統管理工具的過程中， Lync Server 部署精靈會和其他工具一起安裝在本機中，之後您可以使用它來安裝其他元件的檔案，或者將您不想放到電腦上的元件檔案移除。

如需關於如何首次從 Lync Server 安裝媒體執行 Lync Server 部署精靈的詳細資訊，請參閱＜ [安裝 Lync Server 2013 系統管理工具](lync-server-2013-install-lync-server-administrative-tools.md)＞。

## 拓撲產生器

如需使用 拓撲產生器可以執行的部署工作詳細資訊，請參閱每個伺服器角色的部署文件。

## Lync Server 控制台

您可以使用 Lync Server 2013 控制台執行管理和維護 Lync Server 2013 所需的大部分系統管理工作。除了組織中的使用者、用戶端及裝置之外， Lync Server 控制台提供您圖形化使用者介面 (GUI) 以管理執行 Lync Server 之伺服器的組態。 Lync Server 管理命令介面 使用 Lync Server 控制台作為執行 Lync Server 組態的基礎機制。

Lync Server 控制台會自動安裝於每一部 Lync Server 前端伺服器或 Standard Edition Server。在這一版中，您可以遠端方式管理 Edge Server。您也可以在其他電腦上安裝 Lync Server 控制台，例如想利用來集中管理 Lync Server 的管理主控台。如需詳細資訊，請參閱＜ [安裝 Lync Server 2013 系統管理工具](lync-server-2013-install-lync-server-administrative-tools.md)＞。

> [!IMPORTANT]  
> <ul>
> <li><p>若要使用 Lync Server 控制台來進行設定，您必須使用已指派給 CsAdministrator 角色的帳戶進行登入。 如需 Lync Server 2013 中可用的預先定義管理角色的詳細資料，請參閱<a href="lync-server-2013-planning-for-role-based-access-control.md">在 Lync Server 2013 中規劃角色型存取控制</a>。</p></li>
> <li><p>若要使用 Lync Server 控制台進行設定，您也必須使用最低螢幕解析度 1024 x 768 的電腦。</p></li>
> </ul>


## Lync Server 管理命令介面

在 Lync Server 中， Lync Server 管理命令介面提供新的支配和管理方法。 Lync Server 管理命令介面是一種功能強大的管理介面，建在 Windows PowerShell 命令列介面上，包含各式各樣 Lync Server 專用的 Cmdlet。使用 Lync Server 管理命令介面，您可以獲得豐富的設定和自動控制項。 拓撲產生器和 Lync Server 控制台都實作這些 Cmdlet 的子集，以便支援 Lync Server 的管理。 Lync Server 管理命令介面包含所有 Lync Server 管理工作所需的 Cmdlet，而且您可以個別使用這些 Cmdlet 管理自己的部署。如需詳細資訊，請參閱每個 Cmdlet 的 [Lync Server 管理命令介面](lync-server-2013-lync-server-management-shell.md)文件或命令列說明。

## 記錄工具

Lync Server 記錄工具可以在產品執行時，從產品擷取記錄和追蹤資訊，進而協助進行疑難排解。您可以使用這個工具，在任何 Lync Server 伺服器角色上執行偵錯工作階段。如需記錄工具的詳細資訊，請參閱 TechNet Library 的＜Lync Server 2010 記錄工具＞文件，網址為 <http://go.microsoft.com/fwlink/?linkid=199265>。

> [!IMPORTANT]  
> 在所有情況下的各種 Lync Server 記錄工具之間的所有記錄集合建議使用 集中記錄服務。 Lync Server 記錄工具仍會正常運作，但如果 集中記錄服務正在執行中，則該工具會干擾或大部分呈現無效。您應該僅使用 集中記錄服務或 Lync Server 記錄工具，但絕對不要同時使用兩種工具。如需 集中記錄服務以及為何應該單獨使用的詳細資訊，請參閱＜ <a href="lync-server-2013-using-the-centralized-logging-service.md">使用集中式記錄服務</a>＞。



## 本節內容

  - [Lync Server 2013 中的系統管理工具基礎結構需求](lync-server-2013-administrative-tools-infrastructure-requirements.md)

  - [Lync Server 2013 中的伺服器及工具作業系統支援](lync-server-2013-server-and-tools-operating-system-support.md)

  - [Lync Server 2013 中的系統管理工具軟體需求](lync-server-2013-administrative-tools-software-requirements.md)

  - [設定和管理 Lync Server 2013 所需的系統管理員權限](lync-server-2013-administrator-rights-and-permissions-required-for-setup-and-administration.md)

  - [在 Lync Server 2013 中發行拓撲的需求](lync-server-2013-requirements-to-publish-a-topology.md)

  - [安裝 Lync Server 2013 系統管理工具](lync-server-2013-install-lync-server-administrative-tools.md)

  - [開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)

  - [疑難排解 Lync Server 2013 控制台](lync-server-2013-troubleshooting-lync-server-2013-control-panel.md)

  - [使用集中式記錄服務](lync-server-2013-using-the-centralized-logging-service.md)

## 請參閱

#### 其他資源

[Lync Server 管理命令介面](lync-server-2013-lync-server-management-shell.md)

