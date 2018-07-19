---
title: Lync Server 2013：建立宣告
TOCTitle: 建立宣告
ms:assetid: a6fd5922-fe46-41ba-94e3-c76b1101a31b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg412783(v=OCS.15)
ms:contentKeyID: 49291919
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中建立宣告

 

_**上次修改主題的時間：** 2012-11-01_

若要建立新的宣告，您必須執行下列步驟：

1.  若為音訊提示，請使用您偏好的音訊錄製應用程式錄製音訊檔。

2.  針對音訊提示執行 **Import-CsAnnouncementFile** Cmdlet，將音訊檔的內容匯入至檔案存放區。

3.  執行 **New-CsAnnouncement** Cmdlet 建立宣告並為其命名。執行此步驟可建立含有音訊提示、文字轉語音 (TTS) 提示或無提示的宣告。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ205025.tip(OCS.15).gif" title="tip" alt="tip" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您想要將來電轉接至特定目的地而不播放訊息，可能會希望建立沒有提示的宣告。</td>
    </tr>
    </tbody>
    </table>


4.  將新的宣告指派給未指派號碼表中的某個號碼範圍。

本主題描述如何匯入和建立宣告。如需關於在未指派號碼表中指派宣告的詳細資訊，請參閱＜ [在 Lync Server 2013 中設定未指派號碼表](lync-server-2013-configure-the-unassigned-number-table.md)＞。

## 若要建立新的宣告

1.  若為音訊提示，請建立音訊檔。

2.  以 RTCUniversalServerAdmins 群組成員身分或使用[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)中描述的必要使用者權限，登入裝有 Lync Server 管理命令介面的電腦。

3.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

4.  針對音訊提示，執行：
    
        Import-CsAnnouncementFile -Parent <service of the Application Server running the Announcement application> -FileName <name for file in File Store> -Content Byte [<contents of file in byte array>]

5.  執行：
    
        New-CsAnnouncement -Parent <service of Application Server running the Announcement application, in the form: service:ApplicationServer:<fqdn>> -Name <unique name to be used as destination in unassigned number table> [-AudioFilePrompt <FileName specified in Import-CsAnnouncementFile>] [-TextToSpeechPrompt <text string to be converted to speech>] [-Language <Language for playing the TTS prompt (required for PromptTts)>] [-TargetUri sip:SIPAddress for transferring caller after announcement]
    
    若要將通話轉接至語音信箱，請以下列格式輸入 SIPAddress：sip:username@domainname;opaque=app:voicemail (例如，sip:bob@contoso.com;opaque=app:voicemail)。若要將通話轉接至電話號碼，請以下列格式輸入 SIPAddress：ip:number@domainname;user=phone (例如，sip:+ 14255550121@contoso.com;user=phone)。
    
    例如，若要指定音訊提示：
    
        $a = Get-Content ".\PromptFile.wav" -ReadCount 0 -Encoding Byte
        Import-CsAnnouncementFile -Parent service:ApplicationServer:pool0@contoso.com -FileName "ChangedNumberMessage.wav" -Content $a
        New-CsAnnouncement -Parent service:ApplicationServer:pool0.contoso.com -Name "Number Changed Announcement" -AudioFilePrompt "ChangedNumberMessage.wav"
    
    例如，若要指定 TTS 提示：
    
        New-CsAnnouncement -Parent service:ApplicationServer:pool0.contoso.com -Name "Help Desk Announcement" -TextToSpeechPrompt "The Help Desk number has changed. Please dial 5550100." -Language "en-US"
    
    如需有關這些 Cmdlet 的詳細資訊，以及查看在 **TextToSpeechPrompt** 參數中使用的語言代碼清單，請參閱＜ [New-CsAnnouncement](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsAnnouncement)＞。

## 請參閱

#### 其他資源

[Import-CsAnnouncementFile](https://docs.microsoft.com/en-us/powershell/module/skype/Import-CsAnnouncementFile)  
[New-CsAnnouncement](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsAnnouncement)  
[在 Lync Server 2013 中設定未指派號碼表](lync-server-2013-configure-the-unassigned-number-table.md)

