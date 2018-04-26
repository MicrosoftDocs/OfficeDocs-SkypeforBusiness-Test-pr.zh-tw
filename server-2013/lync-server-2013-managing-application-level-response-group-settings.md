---
title: 在 Lync Server 2013 中管理應用程式層級回應群組設定
TOCTitle: 在 Lync Server 2013 中管理應用程式層級回應群組設定
ms:assetid: aab749a1-fa2d-4ce8-a6c6-ebcfa37ce02a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ721843(v=OCS.15)
ms:contentKeyID: 49890253
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中管理應用程式層級回應群組設定

 

_**上次修改主題的時間：** 2012-11-01_

回應群組應用程式的應用程式層級設定包含預設等候音樂組態、預設等候音樂音訊檔、代理人回電寬限期及通話內容組態。您可以為每一個集區只定義一組應用程式層級設定。若要檢視應用程式層級設定，請使用 **Get-CsRgsConfiguration** Cmdlet。若要修改應用程式層級設定，請使用 **Set-CsRgsConfiguration** Cmdlet。

只有在未定義自訂等候音樂時，才會於電話保留時播放預設等候音樂。通話內容僅適用於指派給互動式工作流程的佇列。若已啟用通話內容，代理人即可在接到電話時看見相關資訊，例如：來電者等候時間或工作流程問題和答案。

## 修改回應群組應用程式層級設定

1.  以 RTCUniversalServerAdmins 群組成員或支援回應群組的某個預先定義之管理角色成員的身分登入。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  在命令列中執行：
    
        Set-CsRgsConfiguration -Identity <name of service hosting Response Group> [-AgentRingbackGracePeriod <# seconds until call returns to agent after declined>] [-DefaultMusicOnHoldFile <audio file>] [-DisableCallContext <$true | $false>]
    
    例如：
    
        Set-CsRgsConfiguration -Identity "service:ApplicationServer:redmond.contoso.com" -AgentRingbackGracePeriod 30 -DisableCallContext $false
    
    若要指定音訊檔作為預設等候音樂，您必須先匯入音訊檔。例如：
    
        $x = Import-CsRgsAudioFile -Identity "service:ApplicationServer:redmond.contoso.com" -FileName "MusicWhileYouWait.wav" -Content (Get-Content C:\Media\ MusicWhileYouWait.wav -Encoding byte -ReadCount 0)
        Set-CsRgsConfiguration -Identity "service:ApplicationServer:redmond.contoso.com" -DefaultMusicOnHoldFile <$x>

## 請參閱

#### 其他資源

[Get-CsRgsConfiguration](get-csrgsconfiguration.md)  
[Set-CsRgsConfiguration](set-csrgsconfiguration.md)  
[Import-CsRgsAudioFile](import-csrgsaudiofile.md)

