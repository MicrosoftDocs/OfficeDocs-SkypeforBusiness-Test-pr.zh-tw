---
title: 會議的移轉考量
TOCTitle: 會議的移轉考量
ms:assetid: a9807d58-99a3-4cff-b4c6-74950d106a2b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412800(v=OCS.15)
ms:contentKeyID: 61130827
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 會議的移轉考量

 

_**上次修改主題的時間：** 2014-02-10_

本節討論下列主題：

  - 對於 Microsoft Lync Server 2013 中會議的變更

  - 根據使用者的會議需求移轉使用者

  - 移轉現有會議與會議內容

  - Lync Server 2010 移轉期間的使用者經驗

  - Office Communications Server 2007 R2 移轉期間的使用者經驗

  - Microsoft Lync 2013 與舊版伺服器會議之間的相容性

## 對於 Lync Server 2013 中會議的變更

**Lync Server 2013 功能。**   Lync Server 2013 提供新會議功能，這些功能可在將使用者的帳戶移至 Lync Server 2013 且使用者使用 Lync 2013 用戶端登入之後使用。新功能在[Lync Server 2013 中的新會議功能](lync-server-2013-new-conferencing-features.md)與[Lync Server 2013 中的用戶端最新訊息](lync-server-2013-what-s-new-for-clients.md)中有所說明。

**會議 URL。**   如同在 Lync Server 2010 中一樣，所有在 Lync Server 2013 中新排程的會議都有 https:// 的 URL 首碼，而現有會議會與使用者帳戶一起移轉。但是，Lync Server 2013 並不支援 Office Communications Server 2007 R2 電話會議 (conf:// URL prefix) 或 Web 會議 (meet:// URL prefix)。如需詳細資訊，請參閱本主題稍後的＜從 Office Communications Server 2007 R2 移轉會議＞。

**用戶端支援。**   與 Lync Server 2010 不同，Lync Server 2013 並不支援 Office Communicator 用戶端的會議。您無法使用下列用戶端加入透過 Lync 2013 的線上會議增益集 排程的會議：

  - Office Communicator 2007 R2

  - Microsoft Office Communications Server 2007 R2 Attendant

  - Office Communicator 2007

  - Office Live Meeting 2007

在移轉期間，Office Communicator 2007 R2 使用者應使用 Lync Web App 2013 加入 Lync Server 2013 會議，直到其用戶端升級為止。請注意，Office Communicator 2007 R2 使用者可以繼續針對 Lync Server 2013，就目前狀態和 IM 功能使用他們現有的用戶端，但並不支援會議功能。


## 根據使用者的會議需求移轉使用者

**經常召開會議的會議召集人。**   請考慮及早在程序中移轉經常召開會議的會議召集人，這樣他們便可充分發揮新 Lync Server 2013 與 Lync 2013 功能，如[Lync Server 2013 中的新會議功能](lync-server-2013-new-conferencing-features.md)與[Lync Server 2013 中的用戶端最新訊息](lync-server-2013-what-s-new-for-clients.md)所述。

**Live Meeting 使用者。**   如果您從 Office Communications Server 2007 R2 移轉，而您有使用者需要 Live Meeting 特有之 Web 會議功能 (特別是對於大型會議及分組討論區的支援)，您有下列幾種選擇：

  - 貴公司如有提供 Live Meeting 服務，建議召集人使用這項服務。

  - 將召集人繼續保留在舊版的 Office Communications Server 上，以便其可以繼續排程伺服器版的 Live Meeting Web 會議。

## 移轉現有的會議與會議內容

## 從 Lync Server 2010 移轉會議

當您將使用者從 Lync Server 2010 移至 Lync Server 2013 時，下列資訊會隨使用者的帳戶移動：

  - 已由使用者排定的會議。這包含會議目錄及會議資料。

  - 使用者的個人識別碼 (PIN)。直到過期或使用者要求新 PIN 前，使用者目前的 PIN 都持續有效。

但是，下列使用者帳戶資訊不會移到新的伺服器：

  - 會議內容，例如 PowerPoint 簡報、白板內容與輪詢資料

