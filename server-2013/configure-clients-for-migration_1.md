---
title: 設定用戶端以進行移轉
TOCTitle: 設定用戶端以進行移轉
ms:assetid: 8f17862b-d9d1-47f6-b248-51f4710f5030
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ688130(v=OCS.15)
ms:contentKeyID: 49890203
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 設定用戶端以進行移轉

 

_**上次修改主題的時間：** 2015-03-09_

本主題包含在您將用戶端移轉至 Lync Server 2013 之前建議應該採取的用戶端部署步驟。您應在 Office Communications Server 2007 R2 上進行這些設定變更。請務必在移轉之前執行這些步驟。如需詳細資訊，請參閱＜ [規劃 Lync Server 2013 中的用戶端和裝置](lync-server-2013-planning-for-clients-and-devices.md)＞。

## 移轉之前設定用戶端

1.  部署最新的 Office Communications Server 2007 R2 伺服器、用戶端及裝置更新 (Hotfix)：
    
      - [套用 Office Communications Server 2007 R2 更新](apply-office-communications-server-2007-r2-updates.md)
    
      - [Communicator 2007 R2 的累計更新套件說明](http://go.microsoft.com/fwlink/p/?linkid=335808) (機器翻譯)
    
      - [為裝置取得軟體更新](http://go.microsoft.com/fwlink/?linkid=335809) (英文)

2.  在 Office Communications Server 2007 R2 上，使用 \[用戶端版本篩選\]，只允許安裝了最新更新的 Office Communications Server 2007 R2 用戶端登入。

3.  在 Office Communications Server 2007 R2 上，使用 \[用戶端版本篩選\] 封鎖 Lync Server 2013 用戶端登入。遵循 \[設定用戶端版本篩選\] (網址為： [http://go.microsoft.com/fwlink/?linkid=202488\&clcid=0x404](http://go.microsoft.com/fwlink/?linkid=202488%26clcid=0x404)) 中說明的步驟，新增下表列出的版本篩選器。針對每個版本篩選器，指派 \[封鎖\] 動作。
    
    
    <table>
    <colgroup>
    <col style="width: 33%" />
    <col style="width: 33%" />
    <col style="width: 33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>用戶端</th>
    <th>使用者代理程式標頭</th>
    <th>版本</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Lync 2013</p></td>
    <td><p>OC</p></td>
    <td><p>15.*.*.*</p></td>
    </tr>
    <tr class="even">
    <td><p>Lync Web App</p></td>
    <td><p>CWA</p></td>
    <td><p>5.*.*.*</p></td>
    </tr>
    <tr class="odd">
    <td><p>Lync Phone Edition</p></td>
    <td><p>OCPhone</p></td>
    <td><p>4.*.*.*</p></td>
    </tr>
    </tbody>
    </table>

