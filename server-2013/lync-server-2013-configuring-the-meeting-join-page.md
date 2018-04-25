---
title: Lync Server 2013：設定會議加入頁面
TOCTitle: 設定會議加入頁面
ms:assetid: 45880423-47f4-49af-b825-cbd8e3fc1046
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204861(v=OCS.15)
ms:contentKeyID: 49290776
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定會議加入頁面

 

_**上次修改主題的時間：** 2015-03-09_

使用者按一下會議邀請中的會議連結時，會議加入頁面會偵測使用者的電腦上是否已安裝 Lync 2013 用戶端。如果已安裝用戶端，則用戶端會開啟並加入會議。如果未安裝用戶端，依預設會開啟 2013 版本的 Lync Web App。

如果您希望允許使用者透過 Office Communicator 2007 R2 或 Lync 2010 Attendant 加入會議，可以修改會議加入頁面的行為。雖然 Lync Server 2013 控制台中已移除這些設定選項，但您可使用 Set-CsWebServiceConfiguration Cmdlet 進行設定。

### 會議加入頁面 Set-CsWebServiceConfiguration 參數

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Set-CsWebServiceConfiguration 參數</th>
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

2.  如果要檢視 Web 服務組態設定，請執行下列 Cmdlet：
    
        Get-CsWebServiceConfiguration

3.  執行參數設定為 True 或 False (取決於偏好設定) 的下列命令 (如需此 Cmdlet 的參數詳細資訊，請參閱＜Lync Server 2013 管理命令介面＞文件中的 [Set-CsWebServiceConfiguration](set-cswebserviceconfiguration.md))：
    
        Set-CsWebServiceConfiguration -Identity global -ShowJoinUsingLegacyClientLink $True

## 請參閱

#### 其他資源

[Set-CsWebServiceConfiguration](set-cswebserviceconfiguration.md)

