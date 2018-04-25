---
title: Lync Server 2013：設定 Kerberos 驗證帳戶密碼
TOCTitle: 設定 Kerberos 驗證帳戶密碼
ms:assetid: b435f88e-4a77-4be7-b7e5-c17484303b74
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412870(v=OCS.15)
ms:contentKeyID: 49292060
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定 Kerberos 驗證帳戶密碼

 

_**上次修改主題的時間：** 2010-11-03_

為 Kerberos 驗證帳戶建立電腦物件之後，可以設定帳戶的密碼。若要在一部伺服器上設定 Kerberos 帳戶密碼，請執行 Windows PowerShell Cmdlet。您可以在您為 Kerberos 驗證建立的物件上設定密碼。密碼可設為已知的值，不過預設會使用隨機密碼。密碼會提供給所有使用帳戶的 Kerberos 驗證來源。您可使用 Windows PowerShell Cmdlet 來設定及管理 Kerberos 帳戶密碼。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Kerberos 帳戶物件是電腦物件，但針對參考的 Windows PowerShell Cmdlet 中的作業使用 UserAccount 參數。請注意，這不是一項錯誤，而是該 Cmdlet 在用於 Kerberos 帳戶建立和維護時的預定行為。</td>
</tr>
</tbody>
</table>


## 本章節內容

  - [在 Lync Server 2013 中於伺服器上設定 Kerberos 驗證帳戶密碼](lync-server-2013-set-a-kerberos-authentication-account-password-on-a-server.md)

  - [在 Lync Server 2013 中同步處理 Kerberos 驗證帳戶密碼至 IIS](lync-server-2013-synchronize-a-kerberos-authentication-account-password-to-iis.md)

