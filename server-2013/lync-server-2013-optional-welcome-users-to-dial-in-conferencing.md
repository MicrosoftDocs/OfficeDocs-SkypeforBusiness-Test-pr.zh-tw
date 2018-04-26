---
title: Lync Server 2013：(選用) 歡迎使用者使用電話撥入式會議
TOCTitle: (選用) 歡迎使用者使用電話撥入式會議
ms:assetid: caa4fd61-f506-4c09-bb5b-1aa260d7a720
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398846(v=OCS.15)
ms:contentKeyID: 49292305
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# (選用) 在 Lync Server 2013 中歡迎使用者使用電話撥入式會議

 

_**上次修改主題的時間：** 2012-09-30_

在您設定電話撥入式會議並測試以確認其運作正常時，您應該為使用者設定初始個人識別碼 (PIN)，並通知使用者功能的可用性，包括簡介指示，例如初始 PIN 和電話撥入式會議設定網頁的連結。這是選用步驟。一般而言，您會使用 **Set-CsClientPin** Cmdlet 來重設 PIN，但是如果您要傳送包含該資訊的電子郵件，可以在第一次使用本主題中的程序。如果您不要傳送該電子郵件，則可改用 **Set-CsClientPin**。

您可以使用 **Set-CsPinSendCAWelcomeMail** 指令碼來設定 PIN，並傳送歡迎電子郵件給單一使用者。根據預設，如果已經設定 PIN，則指令碼不會重設 PIN，但是您可以使用 **Force** 參數來強制重設 PIN。電子郵件訊息是使用 Simple Mail Transfer Protocol (SMTP) 來傳送。

您可以建立一個指令碼，使其反覆執行 **Set-CsPinSendCAWelcomeMail** 指令碼來設定 PIN，並傳送電子郵件給一組使用者。您可以修改電子郵件範本 (也就是 **CAWelcomeEmailTemplate.html** 檔案)，以便將更多連結新增至內部網路頁面或修改電子郵件文字。

## 若要設定初始 PIN 及傳送歡迎電子郵件

1.  以 RTCUniversalServerAdmins 群組成員的身分登入。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  在命令提示字元中執行下列命令：
    
        Set-CsPinSendCAWelcomeMail -UserUri <user identifier>
        -From <email address of sender> [-Subject <subject for email message>]
        [-UserEmailAddress <destination email address>]
        [-Cc <email address of recipients who receive copy of email>]
        [-Bcc <email address of recipients who receive blind copies>]
        [-TemplatePath <path for email template>]
        [-SmtpServer] <SMTP server name>]
        [-BodyAsPlainText] [-UseSsl]
        [-Pin <new numeric PIN>] [-Force] `
        [-Credential <SMTP server credentials used to send email with the specified From address>]
    
    **SmtpServer**   根據預設，指令碼會將保留的環境變數 **$PSEmailServer** 的值用於此參數。如果未設定 **$PSEmailServer** 變數，您必須指定此參數。
    
    **Credential**   根據預設，指令碼會使用目前使用者的認證。如果目前使用者沒有權限可代表指定之寄件者地址傳送電子郵件，您必須指定此參數。一般而言，如果您沒有將電子郵件地址指定為寄件者地址，請指定此參數。
    
    例如：
    
        Set-CsPinSendCAWelcomeMail -UserUri "bob@contoso.com"
        -From "marco@contoso.com"
    
    此範例會建立新的 PIN，然後由 Marco 傳送歡迎電子郵件給 Bob。它會使用來自預設範本的電子郵件文字，並以 HTML 格式建立電子郵件訊息。預設主旨為「歡迎使用電話撥入式會議」。
    
    另一個範例：
    
        Set-CsPinSendCAWelcomeMail -UserUri "bob@contoso.com"
        -From "marco@contoso.com" -Subject "Your new dial-in conferencing PIN"
        -Pin "383042650" -Force
        -Credential Admin@contoso.com -UseSsl
    
    此範例會強制將值為 "383042650" 的新 PIN 指定給 Bob (即使 Bob 已有現存的 PIN)，然後由 Marco 傳送歡迎電子郵件給 Bob。由於 Credential 參數已指定，因此會提示執行命令的人輸入密碼。電子郵件是使用安全通訊端層 (SSL) 所傳送。

