---
title: 設定會議加入頁面
TOCTitle: 設定會議加入頁面
ms:assetid: 036c9d03-ad95-4d63-a3d8-6cae1a8ad530
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204635(v=OCS.15)
ms:contentKeyID: 49289928
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定會議加入頁面

 

_**上次修改主題的時間：** 2015-03-09_

使用者按一下會議邀請中的會議連結時，會議加入頁面會偵測使用者的電腦上是否已安裝 Lync 2013 用戶端。 若已安裝用戶端，將會開啟該用戶端，然後加入會議。若未安裝用戶端，預設會開啟 2013 版的 Lync Web App。

如果想要允許使用者透過 Office Communicator 2007 R2 或 Lync 2010 Attendant 加入會議，可以修改會議加入頁面的行為。這些設定選項已從 Lync Server 2013 控制台中移除，但您可使用 CsWebServiceConfiguration Cmdlet 加以設定。

### 會議加入頁面 CsWebServiceConfiguration 參數

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>CsWebServiceConfiguration 參數</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ShowJoinUsingLegacyClientLink</p></td>
<td><p>如果設為 True，可讓使用 Lync 以外之用戶端應用程式加入會議的使用者，有機會使用 Office Communicator 2007 R2 加入會議。預設值為 False。</p></td>
</tr>
<tr class="even">
<td><p>ShowAlternateJoinOptionsExpanded</p></td>
<td><p>此參數設為 True 時，就會自動展開參加線上會議 (例如 Office Communicator 2007 R2) 的其他選項，並且顯示給使用者。設為 False (預設值) 時，這些選項仍然可用，但使用者必須自行顯示選項清單。</p></td>
</tr>
</tbody>
</table>


## 使用 Lync Server 2013 管理命令介面設定會議加入頁面

1.  啟動 Lync Server 2013 管理命令介面：依序按一下 \[開始\] 、\[所有程式\] 、\[ Microsoft Lync Server 2013\] 及 \[ Lync Server 管理命令介面\] 。

2.  執行下列 Cmdlet：
    
        Get-CsWebServiceConfiguration
    
    此 Cmdlet 會傳回 Web 服務設定。

3.  執行下列命令，並根據您的偏好將參數設定 True 或 False (此 Cmdlet 之參數的詳細資料請參閱 Lync Server 2013 管理命令介面 文件)：
    
        Set-CsWebServiceConfiguration -Identity global -ShowJoinUsingLegacyClientLink $True

