---
title: Lync Server 2013 的使用者和用戶端驗證
TOCTitle: Lync Server 2013 的使用者和用戶端驗證
ms:assetid: 77f4b62a-f75c-424d-8f02-a6519090015d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn481132(v=OCS.15)
ms:contentKeyID: 59679126
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 的使用者和用戶端驗證

 

_**上次修改主題的時間：** 2013-11-11_

「信用的使用者」即是其認證已在 Microsoft Lync Server 2013 中通過信任的伺服器驗證的使用者。此伺服器通常是 Standard Edition 伺服器、Enterprise Edition前端伺服器 或 Director。Lync Server 2013 會將 Active Directory 網域服務 作為單一信任的後端使用者認證存放庫。

驗證是將使用者認證佈建到受信任伺服器的歷程。Lync Server 2013 會根據使用者的狀態和位置，使用下列幾種驗證通訊協定。

  - **MIT Kerberos 第 5 版安全性通訊協定**：針對有 Active Directory 憑證的內部使用者。Kerberos 要求能連至 Active Directory 網域服務 的用戶端連線，因此無法用來驗證企業防火牆之外的用戶端。

  - **NTLM 通訊協定**：針對有 Active Directory 認證且從企業防火牆外的端點連線的使用者。Access Edge Service 會將登入要求傳送至 Director (若有的話) 或是 前端伺服器 進行驗證。Access Edge Service 本身不執行驗證。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>NTLM 通訊協定所提供的攻擊防護較 Kerberos 弱，因此部分組織會盡量少用 NTLM。因此，Lync Server 2013 的存取權可能會限制為內部用戶端，或是透過 VPN 或 DirectAccess 連線的用戶端。</td>
    </tr>
    </tbody>
    </table>


  - **摘要式通訊協定**：針對所謂的匿名使用者。匿名使用者是沒有經認可 Active Directory 認證、但受邀參加內部會議且擁有有效的會議金鑰的外部使用者。摘要式驗證並非用於其他的用戶端互動。

Lync Server 2013 驗證有兩個階段：

1.  用戶端和伺服器之間會建立安全性關聯。

2.  用戶端和伺服器會使用現有的安全性關聯，簽署所傳送的訊息，並驗證接收的訊息。伺服器啟用驗證時，並不會接受來自用戶端的任何未驗證訊息。

使用者信任是附加於每個使用者發出的訊息中，而不是附加於使用者的識別證明上。伺服器會檢查每個訊息，看看是否具有有效的使用者憑證。如果使用者憑證有效，不但接收訊息的第一個伺服器不會驗證訊息，受信任伺服器 Cloud 中的所有伺服器也都不會驗證訊息。

具有同盟夥伴所發出之有效認證的使用者會受到信任，但是可能會選擇性地受到其他限制，而無法享有與內部使用者相同的完整權限。

ICE 和 TURN 通訊協定也會使用 IETF TURN RFC 中所述的摘要式挑戰。

用戶端憑證提供使用者另一種進行 Lync Server 2013 驗證的方法。使用者不必提供使用者名稱和密碼，而是擁有解析密碼編譯挑戰所需之憑證的相對應憑證和私密金鑰。此憑證必須具有可識別使用者身分的主體名稱或主體別名，並且必須是由執行 Lync Server 2013 之伺服器信任的根 CA 發行、在憑證的效期內，並且未經撤銷)。若要進行驗證，使用者只需輸入個人識別碼 (PIN)。對於電話和執行 Microsoft Lync 2013 Phone Edition 的其他裝置而言，因為難以輸入使用者名稱及/或密碼，因此憑證顯得特別實用。

