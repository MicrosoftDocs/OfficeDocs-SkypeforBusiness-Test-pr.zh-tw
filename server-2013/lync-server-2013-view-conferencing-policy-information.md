---
title: 檢視會議原則資訊
TOCTitle: 檢視會議原則資訊
ms:assetid: e99fdc4d-926a-4e36-ac99-ab5035568847
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721918(v=OCS.15)
ms:contentKeyID: 49890361
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 檢視會議原則資訊

 

_**上次修改主題的時間：** 2013-02-23_

在 Lync Server 2013 控制台中，您使用會議原則來控制會議在部署中實作的方法，包含下列會議原則：

  - 部署 Lync Server 2013 時由預設建立的全域原則。

  - 您可建立並用於指定 會議如何為特定網站或使用者實作的選用網站層級與使用者層級原則。

## 檢視會議原則設定

1.  使用指派給 CsUserAdministrator 角色或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入管理 URL 以開啟 Lync Server 控制台。如需可用於啟動 Lync Server 控制台的不同方法的詳細資料，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左導覽列中，依序按一下 \[會議\]、\[會議設定\]。

4.  在 \[會議原則\] 頁面上，按兩下您想檢視的會議原則。

5.  在 \[編輯檔案篩選\] 中，選取 \[顯示詳細資料…\] 核取方塊。
    
    **編輯會議原則：\<原則\>** 開啟即會顯示所選原則的設定。有關設置設定的詳細資訊，請參閱＜[在 Lync Server 2013 中建立或修改會議原則](lync-server-2013-create-or-modify-a-conferencing-policy.md)＞。

## 使用 Lync Server PowerShell Cmdlet 檢視會議原則

會議原則也可透過 Lync Server PowerShell 與 Grant-CsPersistentChatPolicy Cmdlet 檢視。此 Cmdlet 可從 Lync Server 2013 管理命令介面或是 Windows PowerShell 的遠端工作階段執行。如需使用遠端 Windows PowerShell 連線至 Lync Server 的詳細資料，請參閱 Lync Server Windows PowerShell 部落格的＜快速入門：使用遠端 PowerShell 管理 Microsoft Lync Server 2010＞(英文) 一文，網址為：[http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876)。

## 檢視會議原則

  - 要檢視所有會議原則相關資訊，請在 Lync Server 管理命令介面輸入下列命令，然後按下 ENTER：
    
        Get-CsConferencingPolicy
    
    這樣將回傳類似下列的資訊：
    
        Identity                                  : Global
        AllowIPAudio                              : True
        AllowIPVideo                              : True
        AllowMultiView                            : True
        Description                               :
        AllowParticipantControl                   : True
        AllowAnnotations                          : True
        DisablePowerPointAnnotations              : False
        AllowUserToScheduleMeetingsWithAppSharing : True
        AllowNonEnterpriseVoiceUsersToDialOut     : False
        AllowAnonymousUsersToDialOut              : False
        AllowAnonymousParticipantsInMeetings      : True
        AllowExternalUsersToSaveContent           : True
        AllowExternalUserControl                  : False
        AllowExternalUsersToRecordMeeting         : False
        AllowPolls                                : True
        AllowSharedNotes                          : True
        EnableDialInConferencing                  : True
        EnableAppDesktopSharing                   : Desktop
        AllowConferenceRecording                  : False
        EnableP2PRecording                        : False
        EnableFileTransfer                        : True
        EnableP2PFileTransfer                     : True
        EnableP2PVideo                            : True
        AllowLargeMeetings                        : False
        EnableDataCollaboration                   : True
        MaxVideoConferenceResolution              : VGA
        MaxMeetingSize                            : 250
        AudioBitRateKb                            : 200
        VideoBitRateKb                            : 50000
        AppSharingBitRateKb                       : 50000
        FileTransferBitRateKb                     : 50000
        TotalReceiveVideoBitRateKb                : 6000
        EnableMultiViewJoin                       : True

如需詳細資訊，請參閱＜[Get-CsConferencingPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsConferencingPolicy)＞Cmdlet 的說明主題。

