---
title: Lync Server 2013：設定 Kerberos 驗證
TOCTitle: 設定 Kerberos 驗證
ms:assetid: dd8009ef-6265-4cc0-b2c7-e474cd1f4b09
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398976(v=OCS.15)
ms:contentKeyID: 49292540
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定 Kerberos 驗證

 

_**上次修改主題的時間：** 2013-02-21_

Lync Server 2013 支援 Web 服務的 NTLM 和 Kerberos 驗證。 Office Communications Server 2007 和 Office Communications Server 2007 R2 使用預設 RTCComponentService 和 RTCService 做為使用者帳戶來執行 Web 服務應用程式集區，讓服務主體名稱 (SPN) 可以指派給使用者帳戶並當做驗證主體。 Lync Server 使用 NetworkService 來執行 Web 服務，且不能指派 SPN 給 NetworkService。

為解決沒有 Active Directory 物件可保留 SPN 的問題，Lync Server 控制台 可以將電腦帳戶物件用於此用途。電腦帳戶物件可以保留 SPN，且不會受密碼到期問題影響，使用舊版中的使用者帳戶則會有此問題。

您會使用 Windows PowerShell Cmdlet 來設定電腦物件，以提供 Kerberos 驗證。

## 本章節內容

  - [在 Lync Server 2013 中啟用 Kerberos 驗證的先決條件](lync-server-2013-prerequisites-for-enabling-kerberos-authentication.md)

  - [在 Lync Server 2013 中建立 Kerberos 驗證帳戶](lync-server-2013-create-a-kerberos-authentication-account.md)

  - [在 Lync Server 2013 中將 Kerberos 驗證帳戶指派到網站](lync-server-2013-assign-a-kerberos-authentication-account-to-a-site.md)

  - [在 Lync Server 2013 中設定 Kerberos 驗證帳戶密碼](lync-server-2013-setting-up-kerberos-authentication-account-passwords.md)

  - [在 Lync Server 2013 中新增 Kerberos 驗證至其他站台](lync-server-2013-add-kerberos-authentication-to-other-sites.md)

  - [在 Lync Server 2013 中從網站移除 Kerberos 驗證](lync-server-2013-remove-kerberos-authentication-from-a-site.md)

  - [在 Lync Server 2013 中測試和報告 Kerberos 驗證的狀態和指派](lync-server-2013-testing-and-reporting-the-status-and-assignment-of-kerberos-authentication.md)

