---
title: 在 Lync Server 2013 中設定通話駐留設定
TOCTitle: 在 Lync Server 2013 中設定通話駐留設定
ms:assetid: 3bed9d09-8363-4fff-a220-f0f6d3a81241
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425886(v=OCS.15)
ms:contentKeyID: 49290655
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定通話駐留設定

 

_**上次修改主題的時間：** 2015-03-09_

如果不要使用預設的通話駐留設定，可以加以自訂。安裝通話駐留應用程式時，依據預設會設定全域設定。您可以修改全域設定，也可以指定網站特定設定。使用 **New-CsCpsConfiguration** Cmdlet 可建立新的網站特定設定。使用 **Set-CsCpsConfiguration** Cmdlet 可修改現有設定。

> [!NOTE]  
> 建議您至少設定 <strong>OnTimeoutURI</strong> 選項，作為當駐留通話逾時且回撥失敗時的後援目的地。



使用 **New-CsCpsConfiguration** Cmdlet 或 **Set-CsCpsConfiguration** Cmdlet 進行下列任何一項設定：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>此選項：</th>
<th>指定：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>CallPickupTimeoutThreshold</strong></p></td>
<td><p>從駐留通話之後到回撥原先接聽該通話的電話之前，需經過的時間長度。</p>
<p>此值必須以 hh:mm:ss 格式輸入，以指定小時、分鐘和秒數。最小值為 10 秒，最大值為 10 分鐘。預設值為 00:01:30。</p></td>
</tr>
<tr class="even">
<td><p><strong>EnableMusicOnHold</strong></p></td>
<td><p>駐留通話時是否對來電者播放音樂。</p>
<p>值為 True 或 False。預設為 True。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxCallPickupAttempts</strong></p></td>
<td><p>在將駐留通話轉接至 <strong>OnTimeoutURI</strong> 指定的後援統一資源識別元 (URI) 之前，需將駐留通話回撥至當初接聽該通話的次數。預設值為 1。</p></td>
</tr>
<tr class="even">
<td><p><strong>OnTimeoutURI</strong></p></td>
<td><p>在超過 <strong>MaxCallPickupAttempts</strong> 時，將未接聽的駐留通話路由至的使用者或回應群組的 SIP 位址。</p>
<p>值必須是以字串 sip: 開頭的 SIP URI。例如，sip:bob@contoso.com。預設沒有轉接位址。</p></td>
</tr>
</tbody>
</table>


## 設定通話駐留設定

1.  以 RTCUniversalServerAdmins 群組成員身分或使用[在 Lync Server 2013 中委派設定權限](lync-server-2013-delegate-setup-permissions.md)中描述的必要使用者權限，登入裝有 Lync Server 管理命令介面的電腦。

2.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

3.  執行：
    
        New-CsCpsConfiguration -Identity site:<sitename to apply settings> [-CallPickupTimeoutThreshold <hh:mm:ss>] -[EnableMusicOnHold <$true | $false>] [-MaxCallPickupAttempts <number of rings>] [-OnTimeoutURI sip:<sip URI for routing unanswered call>]
    
    > [!TIP]
    > 使用 <strong>Get-CsSite</strong> Cmdlet 來識別網站。如需詳細資訊，請參閱 Lync Server 管理命令介面文件。
    
    例如：
    
        New-CsCpsConfiguration -Identity site:Redmond1 -CallPickupTimeoutThreshold 00:01:00 -EnableMusicOnHold $false -MaxCallPickupAttempts 2 -OnTimeoutURI sip:bob@contoso.com

## 請參閱

#### 工作

[在 Lync Server 2013 中自訂通話駐留等候音樂](lync-server-2013-customize-call-park-music-on-hold.md)  

#### 其他資源

[New-CsCpsConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsCpsConfiguration)  
[Set-CsCpsConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsCpsConfiguration)  
[Get-CsSite](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsSite)

