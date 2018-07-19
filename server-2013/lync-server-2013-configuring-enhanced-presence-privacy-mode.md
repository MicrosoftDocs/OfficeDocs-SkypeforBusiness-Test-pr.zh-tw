---
title: 設定增強的顯示狀態隱私權模式
TOCTitle: 設定增強的顯示狀態隱私權模式
ms:assetid: e7a6b873-486d-4dfb-a967-c48f61f237f3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399028(v=OCS.15)
ms:contentKeyID: 49292649
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定增強的顯示狀態隱私權模式

 

_**上次修改主題的時間：** 2014-12-08_

使用者可以透過增強的目前狀態隱私權模式，限制只讓 Lync 2013 連絡人清單中所列的連絡人看到其目前狀態資訊。**New-CsPrivacyConfiguration** 與 **Set-CsPrivacyConfiguration** Cmdlet 擁有 EnablePrivacyMode 參數可控制這個選項。當 EnablePrivacyMode 設為 True 時，限制只讓連絡人看到目前狀態資訊的選項便會在 Lync 2013 狀態選項中提供。當 EnablePrivacyMode 設為 False 時，使用者可以選擇永遠讓每個人看到其目前狀態資訊，或依循系統管理員未來對隱私權模式所做的任何變更。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lync 2013 與 Lync 2010 隱私權設定不會被舊版 (Microsoft Office Communicator 2007 R2 或 Microsoft Office Communicator 2007) 接受。如果允許舊版 Office Communicator 登入，則 Lync 2013 使用者的狀態、連絡人資訊或圖片可能會讓未經授權者檢視。此外，如果 Lync 2013 使用者稍後使用舊版 Communicator 登入，則會重設其隱私權設定。<br />
基於這些原因，當您在移轉案例中啟用增強的目前狀態隱私權模式之前：
<ul>
<li><p>確認每個使用者都已安裝 Lync 2013。</p></li>
<li><p>定義用戶端版本原則規則，以防止舊版 Communicator 登入。</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 若要啟用增強的目前狀態隱私權模式

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  執行下列命令：
    
        Get-CsPrivacyConfiguration | Set-CsPrivacyConfiguration -EnablePrivacyMode $True
    
    此命令可為組織中目前使用中的所有隱私權組態設定啟用隱私權模式。

## 請參閱

#### 其他資源

[Get-CsPrivacyConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsPrivacyConfiguration)  
[New-CsPrivacyConfiguration](new-csprivacyconfiguration.md)  
[Set-CsPrivacyConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsPrivacyConfiguration)

