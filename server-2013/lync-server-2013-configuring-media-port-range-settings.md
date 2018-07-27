---
title: 設定媒體連接埠範圍設定
TOCTitle: 設定媒體連接埠範圍設定
ms:assetid: 2c4b7c0b-0dce-48f4-a489-336d6e526f7c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ204770(v=OCS.15)
ms:contentKeyID: 49290441
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定媒體連接埠範圍設定

 

_**上次修改主題的時間：** 2015-03-09_

媒體連接埠設定會顯著地影響用戶端效能，而應加以設定。您可以使用 Lync Server 管理命令介面設定這些設定。

### 媒體連接埠範圍設定

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>設定</th>
<th>說明</th>
<th>Lync Server 管理命令介面 Cmdlet</th>
<th>Cmdlet 參數</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Portrange\Enabled</p></td>
<td><p>指定伺服器傳送的連接埠範圍是否應該供用戶端用於媒體和訊號。配合使用子機碼值 MinMediaPort 和 MaxMediaPort。</p></td>
<td><p><strong>CsConferencingConfiguration</strong></p></td>
<td><p>ClientMediaPortRangeEnabled</p></td>
</tr>
<tr class="even">
<td><p>Portrange\MinMediaPort</p></td>
<td><p>指定用於媒體的起始連接埠號碼。與 MaxMediaPort 合併使用可指定連接埠範圍。建議最小範圍為 40 個連接埠。</p></td>
<td><p><strong>CsConferencingConfiguration</strong></p></td>
<td><p>ClientMediaPort (代表用於用戶端媒體的起始連接埠號碼)</p></td>
</tr>
<tr class="odd">
<td><p>Portrange\MaxMediaPort</p></td>
<td><p>指定用於媒體的最高連接埠號碼。與 MinMediaPort 合併使用可指定連接埠範圍。建議最小範圍為 40 個連接埠。</p></td>
<td><p><strong>CsConferencingConfiguration</strong></p></td>
<td><p>ClientMediaPortRange (表示可供用戶端媒體使用的連接埠總數；預設值為 40)</p></td>
</tr>
</tbody>
</table>


## 設定媒體連接埠範圍設定

1.  啟動 Lync Server 管理命令介面：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 管理命令介面\]。

2.  執行下列 Cmdlet：
    
        Get-CsConferencingConfiguration
    
    此 Cmdlet 傳回會議設定。

3.  使用想要變更的參數及值，執行下列 Cmdlet (如需此 Cmdlet 之參數的詳細資訊，請參閱 Lync Server 管理命令介面文件)：
    
        Set-CsConferencingConfiguration
    
    > [!NOTE]  
    > 您可以建立特定網站的其他會議設定集。請搭配使用 <strong>New- CsConferencingConfiguration</strong> Cmdlet 與網站身分識別。當您建立網站的新會議設定時，網站設定的優先順序高於全域設定。如需詳細資訊，請參閱 Lync Server 管理命令介面文件。
    