若要移動已在會議中共用的內容，請使用 Move-CsUser Cmdlet 的 MoveMeetingContent 參數。如需有關使用此 Cmdlet 的詳細資訊，請參閱 Lync Server 2013 Cmdlet 文件中的 [Move-CsUser](move-csuser.md)。

## 從 Office Communications Server 2007 R2 移轉會議

Office Communications Server 2007 R2 會議為電話會議 (conf:// URL prefix) 或 Web 會議 (meet:// URL prefix)。Lync Server 2013 並不支援這些舊版的 conf:// 和 meet:// 會議，它們也不會隨使用者帳戶一起移轉。移轉之後，您應指示使用者更新他們已排定之任何線上會議的連結。他們可在開啟排定的會議邀請 (這會更新會議 URL) 並重新傳送邀請給參與者以安裝 Lync 2013 用戶端之後執行此動作。

## Lync Server 2010 移轉期間的使用者經驗

本節提供當從 Lync 2010 移轉時的使用者會議經驗摘要。如需有關 Lync Server 2013 用戶端如何能夠與之前用戶端及伺服器版本共存和互動的詳細資訊，請參閱[Lync 2013 中的用戶端互通性](lync-server-2013-client-interoperability-in-lync-2013.md)。

## 使用 Lync 2013 用戶端加入 Lync Server 2010 會議

在從 Lync Server 2010 移轉期間，當使用者使用 Lync 2013 用戶端加入 Lync Server 2010 會議時，可能會有一段共存的時間。這些使用者能夠存取 Lync 2013 用戶端功能，但有以下例外：

  - 在 **\[參與者\]** 管理選項中 (其可透過指向會議視窗中的人員圖示來存取)，**\[無會議 IM\]** 選項無法作用。

  - 「圖庫檢視」在視訊會議中無法作用。使用者只會看見目前發言者，不會看見所有發言者。在 **\[挑選版面配置\]** 選項的清單中，**\[圖庫檢視\]** 無法使用

  - 參與者清單預設會顯示在視訊會議中。

  - 以滑鼠右鍵按一下參與者清單中的使用者時，**\[鎖定視訊焦點\]** 與 **\[固定至圖庫\]** 參與者管理選項無法使用。

## Office Communications Server 2007 R2 移轉期間的使用者經驗

本節提供當在安裝 Lync 2013 之前與之後，從 Office Communications Server 2007 R2 移轉時的使用者會議經驗摘要。如需有關 Lync Server 2013 用戶端如何能夠與之前的用戶端與伺服器版本共存和互動的詳細資訊，請參閱[Lync 2013 中的用戶端互通性](lync-server-2013-client-interoperability-in-lync-2013.md)。

## 移轉使用者帳戶之後，安裝 Lync 2013 之前

在使用者移轉至 Lync Server 2013 伺服器之後，但安裝新用戶端之前，Office Communicator 2007 R2 使用者可以繼續針對 Lync Server 2013，就目前狀態和 IM 功能使用他們現有的用戶端，但並不支援會議功能。

## 移轉使用者帳戶之後，安裝 Lync 2013 之後

當移轉的使用者安裝 Lync 2013 時，也會安裝 Lync 2013 的線上會議增益集。這會產生下列效果：

  - 所有後續排定的會議會使用新會議格式，即使用 https:// 位址，而非舊有的 meet:// Live Meeting 位址。

  - 在 IT 管理的 Lync 2013 部署中，管理員可以選擇解除安裝用來排定 Live Meeting 伺服器與服務型會議的 Microsoft Office Outlook 會議增益集。但是，您可能也會有一些使用者需要繼續排定 Live Meeting 服務會議。在此情況下，您可以允許兩個增益集共存。

## 使用舊版用戶端之同盟組織的會議

如果會議遭到召集人鎖定，在同盟組織中使用 Microsoft Office Communicator 2007 的使用者無法加入組織中的 Lync Server 2013 會議。您必須在 Lync Server 2013 中重新排定這些會議，以便當同盟參與者使用新 https:// 會議 URL 加入會議時，他們能夠使用 Lync Web App。

