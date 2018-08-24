---
title: Lync Server 2013：設定行動原則
TOCTitle: 設定行動原則
ms:assetid: 595536e0-9bb3-49a3-8d13-1a77351ebc62
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh690018(v=OCS.15)
ms:contentKeyID: 49291002
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定行動原則

 

_**上次修改主題的時間：** 2013-02-13_

    Some information in this topic pertains to Cumulative Updates for Lync Server 2013: February 2013.

Lync Server 2013 提供行動原則，可判斷哪些人可以使用行動功能 (從公司撥號、VoIP 或視訊)，並可判斷 VoIP 或視訊是否需要 WiFi。「從公司撥號」功能可以讓行動使用者在行動電話上使用公司電話號碼來撥打及接收電話，而不是使用行動電話號碼。此功能可以防止受話方看到發話者的行動電話號碼，並且可以讓使用者避免產生撥出電話的費用。設定 VoIP 和視訊可讓使用者接收及撥打 VoIP 通話和視訊。WiFi 使用方式的設定可定義使用者裝置是否將需要使用 WiFi 網路，而非透過行動數據網路。

依預設會啟用行動性、「從公司撥號」及 VoIP 和視訊功能。要求 VoIP 和視訊使用 WiFi 的設定會停用。系統管理員可以執行 Cmdlet 來決定哪些人可以存取這些功能。您可以全域關閉選項，或依網站或使用者。

若要能夠使用行動功能和「從公司撥號」功能，使用者必須符合下列先決條件：

  - 使用者必須能夠使用 Lync Server 2013。

  - 使用者必須能夠使用 企業語音。

  - 使用者必須被指派 \[EnableMobility\] 選項設為 True 的行動原則。

若要讓使用者能夠使用「從公司撥號」，使用者必須符合下列兩項先決條件：

  - 使用者必須被指派已選取 \[使電話同時響鈴\] 選項的語音原則。

  - 必須為使用者指派 **\[EnableOutsideVoice\]** 選項設為 True 的行動原則。

> [!NOTE]  
> 未啟用 企業語音的使用者則可使用行動裝置撥打 Lync 至 Lync VoIP 通話，或使用行動裝置上的 [按一下加入] 連結來加入會議，只要您有將語音原則的適當選項指派給那些使用者。如需詳細資訊，請參閱＜ <a href="lync-server-2013-defining-your-mobility-requirements.md">定義 Lync Server 2013 的行動需求</a>＞。



如需讓使用者能夠使用 Lync Server 2013 的詳細資訊，請參閱＜ [停用或重新啟用 Lync Server 的使用者帳戶](lync-server-2013-disable-or-re-enable-user-account-for-lync-server.md)＞。如需讓使用者能夠使用 企業語音的詳細資訊，請參閱＜ [在 Lync Server 2013 中為使用者啟用企業語音](lync-server-2013-enable-users-for-enterprise-voice.md)＞。如需設定語音原則選項的詳細資訊，請參閱＜ [在 Lync Server 2013 中修改語音原則和設定 PSTN 使用方式記錄](lync-server-2013-modify-a-voice-policy-and-configure-pstn-usage-records.md)＞。

## 修改全域行動原則

1.  以 CsAdministrator 角色成員的身分登入任一部已安裝 Lync Server 管理命令介面和 Ocscore 的電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  全域關閉對行動性和「從公司撥號」功能的存取權。在命令列中輸入：
    
        Set-CsMobilityPolicy -EnableMobility $False -EnableOutsideVoice $False
    
    > [!NOTE]  
    > 您不需要關閉對行動性的存取權，即可關閉「從公司撥號」。不過，如果您要關閉行動性，也必須關閉「從公司撥號」。
    


## 依網站修改行動原則

1.  以 CsAdministrator 角色成員的身分登入任一部已安裝 Lync Server 管理命令介面和 Ocscore 的電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  建立網站層級原則，並關閉 VoIP 和視訊，且依網站啟用「要求 IP 音訊和 IP 視訊使用 WiFi」。在命令列中輸入：
    
        New-CsMobilityPolicy -Identity site:<site identifier> -EnableIPAudioVideo $False -RequireWiFiForIPAudio $True -RequireWiFiForIPVideo $True

## 依使用者修改行動原則

1.  以 CsAdministrator 角色成員的身分登入任一部已安裝 Lync Server 管理命令介面和 Ocscore 的電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  建立使用者層級行動原則，並依使用者關閉行動性和「從公司撥號」。在命令列中輸入：
    
        New-CsMobilityPolicy -Identity <policy name> -EnableMobility $False -EnableOutsideVoice $False
        Grant-CsMobilityPolicy -Identity <user identifier> -PolicyName <policy name>
    
    您不需要關閉對行動性的存取權，即可關閉「從公司撥號」。不過，如果您要關閉行動性，也必須關閉「從公司撥號」。
    
    例如：
    
        New-CsMobilityPolicy "tag:disableOutsideVoice" -EnableOutsideVoice $False
        Grant-CsMobilityPolicy -Identity -MobileUser1@contoso.com -PolicyName Tag:disableOutsideVoice

## 請參閱

#### 工作

[停用或重新啟用 Lync Server 的使用者帳戶](lync-server-2013-disable-or-re-enable-user-account-for-lync-server.md)  
[在 Lync Server 2013 中為使用者啟用企業語音](lync-server-2013-enable-users-for-enterprise-voice.md)  
[在 Lync Server 2013 中修改語音原則和設定 PSTN 使用方式記錄](lync-server-2013-modify-a-voice-policy-and-configure-pstn-usage-records.md)  

#### 概念

[定義 Lync Server 2013 的行動需求](lync-server-2013-defining-your-mobility-requirements.md)  

#### 其他資源

[New-CsMobilityPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsMobilityPolicy)  
[Set-CsMobilityPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsMobilityPolicy)  
[Get-CsMobilityPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsMobilityPolicy)  
[Grant-CsMobilityPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Grant-CsMobilityPolicy)  
[Remove-CsMobilityPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsMobilityPolicy)

